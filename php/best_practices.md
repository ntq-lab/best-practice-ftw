# PHP Best practices

## 1. Use an IDE

- For now: PHPStorm is the best
- Keep your IDE up to date
- Use of shortcuts: make shortcuts for all common tasks => improve productivity
- IDE tools:
  - DB
  - Git
  - Code quality 
  - Startup tasks: automatically run Grunt, Vagrant at project startup
  
  - ...

## 2. Follow strictly a coding standard
- PSR-1: www.php-fig.org/psr/psr-1/
- PSR-2: www.php-fig.org/psr/psr-2/
- Framework specific...

## 3. Coding

### 1. Readability of code blocks
BAD :(
```php
if ($foo) {
    $bar = 1;
}
if ($spam) {
    $ham = 1;
}
if ($pinky) {
    $brain = 1;
}
```

GOOD :)
```php
if ($foo) {
    $bar = 1;
}

if ($spam) {
    $ham = 1;
}

if ($pinky) {
    $brain = 1;
}
```

### 2. Try not to use else
BAD :(
```php
public function addThreeInts($first, $second, $third) {
    if (is_int($first)) {
        if (is_int($second)) {
            if (is_int($third)) {
                $sum = $first + $second + $third;
            } else {
                return null;
            }
        } else {
            return null;
        }
    } else {
        return null;
    }

    return $sum;
}
```

GOOD :)
```php
public function addThreeInts($first, $second, $third) {
    if (!is_int($first)) {
        return null;
    }

    if (!is_int($second)) {
        return null;
    }

    if (!is_int($third)) {
        return null;
    }

    return $first + $second + $third;
}
```

### 3. Redirect after a successful POST request
BAD :(
```php
if ($post) {
    // Process form data here.
}

// Render html output
```

GOOD :)
```php
// Process form data here.
 
// If the form submission was successful.
if($success){
    //Redirect the user.
    header('Location: page.php?msg=success');
    exit;
}
```

### 4. Do not close your PHP tags

http://php.net/basic-syntax.phptags

http://stackoverflow.com/questions/4410704/why-would-one-omit-the-close-tag

### 5. Always use PHPDoc
- [x] Get IDE suggestions
- [x] Generate documentation

```php
<?php


namespace ME\MasterApiSDK;


use ME\MasterApiSDK\Exceptions\MasterApiSDKException;

/**
 * Class PublicApi
 *
 * @package ME\MasterApiSDK
 *
 * @method PublicApiServices\AuthenticationService authentication()
 * @method PublicApiServices\CategoriesService categories()
 * @method PublicApiServices\EventsService events()
 * @method PublicApiServices\SubThemesService subThemes()
 * @method PublicApiServices\MainThemesService mainThemes()
 */
class PublicApi extends AbstractApi
{
    /**
     * @inheritdoc
     */
    public function getBaseUrl()
    {
        return 'https://master-api.managementevents.com/api/web/v1';
    }

    /**
     * Shorthand to access the API services.
     *
     * @param $name
     * @param null $arguments
     * @return mixed
     * @throws MasterApiSDKException
     */
    public function __call($name, $arguments)
    {
        $serviceClass = "ME\\MasterApiSDK\\PublicApiServices\\" . ucfirst($name) . "Service";

        if (!(new \ReflectionClass($serviceClass))->isInstantiable()) {
            throw new MasterApiSDKException("{$serviceClass} is not instantiable");
        }

        return new $serviceClass($this);
    }

}
```
### 6. Always use === for comparison (especially when compare to null or false values)
BAD (even ERROR!)
```php
$mystring = 'abc';
$findme = 'a';

$pos = strpos($mystring, $findme);
if (!$pos) {
}
//OR
if ($pos == false) {
}
```

GOOD :)
```php
$mystring = 'abc';
$findme = 'a';

$pos = strpos($mystring, $findme);
if ($pos === false) {
}
```

### 7. Chunk for bulk processing
- When process large data you might face out of memory problem
=> Break data to chunks and process each chunk
=> Suitable for console command

```php
    /**
     * Chunk the results of the query.
     *
     * @param ActiveQueryInterface $query
     * @param int $size
     * @param callable $callback
     *
     * @return bool
     */
    protected function chunk(ActiveQueryInterface $query, $size, callable $callback)
    {
        $pageNumber = 1;

        $results = $this->paginateResults($query, $pageNumber, $size)->all();

        while(count($results) > 0)
        {
            // On each chunk result set, pass them to the callback and then let the
            // developer take care of everything within the callback. This allows to
            // keep the memory low when looping through large result sets.
            if (call_user_func($callback, $results) === false) {
                return false;
            }
            
            $pageNumber++;
            
            $results = $this->paginateResults($query, $pageNumber, $size)->all();
        }

        return true;
    }
    
    -----
    
    $this->solutionProviderRepository->chunk(
            $query,
            500,
            function ($solutionProviders) use (&$migrateCount) {

                foreach ($solutionProviders as $solutionProvider) {
                    $migrateResult = $this->managerService->migrateLocation($solutionProvider, $placeDetail, $errors);

                    switch ($migrateResult) {
                        case SolutionProviderManagerService::LOCATION_MIGRATION_API_ERROR:
                            $this->stdout("Could not migrate location for solution provider $solutionProvider->name with city $solutionProvider->city. Errors: \n", Console::FG_RED);
                            $this->outputMigrationErrors($errors);
                            break;
                        case SolutionProviderManagerService::LOCATION_MIGRATION_ALREADY_MIGRATED:
                            $this->stdout("Skip solution provider $solutionProvider->name with city $solutionProvider->city (already migrated) \n", Console::FG_YELLOW);
                            break;
                        case SolutionProviderManagerService::LOCATION_MIGRATION_CITY_NOT_FOUND:
                            $this->stdout("Skip solution provider $solutionProvider->name with city $solutionProvider->city (city not found) \n", Console::FG_YELLOW);
                            break;
                        case SolutionProviderManagerService::LOCATION_MIGRATION_SUCCESS:
                            $this->stdout("Migrated location for solution provider $solutionProvider->name with city $solutionProvider->city \n", Console::FG_GREEN);
                            $this->outputPlaceDetail($placeDetail);
                            $migrateCount++;
                            break;
                    }
                }
            }
        );
```
## 4. Testing
### 1. Use @dataprovider for a group of test cases
https://phpunit.de/manual/current/en/writing-tests-for-phpunit.html#writing-tests-for-phpunit.data-providers

### 2. Always write test method before writing the test body
BAD :(
```php
    /** @test */
    public function it_finds_media_file_by_ids()
    {
        $mediaFiles = $this->mediaFileRepository->findByIds([1, 2]);

        $this->assertCount(2, $mediaFiles);
        $this->assertEquals($this->mediaFile('media-file1')->filename, $mediaFiles[0]->filename);
        $this->assertEquals($this->mediaFile('media-file2')->filename, $mediaFiles[1]->filename);
    }

    /** @test */
    public function it_delete_by_ids()
    {
        $deletedCount = $this->mediaFileRepository->deleteByIds([1, 2]);

        $this->assertEquals(2, $deletedCount);
        $this->tester->dontSeeRecord(MediaFile::class, ['id' => 1]);
        $this->tester->dontSeeRecord(MediaFile::class, ['id' => 2]);
    }
    
    ...
```

GOOD :)
```
    public function it_finds_media_file_by_id()
    {
    }

    public function it_finds_media_file_by_ids()
    {
    }

    public function it_delete_by_ids()
    {
    }

    public function it_return_paged_media_files()
    {
    }

    public function it_can_sort_media_files_by()
    {
    }

    public function it_can_filter_by_search_query()
    {
    }
```

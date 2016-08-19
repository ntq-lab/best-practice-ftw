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
// Demostration will be placed here later
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
    // Demostration will be placed here later
```
## 4. Testing
### 1. Use @dataprovider for a group of test cases
https://phpunit.de/manual/current/en/writing-tests-for-phpunit.html#writing-tests-for-phpunit.data-providers

### 2. Always write test method before writing the test body
BAD :(
```php
    // Demostration will be placed here later
```

GOOD :)
```
    // Demostration will be placed here later
```

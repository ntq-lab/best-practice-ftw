##Giới thiệu

###**SOLID** - 5 nguyên lý của thiết kế hướng đối tượng

**S** – Single-responsiblity principle (nguyên lý đơn nhiệm)

**O** – Open-closed principle (nguyên lý mở rộng - hạn chế)

**L** – Liskov substitution principle (nguyên lý thay thế Liskov)

**I** – Interface segregation principle (nguyên lý giao diện phân biệt - hay phân tách interface)

**D** – Dependency Inversion Principle (nguyên lý nghịch đảo phụ thuộc)
##Nội dung
####1. **S** – Single-responsiblity principle (nguyên lý đơn nhiệm)
Nội dung: Một class hay method chỉ nên giữ 1 trách nhiệm duy nhất.

Giải thích: Một class có quá nhiều chức năng cũng sẽ trở nên cồng kềnh và phức tạp.
Khi yêu cầu thay đổi, một class quá cồng kềnh thì việc thay đổi code rất khó khăn và mất nhiều thời gian.
Áp dụng nguyên lý đơn nhiệm chia các chức năng thành nhiều class khác nhau giúp việc quản lý, mở rộng, bảo trì code thuận tiện hơn.

Lưu ý:

Về bản chất nguyên lý này chỉ là hướng dẫn không phải là nguyên tắc tuyệt đối.
Có những trường hợp như các class Helper xét cho cùng toàn bộ các hàm trong class này đều thực hiện những tác vụ nhỏ nên nếu số lượng hàm ít vẫn có thể cho các hàm này vào cùng 1 class.

Tuy nhiên khi số lượng hàm tăng lên quá nhiều thì nên cân nhắc sử dụng nguyên lý này để chia nhỏ module thuận tiện cho việc quản lý.

Việc hiểu và áp dụng nguyên này giúp cho việc viết code dễ đọc, dễ hiểu, dễ quản lý hơn.
Tuy nhiên nguyên đơn nhiệm là nguyên lý đơn giản nhưng khó áp dụng đúng, việc xác định khi nào cần áp dụng khi nào không còn phụ thuộc vào việc người code xác định được đúng chức năng của module đang làm.

####2. **O** – Open-closed principle (OCP - nguyên lý mở rộng - hạn chế)
Nội dung: Có thể mở rộng 1 module nhưng hạn chế sửa đổi bên trong module đó.

Giải thích: Theo nguyên lý một module phải đáp ứng 2 điều kiện:
 - Dễ mở rộng: có thể dễ dàng nâng cấp, mở rộng, thêm tính năng mới cho module khi có yêu cầu.
 - Hạn chế sửa đổi: Hạn chế hoặc cấm việc sửa source code của module sẵn có.
Thông thường việc mở rộng thêm chức năng thì phải viết thêm code, vậy để thiết kế ra một module có thể dễ dàng mở rộng nhưng lại hạn chế sửa đổi code ta cần làm gì.
Cách giải quyết là tách những phần dễ thay đổi ra khỏi phần khó thay đổi mà vẫn đảm bảo không ảnh hưởng đến phần còn lại.

Ví dụ:

Đặt vấn đề: Ta cần 1 lớp đảm nhận việc kết nối đến CSDL. Thiết kế ban đầu chỉ có SQL Server và MySQL. Thiết kế ban đầu có dạng như sau:
```php
class ConnectionManager
{
    public function doConnection(Object $connection)
    {
        if($connection instanceof SqlServer) {
            //connect with SqlServer
        } elseif($connection instanceof MySql) {
            //connect with MySql
        }
    }
}
```

Sau đó yêu cầu đặt ra phải kết nối thêm đến Oracle và một vài hệ CSDL khác.
Để thêm chức năng ta phải thêm vào code những khối esleif khác, việc này làm code cồng kềnh và khó quản lý hơn.

Giải pháp:
 - Áp dụng Abstract thiết kế lại các lớp SqlServer, MySql, Oracle...
 - Các lớp này đều có chung nhiệm vụ tạo kết nối đến csdl tương ứng có thể gọi chung là Connection.
 - Cách thức kết nối đến csdl thay đổi tùy thuộc vào từng loại kết nối nhưng có thể gọi chung là doConect.
 - Vậy ta có lớp cơ sở Connection có phương thức doConnect, các lớp cụ thể là SqlServer, MySql, Oracle... kế thừa từ Connection và overwrite lại phương thức doConnect phù hợp với lớp đó.

Thiết kế sau khi làm lại có dạng như sau:
```php
abstract class Connection()
{
        public abstract function doConnect();
}

class SqlServer extends Connection
{
    public function doConnect()
    {
        //connect with SqlServer
    }
}

class MySql extends Connection
{
    public function doConnect()
    {
        //connect with MySql
    }
}

class ConnectionManager
{
    public function doConnection(Connection $connection)
    {
        //something
        //.................
        //connection
        $connection->doConnect();
    }
}
```

Với thiết kế này khi cần kết nối đến 1 loại csdl mới chỉ cần thêm 1 lớp mới kế thừa Connection mà không cần sửa đổi code của lớp ConnectionManager, điều này thỏa mãn 2 điều kiện của nguyên lý OCP.

Lưu ý:

Trên thực tế không có mô hình nào thỏa mãn hoàn toàn OCP, sẽ luôn có những thay đổi khiến mô hình không thỏa mãn OCP.

Ví dụ với yêu cầu show ra toàn bộ các hình được đưa vào ta có mô hình sau:
```php
abstract class Shape
{
    public abstract function Draw();
}

class Square extends Shape
{
    public function Draw()
    {
        // show Square
    }
}

class Circle extends Shape
{
    public function Draw()
    {
        // show Circle
    }
}

class DrawShape
{
    public function DrawAllShape(array $shapes)
    {
        // $shapes is an array of shape object
        foreach($shapes as $shape) {
            $shape->draw();
        }
    }
}
```
Nếu các thay đổi đưa ra như thêm các hình mới thì mô hình vẫn thỏa mãn OCP.

Nhưng nếu yêu cầu thay đổi là show hình tròn trước hoặc không show ra những hình đặc biệt thì chúng ta vẫn phải thay đổi code của function DrawAllShape và việc này làm thiết kế không thỏa mãn OCP.

Khi áp dụng nguyên lý này để thiết kế cần phải xác định được những thứ dễ bị thay đổi để thiết kế phù hợp với thay đổi đó. Việc này cần kinh nghiệm và một tầm nhìn xa.
####3. **L** – Liskov substitution principle (nguyên lý thay thế Liskov)
Nội dung: Lớp B được gọi là kế thừa từ lớp A khi và chỉ khi với mọi hàm F thao tác trên các đối tượng của A, cách cư xử (behavior) của F không đổi khi thay thế các đối tượng của A bằng các đối tượng của B.

Giải thích:
 - Nội dung nguyên lý có thể hiểu như sau trong một chương trình, các object của class con có thể thay thế class cha mà không làm thay đổi tính đúng đắn của chương trình.
 - Mối quan hệ IS-A (là một) thường được dùng để xác định kế thừa. Lớp B kế thừa lớp A khi B là một A, do đó B có thể thay thay thế hoàn toàn cho A mà không làm mất đi tính đúng đắn.

Ví dụ: Thực tế ta biết hình vuông là hình chữ nhật đặc biệt có chiều cao = chiều rộng.

Vậy lớp hình vuông có phải con của lớp hình chữ nhật.

Xem xét mối quan hệ kế thừa giữa hình vuông và hình chữ nhật như sau:
```php
class Rectangle
{
    protected $m_width;
    protected $m_height;

    public function setWidth(int $width) {
        $this->m_width = $width;
    }

    public function setHeight(int $height) {
        $this->m_height = $height;
    }

    public function getWidth() {
        return $this->m_width;
    }

    public function getHeight() {
        return $this->m_height;
    }

    public function getArea() {
        return $this->m_width * $this->m_height;
    }
}

class Square extends Rectangle
{
    public function setWidth(int $width) {
        $this->m_width = $width;
        $this->m_height = $width;
    }

    public function setHeight(int $height) {
        $this->m_height = $height;
        $this->m_width = $height;
    }
}
```
Theo nguyên lý Liskov thì lớp Square có thể thay thế lớp Rectangle nên ta thực hiện việc test như sau:
```php
class Test
{
    public function checkArea(Rectangle $r)
    {
        $r->setWidth(10);
        $r->setHeight(5);

        if($r->getArea() == 50) {
            return 'true';
        }

        return 'false';
    }
}

$test = new Test;
echo 'Test with Rectangle: '.$test->checkArea(new Rectangle).PHP_EOL;// Test with Rectangle: true
echo 'Test with Square: '.$test->checkArea(new Square).PHP_EOL;// Test with Rectangle: false
```
Phương thức test hoạt động đúng (50) khi `$r` là một thể hiện của `Rectangle` nhưng khi thay thế `$r` là thể hiện của `Square` thì kết quả là `false` (25).

Lớp `Square` đã làm mất đi tính đúng đẵn của chương trình.

Vậy hình vuông không phải là 1 hình chữ nhật (?).

Xét về mặt hành vi thì 1 hình vuông không phải là 1 hình chữ nhật vì hành vi của hình vuông không thỏa mãn yêu cầu của hàm checkArea.

Lưu ý & kết luận:

Trong đời sống, `A` là `B` (`hình vuông` là `hình chữ nhật`) không có nghĩa là class `A` nên kế thừa class `B`.

Trong lập trình chỉ cho class `A` kế thừa class `B` khi class `A` thay thế được cho class `B`.

Cần xem xét các đối tượng về mặt hành vi chứ không nên sử dụng những mối quan hệ trong đời thật.
####4. **I** – Interface segregation principle (ISP - nguyên lý tách biệt giao tiếp hay phân tách interface)
Nội dung: Client không nên phụ thuộc vào giao tiếp (interface) mà chúng không sử dụng.

Giải thích:

Khi viết các giao tiếp (interface) chỉ nên thêm những phương thức mà nó cần phải có.

Nếu thêm các phương thức không cần thiết vào 1 interface các lớp thực hiện giao tiếp (class implement interface) sẽ bị bắt buộc thực thi những phương thức không cần thiết đó.

Điều này dẫn đến sự dư thừa trong thực thể.

Ví dụ:

Đặt vấn đề: Xây dựng 1 interface Phone, các lớp SmartPhone, PhoneBox implement Phone.
```php
interface Phone
{
    public function call();
    public function sms();
    public function picture();
}

class SmartPhone implements Phone
{
    public function call()
    {
        // do call
    }

    public function sms()
    {
        // send sms
    }

    public function picture()
    {
        // take picture
    }
}

class PhoneBox implements Phone
{
    public function call()
    {
        // do call
    }

    public function sms()
    {
        throw new Exception("PhoneBox can't send SMS");
    }

    public function picture()
    {
        throw new Exception("PhoneBox can't take picture");
    }
}
```
Nếu lớp Phone có thêm các phương thức mới thì các lớp SmartPhone, PhoneBox sẽ phải thay đổi theo trong khi nó không cần hoặc không thế thực hiện.

Giải pháp:
 - Chia nhỏ interface Phone thành những interface mang nhiệm vụ đặc thù
 - Các lớp SmartPhone, PhoneBox implement interface đặc thù mà nó cần
```php
interface Callable()
{
    public function call();
}

interface Smsable()
{
    public function sms();
}

interface Pictureable()
{
    public function sms();
}

class SmartPhone implements Callable, Smsable, Pictureable
{
    public function call()
    {
        // do call
    }

    public function sms()
    {
        // send sms
    }

    public function picture()
    {
        // take picture
    }
}

class PhoneBox implements Callable
{
    public function call()
    {
        // do call
    }
}
```
Như vậy khi mở rộng ta thêm các interface đặc thù với chức năng mở rộng thì sẽ không ảnh hưởng đến các lớp dẫn xuất.

Lưu ý & kết luận:
 - Nguyên lý ISP (tách biệt giao tiếp) có mối liên hệ với nguyên lý OCP (nguyên lý mở rộng - hạn chế).
 - Vi phạm ISP có khả năng dẫn tới sự vi phạm OCP.
 - Những lớp trừu tượng chứa quá nhiều thuộc tính và chức năng gọi là những lớp bị ô nhiễm (polluted).
 - Các lớp dẫn xuất phụ thuộc vào polluted interface làm tăng sự kết dính giữa các thực thể.
 - Khi nâng cấp, sửa đổi đòi hỏi các interface này thay đổi, các lớp dẫn xuất này buộc phải thay đổi theo, điều này vi phạm nguyên lý OCP ().
####5. **D** – Dependency Inversion Principle (DIP - nguyên lý nghịch đảo phụ thuộc)
Nội dung:
 - Module ở level cao hơn không nên phụ thuộc vào module ở level thấp hơn mà cả 2 nên phụ thuộc vào sự trừu tượng (abstractions).
 - Sự trừu tượng (abstraction) không nên phụ thuộc vào chi tiết (details) mà ngược lại chi tiết nên phụ thuộc vào sự trừu tượng.

Giải thích:

Có thể hiểu nguyên lí này như sau: những thành phần trong 1 chương trình chỉ nên phụ thuộc vào những cái trừu tượng (abstraction). Những thành phần trừu tượng không nên phụ thuộc vào các thành phần mang tính cụ thể mà nên ngược lại.

Những cái trừu tượng (abstraction) là những cái ít thay đổi và biến động, nó tập hợp những đặc tính chung nhất của những cái cụ thể. Những cái cụ thể dù khác nhau thế nào đi nữa đều tuân theo các quy tắc chung mà cái trừu tượng đã định ra. Việc phụ thuộc vào cái trừu tượng sẽ giúp chương trình linh động và thích ứng tốt với các sự thay đổi diễn ra liên tục.

Ví dụ:
Đặt vấn đề: Ta cần 1 lớp đảm nhiệm chức năng thông báo khi nhận được 1 event từ hệ thống. Thiết kế ban đầu có dạng như sau:
```php
class Notice
{
    public function pushNotification()
    {
        //push notic
    }
}

class EventListener
{
    public function listen($event)
    {
        $notice = new Notice;
        $notice->pushNotification();
    }
}
```
Như thiết kế này lớp EventListener muốn hoạt động thì phụ thuộc vào lớp Notice.

Khi yêu cầu thay đổi ta cần 1 số event thì thông báo 1 số event thì ghi lại log. Lúc này ta thêm 1 lớp LogWriter và sửa code của hàm listen():
```php
class LogWriter
{
    public function writeLog()
    {
        // write something
    }
}

class EventListener
{
    public function listen($event)
    {
        if($event == 'notice') {
            $notice = new Notice;
            $notice->pushNotification();
        } elseif($event == 'write') {
            $writer = new LogWriter;
            $writer->writeLog();
        }
    }
}
```
Như vậy với mỗi yêu cầu tăng thêm lớp EventListener sẽ càng phụ thuộc nhiều lớp, đồng thời phải sửa hàm listen() nhiều lần điều này vi phạm nguyên lý OCP (nguyên lý mở rộng - hạn chế).

Giải pháp:
 - Xây dựng 1 interface Handler, các lớp cụ thể Notice, LogWriter sẽ implements Handler.
 - Lớp EventListener phụ thuộc vào Handler thay vì các lớp cụ thể Notice, LogWriter.
```php
interface Handler
{
    public function fire();
}

class Notice implements Handler
{
    public function fire()
    {
        //push notic
    }
}

class LogWriter implements Handler
{
    public function fire()
    {
        // write something
    }
}

class EventListener
{
    public function listen(Handler $event)
    {
        $event->fire();
    }
}
```
Như vậy lớp EventListener không còn phụ thuộc vào các lớp cụ thể mà chỉ phụ thuộc vào 1 lớp trừu tượng Handler, ta có thể thêm các lớp cụ thể mà không hề ảnh hưởng đến lớp EventListener.

Lưu ý & kết luận:

Nguyên lý DIP (nghịch đảo phụ thuộc) có mối liên hệ với nguyên lý OCP (nguyên lý mở rộng - hạn chế). Vi phạm DIP có khả năng dẫn tới sự vi phạm OCP.

Dependency Inversion Principles != Dependency Injection.

Dependency Injection chỉ là 1 trong những pattern để thực hiện Dependency Inversion Principles.


> 
# Introducing method

- Trong Java, một lớp (class) thường bao gồm biến instance và phương thức (method). Phương thức giúp thao tác với dữ liệu trong lớp và cung cấp giao diện để tương tác với đối tượng.
- Cú pháp: 
```java
type name(parameter-list) {  
    // body của phương thức 
    return value; // khong bat buoc 
}
```
- Trong đó: 
  * type: Kiểu dữ liệu trả về (hoặc `void` nếu phương thức không trả về gì).
  * name: Tên phương thức (tuân theo quy tắc đặt tên biến).
  * parameter-list: Danh sách tham số (nếu có).
- Một phương thức có thể trả về giá trị, nhưng cần chú ý: 
  * Khi return được thực thi, chương trình sẽ thoát khỏi phương thức ngay lập tức.
  * Mọi dòng code sau return sẽ không được thực thi.
  * Nếu phương thức có kiểu trả về (khác void), thì return phải trả về một giá trị đúng với kiểu dữ liệu đã khai báo.

## Thêm method vào class Box
- Như ở những post trước, khi cần tình thể tích của Box, chúng ta cần truy cập các giá trị width, depth, height của 1 đối tượng Box và thực hiện tính toán, thì với method, chúng ta có thể tạo ra 1 method thực hiện tính thể tích: 
```java
 // Now, volume() returns the volume of a box.
class Box {
    double width;
    double height;
    double depth;

    // compute and return volume
    double volume() {
        return width * height * depth;
    }
}

class BoxDemo {
    public static void main(String args[]) {
        Box mybox1 = new Box();
        double vol;

        // assign values to mybox1's instance variables
        mybox1.width = 10;
        mybox1.height = 20;
        mybox1.depth = 15;

        // get volume of first box
        vol = mybox1.volume();
        System.out.println("Volume is " + vol);
    }
}

```
## Constructor
- Constructor là một phương thức (method) đặc biệt giúp khởi tạo đối tượng ngay khi nó được tạo ra:
  * Constructor có cùng tên với lớp chứa nó và không có kiểu trả về (kể cả void)
  * Nếu không có constructor nào được định nghĩa, Java sẽ tự động tạo một constructor mặc định (như ở những ví dụ trước), khởi tạo các biến instance về giá trị mặc định (số → 0, boolean → false, object → null)
- Ví dụ dưới đây sẽ refactor lại đoạn code tính thể tích phía trên, có sử dụng constructor:
  * Thay vì phải khởi tạo từng đối tượng tại class main, chúng ta có thể khởi tạo qua constructor
  * Khi khai báo 1 đối tượng Box, cần truyền chính xác các tham số theo thứ tự được định nghĩa trong hàm constructor:
    ```java
    // Now, volume() returns the volume of a box.
    class Box {
        double width;
        double height;
        double depth;

        // Constructor to initialize the dimensions
        Box(double w, double h, double d) {
            width = w;
            height = h;
            depth = d;
        }

        // Compute and return volume
        double volume() {
            return width * height * depth;
        }
    }

    class BoxDemo {
        public static void main(String args[]) {
        // Create a Box object using the constructor
        Box mybox1 = new Box(10, 20, 15);

        // Get volume of the box
        double vol = mybox1.volume();
        System.out.println("Volume is " + vol);
        }
    }  
    ```
    
## Từ khoá "This"
- Trong Java, nếu một biến cục bộ (local variable) hoặc tham số của phương thức có cùng tên với một biến instance của lớp, thì biến cục bộ sẽ “che khuất” biến instance.
- Do đó, để phân biệt biến cục bộ và biến instance cùng tên, Java cung cấp từ khoá “this” 
- Quy trở lại với ví dụ về class Box, dưới đây là đoạn code mô tả việc sử dụng this để phân biệt biến instance và biến cục bộ trong hàm constructor: 
  * Ở đây, this.width chỉ đến biến instance, còn width chỉ đến tham số của constructor.
    ```java
    class Box {
        double width, height, depth;
    
        // Constructor sử dụng this để tham chiếu đến biến instance
        Box(double width, double height, double depth) {
            this.width = width;   // this.width là biến instance
            this.height = height; // this.height là biến instance
            this.depth = depth;   // this.depth là biến instance
        }
    }
    ```

## Garbage collection
- Garbage Collection (GC) là cơ chế tự động của Java để thu hồi bộ nhớ của các đối tượng không còn được sử dụng ⇒ Lập trình viên không cần quản lý bộ nhớ thủ công trong Java, vì JVM sẽ tự động xử lý thông qua Garbage Collection.
- Cách hoạt động: 
  * Khi một đối tượng không còn tham chiếu nào trỏ tới, nó sẽ được coi là không cần thiết ⇒ Bộ nhớ của đối tượng đó sẽ được thu hồi để sử dụng lại.
  * Việc thu hồi xảy ra một cách tự động và không có thời gian cụ thể
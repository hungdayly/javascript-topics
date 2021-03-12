# Phương thức của kiểu cơ sở

## Giá trị cơ sở và đối tượng

JavaScript cho phép chúng ta làm việc với các giá trị cơ sở (chuỗi, số, ...) như thể chúng là các đối tượng.

Chúng ta hãy xem xét sự khác biệt chính giữa giá trị cơ sở và đối tượng.

Các giá trị cơ sở:

- Là một giá trị có kiểu cơ sở.
- Có 7 loại giá trị cơ sở: `string`, `number`, `bigint`, `boolean`, `symbol`, `null` và `undefined`.

Một đối tượng:

- Có khả năng lưu trữ nhiều giá trị dưới dạng thuộc tính.
- Có thể được tạo ra với `{}`, ví dụ `{name: "John", age: 30}`. Có nhiều loại đối tượng khác nhau trong JavaScript, ví dụ: các hàm là các đối tượng.

Một trong những điều tốt nhất về các đối tượng là chúng ta có thể lưu trữ một hàm như một trong các thuộc tính của nó.

```javascript
let john = {
    name: "John",
    sayHi: function() {
        console.log("Hi buddy!");
    }
};

john.sayHi(); // Hi buddy!
```

Nhiều đối tượng dựng sẵn đã tồn tại, chẳng hạn như những đối tượng hoạt động với ngày tháng, với lỗi, với các phần tử HTML,... Chúng có các thuộc tính và phương thức khác nhau.

Nhưng sự mạnh mẽ của đối tượng đi kèm với cái giá phải trả! Các đối tượng "nặng nề" hơn so với giá trị cơ sở. Chúng yêu cầu nhiều tài nguyên và năng lực xử lý của máy tính hơn.

## Một giá trị cơ sở được xem như một đối tượng

Bất cứ khi nào ta sử dụng một giá trị cơ sở như một đối tượng, một "đối tượng bao" tạm thời được tạo chứa giá trị cơ sở này. Lúc này, chúng ta đang làm việc với đối tượng bao này, sau khi công việc kết thúc, đối tượng bao bị hủy.

Ví dụ:

```javascript
let str = "Hello";

console.log(str.toUpperCase()); // HELLO
```

Đây là những gì thực sự xảy ra trong `str.toUpperCase()`:

1. Chuỗi `str` là một giá trị cơ sở. Vì vậy trong thời điểm truy cập phương thức `.toUpperCase()` của nó, một đối tượng bao đặc biệt được tạo ra chứa giá trị của chuỗi này và cung cấp phương thức `.toUpperCase()`.
2. Phương thức `.toUpperCase()` của đối tượng bao được chạy và trả về chuỗi mới, được hiển thị bằng `console.log`.
3. Đối tượng bao bị hủy, chỉ còn lại giá trị cơ sở `str`.

Một ví dụ nữa là khi gọi phương thức `.toFixed()` trên một số:

```javascript
let n = 1.23456;

console.log(n.toFixed(2)); // 1.23
```

## null/undefiend không được xem là đối tượng

Có hai giá trị cơ sở đặc biệt là `null` và `undefined` không có đối tượng bao, tức chúng không thể được sử dụng như một đối tượng.

Cố gắng truy cập thuộc tính của `null` hoặc `undefined` sẽ gây ra lỗi:

```javascript
console.log(null.test); // error
```

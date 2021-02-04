# Biến

Hầu hết thời gian, một ứng dụng JavaScript cần làm việc với thông tin. Đây là hai ví dụ:

1. Một cửa hàng trực tuyến - thông tin có thể bao gồm hàng hóa đang được bán và một giỏ hàng.
2. Một ứng dụng trò chuyện - thông tin có thể bao gồm người dùng, tin nhắn, v.v.

Các biến được sử dụng để lưu trữ thông tin này.

## Một biến số

Một biến là một "bộ nhớ được đặt tên" cho dữ liệu. Chúng ta có thể sử dụng các biến để lưu trữ các món quà, khách truy cập và các dữ liệu khác.

Để tạo một biến trong JavaScript, hãy sử dụng từ khóa `let`.

Câu lệnh dưới đây tạo (còn gọi là *khai báo*) một biến có tên `"message"`:

```javascript
let message;
```

Bây giờ chúng ta có thể đưa một số dữ liệu vào biến bằng cách sử dụng toán tử gán `=`:

```javascript
let message;

message = 'Hello'; // lưu một chuỗi
```

Chuỗi giờ được lưu vào vùng nhớ liên kết với biến. Chúng ta có thể truy cập nó bằng cách sử dụng tên biến:

```javascript
let message;
message = 'Hello!';

alert(message);  // hiển thị nội dung của biến
```

Chúng ta có thể khai báo nhiều biến trên một dòng:

```javascript
let user = 'John', age = 25, message = 'Hello';
```

Nhưng bạn nên khai báo mỗi biến trên một dòng:

```javascript
let user = 'John';
let age = 25;
let message = 'Hello';
```

## Một hình dung về biến

Chúng ta có thể dễ dàng nằm bắt được khái niệm "biến" nếu chúng ta hình dung nó như một "hộp" chứa dữ liệu, với một nhãn dán có tên riêng trên đó.

Ví dụ, biến `message` có thể được hình dung như một hộp được gán nhãn `"message"` với giá trị `"Hello!"` trong đó:

![hộp có tên message](variable.svg)

Chúng ta có thể đặt bất kỳ giá trị nào vào hộp.

Chúng ta cũng có thể thay đổi giá trị của hộp bất cứ lúc nào ta muốn:

```javascript
let message;

message = 'Hello!';

message = 'World!'; // giá trị đã thay đổi

alert(message);
```

Khi giá tị được thay đổi, dữ liệu cũ sẽ bị xóa khỏi biến:

![thay đổi giá trị của hộp](variable-change.svg)

Chúng ta có thể khai báo biến và sao chép dữ liệu từ biến này sang biến khác:

```javascript
let hello = 'Hello world!';

let message;

// sao chép 'Hello world' từ hello sang message
message = hello;

// giờ hai biến cùng lưu một dữ liệu giống nhau
alert(hello);  // Hello world!
alert(message);  // Hello world!
```

> Một biến chỉ nên được khai báo một lần.
>
> Một khai báo lặp lại của cùng một biến là một lỗi:
> ```javascript
> let message = "This";
>
> // lặp lại 'let' dẫn đến một lỗi
> let message = "That";  // SyntaxError: 'message' has already been declared
>```
> Vì vậy, chúng ta nên khai báo một biến một lần và sau đó tham chiếu đến nó mà không cần `let`

## Đặt tên biến

Có hai hạn chế về tên biến trong JavaScript:

1. Tên chỉ được chứa các chữ cái, chữ số hoặc các ký hiệu `$` và `_`.
2. Kí tự đầu tiên không được là một chữ số.

Ví dụ về tên hợp lệ:

```javascript
let userName;
let test123;
```

Khi tên chứa nhiều từ thì cú pháp lạc đà thường được dùng để viết tên. Đó là: ký tự đầu của mỗi từ, bắt đầu từ từ thứ hai trở đi được viết hoa: `myVeryLongName`.

Điều thú vị là - ký hiệu đô-la `$` và dấu gạch dưới `_` cũng có thể được dùng trong tên. Chúng là những ký hiệu thông thường, giống như chữ cái, chữ số, không có bất kỳ ý nghĩa đặc biệt nào.

Những tên này hợp lệ:

```javascript
let $ = 1;
let _ = 2;

alert($ + _);  // 3
```

Ví dụ về tên biến không hợp lệ:

```javascript
let 1a;  // không thể bắt đầu bằng chữ số

let my-name;  // không thể chứa kí tự gạch ngang '-'
```

> Các biến trong JavaScript phân biệt chữ hoa, chữ thường. Hai biến `apple` và `AppLE` là hai biến khác nhau.

## Từ khóa

Có một danh sách các từ danh riêng cho JavaScript, được gọi là các *từ khóa*. Từ khóa không được dùng làm tên biến vì chúng đã được chính JavaScript sử dụng.

Ví dụ: `let`, `class`, `return` và `function` là các từ khóa.

Đoạn mã dưới đây mắc phải lỗi cú pháp vì sử dụng từ khóa làm tên biến:

```javascript
let let = 5;  // Unexpected strict mode reserved word
let return = 5;  // Unexpected strict mode reserved word biến
```

## Hằng số

Để khai báo một hằng số, tức một biến không thay đổi giá trị, hãy sử dụng từ khóa `const` thay vì từ khóa `let`.

```javascript
const MY_BIRTH_DAY = '03.08.1986';

MY_BIRTH_DAY = '01.01.2021';  // TypeError: Assignment to constant variable.
```

Các hằng số thường được viết hoa, các từ phân cách nhau bằng dấu gạch dưới `_`:

```javascript
const COLOR_RED = "#F00";
const COLOR_GREEN = "#0F0";
const COLOR_BLUE = "#00F";
const COLOR_ORANGE = "#FF7F00";
```
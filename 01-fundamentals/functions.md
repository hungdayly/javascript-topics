# Hàm

Rất thường xuyên, chúng ta cần thực hiện một hành động nào đó ở nhiều nơi trong trong chương trình.

Ví dụ, chúng ta cần hiển thị một thông báo đẹp mắt khi khách đăng nhập, đăng xuất, hoặc khi ở một nơi khác.

Hàm là những "khối chức năng" chính của chương trình. Chúng cho phép một chức năng được thực hiện nhiều lần mà không cần viết lại mã ở khắp nơi.

Chúng ta đã thấy ví dụ về các hàm có sẵn (hàm tích hợp) của JavaScript như `alert(message)`, `console.log(message)`, `prompt(message, default)`... Nhưng chúng ta cũng có thể tạo ra các hàm của riêng mình.

## Khai báo hàm

Để tạo một hàm, chúng ta sử dụng *khai báo hàm* (còn gọi là *định nghĩa hàm*).

Nó trông như thế này:

```javascript
function showMessage() {
    console.log('Hello everyone!');
}
```

Từ khóa `function` luôn phải đặt đầu tiên, sau đó là tên của hàm, sau đó là một danh sách các *tham số* đặt giữa `(...)`, nếu không có tham số vẫn phải viết `()` như ví dụ trên. Cuối cùng là thân của hàm nằm giữa `{...}`. Cú pháp chung như sau:

```javascript
function name(parameters) {
    ...body...
}
```

Để chạy hàm, chúng ta gọi nó:

```javascript
function showMessage() {
    console.log('Hello everyone!');
}

showMessage(); // Hello everyone!
showMessage(); // Hello everyone!
```

Gọi `showMessage()` sẽ thực thi thân của nó. Ở đây chúng ta thực thi thân của hàm hai lần qua hai lần gọi `showMessage()`.

Ví dụ này thể hiện rõ mục đích chính của các hàm: "tránh trùng lặp mã".

Nếu chúng ta cần thay đổi thông báo cần hiển thị, thì chỉ cần sửa đổi ở một nơi duy nhất: "trong khai báo hàm".

## Biến cục bộ

Một biến được khai báo bên trong một hàm chỉ hiển thị bên trong hàm đó. Biến như vậy gọi là biến cục bộ.

Ví dụ:

```javascript
function showMessage() {
    let message = "Hello, I'm JavaScript!"; // biến cục bộ

    console.log(message);
}

showMessage(); // Hello, I'm JavaScript!

console.log(message); // <-- Error! The variable is local to the function
```

## Các biến bên ngoài

Một hàm có thể truy cập các biến bên ngoài nó, ví dụ:

```javascript
let userName = 'John';

function showMessage() {
    let message = 'Hello, ' + userName;
    console.log(message);
}

showMessage(); // Hello, John
```

Thậm chí hàm có thể sửa đổi biến bên ngoài:

```javascript
let userName = 'John';

function showMessage() {
    userName = "Bob"; // (1) thay đổi biến ngoài

    let message = 'Hello, ' + userName;

    console.log(message);
}

console.log(userName); // John (trước khi gọi hàm)

showMessage(); // Hello, Bob

console.log(userName); // Bob (sau khi gọi hàm)
```

Nếu hàm tạo ra biến một biến cục bộ trùng tên với biến bên ngoài, biến cục bộ sẽ được ưu tiên sử dụng:

```javascript
let userName = 'John';

function showMessage() {
    let userName = "Bob"; // khai báo biến cục bộ trùng tên biến ngoài

    let message = 'Hello, ' + userName;
    
    console.log(message);
}

showMessage(); // Hello, Bob

console.log(userName); // John (không bị thay đổi bởi hàm)
```

> **Biến toàn cục**
> Biến được khai báo bên ngoài mọi hàm, chẳng hạn như `userName` ở ví dụ trên, được gọi là *biến toàn cục*.
> 
> Các biến toàn cục có thể được truy cập và bị sửa đổi bất bất cứ hàm nào trong chương trình.
>
> Một lời khuyên là giảm tối đa việc sử dụng các biến toàn cục. Chúng chỉ nên dùng để lưu dữ liệu dùng chung cho toàn dự án.

## Tham số

Một hàm nhận dữ liệu từ bên ngoài thông qua các *tham số* (đôi khi hay bị gọi là *đối số*).

Trong ví dụ dưới đây, hàm có hai tham số là `from` và `text`.

```javascript
function showMessage(from, text) { // đối số: from, text
    console.log(from + ': ' + text);
}

showMessage('Ann', 'Hello!'); // Ann: Hello! (*)
showMessage('Ann', "What's up?"); // Ann: What's up? (**)
```

Khi hàm được gọi trong `(*)` và `(**)`, các giá trị truyền vào được truyền cho các tham số `from` và `text`. Sau đó, hàm sử dụng chúng để in ra các thông báo.

Đây là một ví dụ nữa, chúng ta có một biến `from` và chuyển nó vào hàm. Trong trường hợp này giá trị của `from` bên ngoài được sao chép cho tham số `from` bên trong hàm. Hàm chỉ thay đổi tham số `from` của nó, không thay đổi `from` bên ngoài:

```javascript
function showMessage(from, text) {
    from = '*' + from + '*'; // làm from trông đẹp hơn

    console.log(from + ': ' + text);
}

let from = "Ann";

showMessage(from, "Hello"); // *Ann*: Hello

console.log(from); // Ann
```

## Giá trị mặc định

Nếu một tham số không được truyền giá trị, giá trị của nó sẽ là `undefined`.

```javascript
function showMessage(from, text) {
    console.log(from + ': ' + text);
}

showMessage("Ann"); // Ann: undefined
```

Nếu muốn một giá trị mặc định khác `undefined` thì có thể chỉ định nó sau dấu `=`:

```javascript
function showMessage(from, text = "no text given") {
    console.log(from + ': ' + text);
}

showMessage("Ann"); // Ann: no text given
```

## Giá trị trả về

Một hàm có thể trả về giá trị cho người gọi nó.

Ví dụ đơn giản nhất là hàm trả về tổng của hai số:

```javascript
function sum(a, b) {
    return a + b;
}

let result = sum(1, 2);
console.log(result); // 3
```

Chỉ thị `return` có thể xuất hiện ở bất cứ đâu trong thân hàm. Khi thực thi, nó khiến hàm kết thúc và trả về một giá trị.

Có thể có nhiều lệnh `return` nhưng chỉ một trong số chúng được chạy. Ví dụ:

```javascript
function checkAge(age) {
    if (age >= 18) {
        return true;
    } else {
        return confirm('Do you have permission from your parents?');
    }
}

let age = prompt('How old are you?', 18);

if (checkAge(age)) {
    console.log('Access granted');
} else {
    console.log('Access denied');
}
```

Nếu dùng `return` không có giá trị trả về cụ thể, nó khiến hàm kết thúc ngay lập tức:

```javascript
function showMovie(age) {
    if (!checkAge(age)) {
        return;
    }

    console.log("Showing you the movie");
}
```

> **Hàm không có `return` hoặc chỉ có `return` mà không có giá trị trả về, sẽ trả về `undefined`.
> ```javascript
> function doNothing() { /* trống */ }
> console.log(doNothing()); // undefined
> ```
>
> ```javascript
> function doNothing() {
>   return;
> }
> console.log(doNothing()); // undefined
> ```
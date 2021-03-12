# Biểu thức hàm

Trong JavaScript, hàm là một giá trị đặc biệt (có thể gọi được).

Ta có thể xem các giá trị thông thường biểu diễn dữ liệu trong khi hàm biểu diễn một hành động.

Cú pháp mà ta thấy trước đây là *khai báo hàm*:

```javascript
function sayHi() {
    console.log("Hello");
}
```

Có một cú pháp khác để tạo hàm gọi là *biểu thức hàm*.

Nó trông như thế này:

```javascript
let sayHi = function() {
    console.log("Hello");
};
```

Ở đây hàm được tạo ra thông qua một biểu thức (*biểu thức hàm*) và được gán cho một biến như bao giá trị khác.

Dù được tạo theo cách nào, hàm về bản chất chỉ là một giá trị được lưu trữ trong biến `sayHi`.

Chúng ta có thể sao chép một hàm sang một biến khác:

```javascript
function sayHi() { // (1) tạo
    console.log("Hello");
}

let func = sayHi; // (2) sao chép

func(); // Hello
sayHi(); // Hello
```

Lưu ý rằng thay vì sử dụng khai báo hàm như ví dụ, ta có thể sử dụng biểu thức hàm:

```javascript
let sayHi = function() {
    console.log("Hello");
};

let func = sayHi;
// ...
```

> **Chú ý:**
>
> Khai báo hàm không có dấu chấm phảy ở cuối, nhưng biểu thức hàm thì có.

## Hàm callback

Là một giá trị, hàm có thể truyền vào một hàm khác làm tham số.

Chúng ta sẽ viết một hàm `ask(question, yes, no)` với ba tham số:

- `question`: nội dung câu hỏi
- `yes`: hàm chạy nếu người dùng trả lời là "Có"
- `no`: hàm chạy nếu người dùng trả lời là "Không"

```javascript
function ask(question, yes, no) {
    if (confirm(question)) yes()
    else no();
}

function showOk() {
    console.log("You agreed.");
}

function showCancel() {
    console.log("You canceled the execution.");
}

ask("Do you agree?", showOk, showCancel);
```

Các đối số `showOk` và `showCancel` của `ask` được gọi là các hàm callback (hàm gọi sau) hoặc ngắn gọn là _callback_.

Khi viết các callback ta nên sử dụng biểu thức hàm vì nó trông sẽ gọn gàng hơn.

```javascript
function ask(question, yes, no) {
    if (confirm(question)) yes()
    else no()
}

ask(
    "Do you agree?",
    function() { console.log("You agreed." ); },
    function() { console.log("You canceled the execution."); }
);
```

## Khác biệt giữa khai báo hàm và biểu thức hàm

### Khác biệt về cú pháp

```javascript
// Khai báo hàm
function sum(a, b) {
    return a + b;
}

// Biểu thức hàm
let sum = function(a, b) {
    return a + b;
};
```

Cần đặc biệt lưu ý về dấu chấm phảy.

### Khai biệt về thứ tự xuất hiện

Hàm tạo bởi khai báo hàm có thể gọi trước khi khai báo:

```javascript
sayHi("John"); // Hello, John

function sayHi(name) {
    console.log(`Hello, ${name}`);
}
```

Biểu thức hàm chỉ có thể được sử dụng sau khi đã tạo:

```javascript
sayHi("John"); // error!

let sayHi = function(name) {
    console.log(`Hello, ${name}`);
};

sayHi("John"); // Hello, John
```
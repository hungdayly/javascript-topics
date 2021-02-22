# Hàm mũi tên

Có một cú pháp rất đơn giản và ngắn gọn khác để tạo hàm, thường tốt hơn so với biểu thức hàm.

Nó được gọi là biểu thức "hàm mũi tên", bởi vì nó trông như thế này:

```javascript
let func = (arg1, arg2, ..., argN) => expression
```

Điều này tạo ra một hàm `func` có các đối số `arg1...argN`, sau đó chạy `expression` và trả về giá trị của biểu thức này.

Nói cách khác, đó là phiên bản ngắn hơn của:

```javascript
let func = function(arg1, arg2, ..., argN) {
    return expression
}
```

Hãy xem một ví dụ cụ thể:

```javascript
let sum = (a, b) => a + b;

/* hàm mũi tên này là dạng ngắn hơn của

let sum = function(a, b) {
    return a + b;
}

*/

console.log(sum(1, 2)); // 3
```

Nếu chúng ta chỉ có một đối số, thì dấu ngoặc quanh các tham số có thể bỏ qua:

```javascript
let double = n => n * 2;

console.log(double(3)); // 6
```

Nhưng không có đối số thì dấu ngoặc đơn vẫn phải có, mặc dù trống:

```javascript
let sayHi = () => console.log("Hello!");

sayHi(); // Hello!
```

Các hàm mũi tên có thể được sử dụng giống như biểu thức hàm, chẳng hạn làm giá trị trả về của một biểu thức điều kiện:

```javascript
let age = prompt("What is your age?", 18);

let welcome = (age < 18) ?
    () => console.log('Hello!) :
    () => console.log("Greeting!");
```

## Hàm mũi tên có nhiều dòng

Khi thân hàm mũi tên có nhiều dòng và cần sử dụng `return`, đặt nó trong `{...}` sau mũi tên như thế này:

```javascript
let sum = (a, b) => {
    let result = a + b;
    return result;
};

console.log(sum(1, 2)); // 3
```
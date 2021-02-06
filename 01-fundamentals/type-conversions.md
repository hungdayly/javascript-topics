# Chuyển đổi kiểu

Hầu hết thời gian, các toán tử và hàm tự động chuyển đổi các giá trị được cấp cho chúng thành kiểu phù hợp.

Ví dụ: `console.log` tự động chuyển đổi bất kỳ giá trị nào thành một chuỗi để hiển thị nó. Các toán tử số học chuyển đổi giá trị thành số.

Cũng có những trường hợp khi chúng ta cần chuyển đổi rõ ràng một giá trị thành kiểu mong đợi.

## Chuyển đổi chuỗi

Chuyển đổi chuỗi xảy ra khi chúng ta cần dạng chuỗi của một giá trị.

Ví dụ, `console.log(value)`, giá trị `value` được chuyển thành chuỗi và được hiển thị.

Chúng ta cũng có thể gọi `String(value)` để chuyển đổi `value` thành một chuỗi:

```javascript
let value = true;
console.log(typeof value);  // boolean

value = String(value);  // giờ value là chuỗi "true"
console.log(typeof value);  // string
```

Kết quả chuyển đổi chuỗi rất trực quan. Giá trị `false` trở thành chuỗi `"false"`, giá trị `null` trở thành `"null"`,v.v.

## Chuyển đổi số

Tự động chuyển đổi số xảy ra trong các hàm và toán tử số học.

Ví dụ, khi phép chia `/` được áp dụng cho các giá trị không phải số:

```javascript
console.log( "6" / "2" );  // 3, các chuỗi được chuyển thành số
```

Chúng ta có thể sử dụng `Number(value)` để chuyển đổi một cách rõ ràng `value` thành một số:

```javascript
let str = "123";
console.log(typeof str);  // string

let num = Number(str); // trở thành số 123

console.log(typeof num);  // number
```

Chuyển đổi rõ ràng thường được yêu cầu khi chúng ta đọc một giá trị số từ bàn phím do người dùng nhập vào.

Nếu chuỗi không phải là một số hợp lệ, kết quả của chuyển đổi là `NaN`. Ví dụ:

```javascript
let age = Number("an arbitrary string instead of a number");

console.log(age);  // NaN, chuyển đổi thất bại
```

Quy tắc chuyển đổi số:

| Giá trị | Trở thành... |
|---------|--------------|
| `undefined` | `NaN` |
| `null` | `0` |
| `true` và `false` | `1` và `0` |
| `string` | Khoảng trắng hai đầu bị xóa. Nếu chuỗi còn lại trống, kết quả là `0`. Nếu không, số được lấy ra từ chuỗi. Nếu chuỗi còn lại không phải số hợp lệ, kết quả là `NaN` |

Ví dụ:

```javascript
console.log( Number("   123   ") );  // 123
console.log( Number("123z") );  // NaN (lỗi khi đọc đến "z")
console.log( Number(true) );  // 1
console.log( Number(false) );  // 0
```

Xin lưu ý rằng `null` và `undefined` cư xử khác ở đây: `null` trở thành `0` trong khi `undefined` trở thành `NaN`.

Hầu hết các toán tử toán học cũng thực hiện chuyển đổi như vậy, chúng ta sẽ thấy điều đó trong chương tiếp theo.

## Chuyển đổi lôgic

Chuyển đổi lôgic là chuyển đổi đơn giản nhất.

Nó xảy ra trong các toán tử lôgic, nhưng cũng có thể được thực hiện một cách rõ ràng bằng cách gọi `Boolean(value)`.

Quy tắc chuyển đổi:

- Các giá trị `0`, `null`, `undefined`, `NaN` trở thành `false`.
- Các giá trị khác trở thành `true`.

Ví dụ:

```javascript
console.log( Boolean(1) );  // true
console.log( Boolean(0) );  // false

console.log( Boolean("hello") );  // true
console.log( Boolean("") );  // false
```
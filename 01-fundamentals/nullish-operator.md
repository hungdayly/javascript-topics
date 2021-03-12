# Toán tử `??`


Toán tử này được gọi là toán tử "nullish" và được viết dưới dạng hai dấu chấm hỏi `??`.

Trước khi đi vào cách hoạt động, ta định nghĩa như sau: _Một biểu thức được gọi là "xác định" nếu giá trị của nó không phải là `null` hoặc `undefined`._

Kết quả của `a ?? b` là:

- `a` nếu `a` xác định.
- `b` nếu `a` không xác định.

Nói cách khác, `??` trả về toán hạng đầu tiên nếu nó xác định (không phải `null/undefined`). Nếu không trả về toán hạng thứ hai.

Trường hợp dùng phổ biến của `??` là cung cấp giá trị mặc định cho một biến có thể không được xác định.

Ví dụ: ở đây chúng ta hiển thị `user` nếu nó được định nghĩa, nếu không hiển thị `"Anonymous"`:

```javascript
let user;

console.log( user ?? "Anonymous" );  // Anonymous (user không được xác định)
```

Đây là ví dụ khi `user` được gán một tên:

```javascript
let user = "John";

console.log( user ?? "Anonymous" );  // John (user được xác định)
```

Có thể sử dụng nhiều `??` để chọn ra giá trị đầu tiên không phải `null/undefined` từ một danh sách các biến/biểu thức:

```javascript
let firstName = null;
let lastName = null;
let nickName = "Supercoder";

// hiển thị giá trị xác định đầu tiên
console.log(firstName ?? lastName ?? nickName ?? "Anonymous" ); // Supercoder
```

## So sánh với `||`

Toán tử `||` có thể được dùng theo cách tương tự `??`.

Ví dụ, trong đoạn mã trên, chúng ta có thể thay thế `??` bằng `||` mà vẫn nhận được kết quả tương tự:

```javascript
let firstName = null;
let lastName = null;
let nickName = "Supercoder";

// hiển thị giá trị trung thực đầu tiên:
console.log(firstName || lastName || nickName || "Anonymous" ); // Supercoder
```

Trong lịch sử, `||` có ngay từ ban đầu. Vì vậy các nhà phát triển đã sử dụng nó cho những mục đích như vậy trong một thời gian dài.

Mặt khác toán tử `??` chỉ mới được thêm vào JavaScript gần đây. Lý do là mọi người không hài lòng với `||` lắm.

Sự khác biệt quan trọng giữa chúng là:

- `||` trả về giá trị trung thực đầu tiên.
- `??` trả về giá trị được xác định đầu tiên.

Nói cách khác `||` không phân biệt giữa `false`, `0`, một chuỗi rỗng `""` và `null/undefined`. Tất cả chúng đều giống nhau - giá trị giả dối. Nếu bất kỳ giá trị nào trong số này là toán hạng đầu tiên của `||`, thì kết quả chúng ta sẽ nhận được toán hạng thứ hai.

Tuy nhiên, trong thực tế, chúng ta có thể chỉ muốn sử dụng giá trị mặc định khi biến là `null/undefined`. Đó là khi, giá trị thực sự không xác định/không được đặt.

Ví dụ, hãy xem xét đoạn mã sau:

```javascript
let height = 0;

console.log(height || 100);  // 100
console.log(height ?? 100);  // 0
```

Trong thực tế, chiều cao bằng `0` là một giá trị hợp lệ, không nên được thay thế bằng giá trị mặc định. Vì vậy, `??` làm việc đúng đắn hơn.

## Quyền ưu tiên

Mức độ ưu tiên của toán tử `??` cũng giống như `||`, chỉ thấp hơn một chút. Nó bằng `5` trong khi `||` là `6`.

Điều đó có nghĩa rằng, giống như `||`, toán tử `??` được thực hiện trước `=` và `?` nhưng sau các toán tử như `+`, `*`.

Vì vậy, nếu chúng ta muốn sử dụng `??` trong một biểu thức cùng với các toán tử khác, hãy xem xét thêm dấu ngoặc đơn:

```javascript
let height = null;
let width = null;

// quan trọng: sử dụng dấu ngoặc đơn
let area = (height ?? 100) * (width ?? 50);

console.log(area);  // 5000
```

## Sử dụng `??` với `&&` hoặc `||`

Vì lý do an toàn, JavaScript cấm sử dụng `??` cùng với `&&` và `||`, trừ khi mức độ ưu tiên được chỉ định rõ ràng bằng dấu ngoặc đơn.

Đoạn mã dưới đây gây ra lỗi cú pháp:

```javascript
let x = 1 && 2 ?? 3; // syntax error
```

Sử dụng dấu ngoặc đơn rõ ràng để giải quyết lỗi này:

```javascript
let x = (1 && 2) ?? 3; // làm việc

console.log(x);  // 2
```

## Tóm tắt

1. Toán tử nullish `??` cung cấp một cách ngắn gọn để chọn giá trị "xác định" đầu tiên từ danh sách.

    Nó được sử dụng để gán các giá trị mặc định cho các biến thay cho `||`:

    ```javascript
    // đặt height=100, nếu height null hoặc undefined
    height = height ?? 100;
    ```

2. Toán tử `??` có mức ưu tiên rất thấp, chỉ cao hơn một chút so với `?` và `=`, vì vậy hãy xem xét thêm dấu ngoặc đơn khi sử dụng nó trong một biểu thức.
3. Nó bị cấm sử dụng cùng với `||` và `&&` mà không có dấu ngoặc đơn rõ ràng.
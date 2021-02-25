# Truy cập thuộc tính một cách an toàn

## Vấn đề "không tồn tại" của một thuộc tính

Nếu bạn mới bắt đầu đọc hướng dẫn và học JavaScript, có thể vấn đề này vẫn chưa chạm đến bạn, nhưng nó khá phổ biến.

Ví dụ: giả sử chúng ta có đối tượng `user` chứa thông tin về người dùng của chúng ta.

Hầu hết người dùng của chúng ta có địa chỉ được lưu trong `user.address`, địa chỉ đường lưu trong `user.address.street`, nhưng không phải đối tượng nào cũng cung cấp thuộc tính này.

Trong trường hợp như vậy, nếu chúng ta cố gắng lấy `user.address.street` và người dùng vô tình không có `address`, chúng ta sẽ gặp lỗi:

```javascript
let user = {}; // một đối tượng user không có thuộc tính "address"

console.log(user.address.street); // Error!
```

Đó là kết quả bình thường. JavaScript hoạt động như vậy. Khi truy cập một thuộc tính không tồn tại, giá trị thu được là `undefined`, như vậy `user.address` là `undefined`. Kết quả là `user.address.street` tương đương `undefined.street` dẫn tới lỗi vì `undefined` không phải là đối tượng và không có thuộc tính `street`!

Giải pháp thông thường là sử dụng `if` hoặc toán tử điều kiện `?` để kiểm tra trước khi truy cập thuộc tính:

```javascript
let user = {};

console.log(user.address ? user.address.street: undefined);
```

Cú pháp này bị rườm ra vì `user.address` bị lặp lại. Tình trạng sẽ tệ hơn khi truy cập các thuộc tính ở mức sâu hơn:

```javascript
let user = {};

console.log(user.address ? user.address.street ? user.address.street.name : undefined : undefined);
```

## Truy cập thuộc tính an toàn bằng "?."

`?.` dừng chạy nếu giá trị trước nó là `undefined` hoặc `null` và trả về `undefined`.

Nói cách khác: `value?.prop`:

- hoạt động như `value.prop` nếu `value` xác định (không phải `null` hoặc `undefined`),
- trả về `undefined` nếu `value` không xác định.

Đây là cách an toàn để truy cập `user.address.street`:

```javascript
let user = {};

console.log(user?.address?.street); // undefined (không có lỗi)
```

Mã ngắn gọn và rõ ràng, không có sự trùng lặp nào cả.

Chú ý rằng `?.` dừng chạy nếu trước nó là `undefined` hoặc `null`, nên câu lệnh `console.log` thứ hai không gây ra lỗi dù có truy cập thêm các thuộc tính ở mức sâu hơn.

```javascript
let user = null;

console.log(user?.address); // undefined
console.log(user?.address.street); // undefined
```

## Các biến thể

**`?.()`** được dùng để gọi một hàm có thể không tồn tại.

Trong đoạn mã dưới đây, một số người dùng của chúng ta có phương thức `admin`, một số người dùng khác thì không:

```javascript
let userAdmin = {
    admin() {
        console.log("I am admin");
    }
};

let userGuess = {};

userAdmin.admin?.(); // I am admin
userGuess.admin?.(); // không có gì
```

Ở đây trong cả hai dòng, đầu tiên chúng ta sử dụng dấu chấm (`userAdmin.admin` và `userGuess.admin`) để lấy thuộc tính `admin`, vì chúng ta giả định rằng `userAdmin` và `userGuess` tồn tại và có thể đọc an toàn từ nó.

Sau đó `?.()` kiểm tra phần bên trái: nếu hàm `admin` tồn tại, thì nó sẽ chạy (đối với `userAdmin`). Nếu không (đối với `userGuess`) việc đánh giá dừng lại mà không có lỗi.

**`?.[]`** được dùng để truy cập thuộc tính tương tự như cách truy cập thuộc tính bằng `[]`.

```javascript
let key = "firstName";

let user1 = {
    firstName: "John"
};

let user2 = null;

console.log(user1?.[key]); // John
console.log(user2?.[key]); // undefined
```

Ngoài ra chúng ta có thể sử dụng `?.` với `delete`:

```javascript
delete user?.name; // delete user.name nếu nó tồn tại
```

> **Không thể sử dụng `?.` để ghi một thuộc tính**
> ```javascript
> let user = null;
> user?.name = "John"; // lỗi, không làm việc
> ```

## Tóm tắt

`?` có ba dạng:

1. `obj?.prop` - trả về `obj.prop` nếu nó tồn tại, trả về `undefined` nếu không.
2. `obj?.[prop]` - trả về `obj[prop]` nếu nó tồn tại, trả về `undefiend` nếu không.
3. `obj.method?.()` - gọi phương `obj.method()` nếu `obj.method()` tồn tại, nếu không trả về `undefined`.
4. 
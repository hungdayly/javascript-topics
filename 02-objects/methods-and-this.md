# Phương thức và "this"

Các đối tượng thường được tạo ra để đại diện cho các thực thể của thế giới thực, như người dùng, đơn đặt hàng,...

```javascript
let user = {
    name: "John",
    age: 30
};
```

Và, trong thế giới thực, người dùng có thể *hành động*: chọn thừ gì đó từ giỏ hảng, đăng nhập, đăng xuất...

Các hành động được biểu diễn trong JavaScript bằng các thuộc tính có giá trị hàm.

## Ví dụ về phương thức

Để bắt đầu, hãy dạy `user` cách nói lời chào:

```javascript
let user = {
    name: "John",
    age: 30
};

user.sayHi = function() {
    console.log("Hello!");
};

user.sayHi(); // Hello!
```

Ở đây chúng ta sử dụng biểu thức hàm để tạo một hàm và gán nó cho thuộc tính `user.sayHi` của đối tượng.

Sau đó, chúng ta có thể gọi nó bằng `user.sayHi()`. Người dùng bây giờ đã có thể nói!

Một hàm là một thuộc tính của một đối tượng được gọi là *phương thức* của nó.

Vì vậy, ở đây chúng ta có một phương thức `sayHi` của đối tượng `user`.

Tất nhiên, chúng ta có thể sử dụng một hàm có sẵn như một phương thức, ví dụ:

```javascript
let user = {
    // ...
};

// trước tiên, khai báo
function sayHi() {
    console.log("Hello!");
};

// sau đó thêm như phương thức
user.sayHi = sayHi;

user.sayHi(); // Hello!
```

### Cú pháp viết tắt

Có một cú pháp ngắn hơn cho các phương thức trong một đối tượng:

```javascript
// các đối tượng này giống nhau

user = {
    sayHi: function() {
        console.log("Hello");
    }
};

// cách viết tắt này trông tốt hơn
user = {
    sayHi() {
        console.log("Hello");
    }
};
```

## Từ khóa "this"

Thông thường, một phương thức cần truy cập thông tin được lưu trữ trong đối tượng để thực hiện công việc của nó.

Ví dụ, mã bên trong `user.sayHi()` có thể cần tên của `user`.

**Để truy cập đối tượng, một phương thức có thể sử dụng từ khóa `this`.**

Giá trị của `this` là "đối tượng trước dấu chấm" - đối tượng được sử dụng để gọi phương thức.

Ví dụ:

```javascript
let user = {
    name: "John",
    age: 30,

    sayHi() {
        console.log(this.name);
    }
};

user.sayHi(); // John
```

### "this" không bị ràng buộc

Trong JavaScript, từ khóa `this` hoạt động không giống như hầu hết các ngôn ngữ lập trình khác. Nó có thể được sử dụng trong bất kỳ hàm nào, ngay cả khi nó không phải là phương thức của một đối tượng.

Không có lỗi cú pháp trong ví dụ sau:

```javascript
function sayHi() {
    console.log(this.name);
}
```

Giá trị của `this` được xác định trong thời gian chạy, tùy thuộc vào ngữ cảnh.

Ví dụ: ở đây, cùng một hàm được gán cho hai đối tượng khác nhau và có "this" khác nhau trong các lệnh gọi:

```javascript
let user = { name: "John" };
let admin = { name: "Admin" };

function sayHi() {
    console.log(this.name);
}

// sử dụng cùng một hàm trong hai đối tượng
user.f = sayHi;
admin.f = sayHi;

user.f(); // John (this == user)
admin.f(); // Admin (this == admin)
```

Quy tắc ở đây rất đơn giản: nếu `obj.f()` được gọi, thì `this` chính là `obj`.

Khi hàm không được gọi từ một đối tượng, có hai khả năng sau:

- Trong chế độ nghiêm ngặt (sử dụng `"use strict"`) thì `this` là `undefined`.
- Trong chế độ không nghiệm ngặt thì `this` là đối tượng toàn cục (`window` trong trình duyệt).

### Hàm mũi tên không có "this"

Các hàm mũi tên rất đặc biệt: chúng không có `this` riêng. Nếu chúng ta sử dụng `this` trong hàm mũi tên, nó được lấy từ hàm bên ngoài gần nhất.

Ví dụ, ở đây `arrow()` sử dụng phương thức `this` bên ngoài `user.sayHi()`:

```javascript
let user = {
    firstName: "Ilya",
    sayHi() {
        let arrow = () => console.log(this.firstName);
        arrow();
    }
};

user.sayHi(); // Ilya
```

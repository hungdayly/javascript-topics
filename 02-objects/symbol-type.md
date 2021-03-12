# Kiểu symbol

Theo đặc tả JavaScript, các khóa của một thuộc tính của một đối tượng chỉ có thể là chuỗi hoặc một giá trị kiểu symbol.

Cho đến lúc này, chúng ta mới chỉ sử dụng chuỗi làm khóa của thuộc tính. Bây giờ chúng ta hãy xem những lợi ích khi sử dụng kiểu symbol làm khóa của một thuộc tính.

## Symbol

Một symbol đại diện cho một định danh duy nhất.

Một symbol được tạo bằng cách sử dụng `Symbol()`:

```javascript
// id là một symbol mới
let id = Symbol();
```

Có thể đặt tên (mô tả) cho một symbol bằng cách truyền đối số (là một chuỗi) vào `Symbol()`:

```javascript
// id là một symbol có tên( mô tả) là "id"
let id = Symbol("id");
```

Các biểu tượng được bảo đảm là duy nhất. Ngay cả khi chúng ta tạo ra nhiều symbol có cùng tên, chúng vẫn là các symbol khác nhau. Tên chỉ là nhãn của symbol, không liên quan đến giá trị của nó.

Ví dụ: đây là hai symbol có cùng mô tả - chúng không bằng nhau:

```javascript
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 == id2): // false
```

## Các symbol toàn cục

Các symbol toàn cục được đặc trưng bởi tên của nó, hai symbol cùng tên sẽ bằng nhau.

Để đọc (tạo nếu không có) một symbol toàn cục, sử dụng `Symbol.for(key)`, trong đó `key` là tên của symbol.

Lệnh này sẽ trả về symbol toàn cục có tên là `key` nếu tồn tại, nếu không tạo ra một symbol toàn cục mới.

Ví dụ:

```javascript
// tạo symbol toàn cục có tên "id"
let id = Symbol.for("id");

// đọc symbol toàn cục vừa tạo
let idAgain = Symbo.for("id");

// hai symbol bằng nhau
console.log(id === idAgain); // true
```

### Lấy tên của một symbol toàn cục

Ngược với `Symbol.for(key)` trả về một symbol toàn cục có tên là `key`, lệnh `Symbol.keyFor(sym)` trả về tên của symbol toàn cục `sym`.

Ví dụ:

```javascript
// lấy/tạo symbol theo tên
let sym = Symbol.for("name");
let sym2 = Symbol.for("id");

// lấy tên theo symbol
console.log(Symbol.keyFor(sym));  // name
console.log(Symbol.keyFor(sym2)); // id
```

## Các symbol hệ thống

Có rất nhiều symbol mà chính JavaScript sử dụng, chúng được gọi là các symbol hệ thống. Chúng ta cũng có thể sử dụng các symbol hệ thống để tinh chỉnh một đối tượng.

Đây là một số symbol hệ thống:

- `Symbol.hasInstance`
- `Symbol.isConcatSpreadable`
- `Symbol.iterator`
- `Symbol.toPrimitive`
- ...

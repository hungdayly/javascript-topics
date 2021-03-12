# Câu lệnh và biểu thức điều kiện

Đôi khi, chúng ta cần thực hiện các hành động khác nhau dựa trên các điều kiện khác nhau.

Để làm điều đó, chúng ta có thể sử dụng câu lệnh `if` và biểu thức điều kiện `?`, nó còn được gọi là toán tử "dấu hỏi".

## Câu lệnh `if`

Câu lệnh `if (...)` đánh giá một điều kiện trong dấu ngoặc đơn `(...)`, và nếu kết quả là `true`, thì thực thi một khối mã.

Ví dụ:

```javascript
let year = prompt('In which year was ECMAScript-2015 specification published?', '');

if (year == 2015) alert( 'You are right!' );
```

Trong ví dụ trên, điều kiện là một phép kiểm tra đẳng thức đơn giản (`year == 2015`), nhưng nó có thể phức tạp hơn nhiều.

Nếu chúng ta muốn thực thi nhiều hơn một câu lệnh, chúng ta phải bọc khối mã của mình bên trong dấu ngoặc nhọn:

```javascript
if (year == 2015) {
  alert( "That's correct!" );
  alert( "You're so smart!" );
}
```

### Chuyển đổi lôgic

Lệnh `if (...)` đánh giá biểu thức trong dấu ngoặc đơn và chuyển đổi kết quả thành giá trị lôgic.

Ta đã biết:

- Số `0` và `NaN`; chuỗi trống `""`; các giá trị đặc biệt `null` và `undefined` được chuyển thành `false`. Chúng được gọi là các giá trị *giả dối* (falsy).
- Các giá trị khác được chuyển thành `true`. Chúng được gọi là các giá trị *trung thực* (truthy).

Vì vậy, mã trong điều kiện này sẽ không bao giờ thực thi:

```javascript
if (0) { // 0 là "giả dối"
    // mã ở đây không chạy
}
```

... và bên trong điều kiện này sẽ luôn chạy:

```javascript
if (1) {  // 1 là "trung thực"
    // mã ở đây luôn chạy
}
```

### Mệnh đề `else`

Lệnh `if` có thể chứa một khối `else` tùy chọn. Nó thực thi khi điều kiện là sai.

Ví dụ:

```javascript
let year = prompt('In which year was the ECMAScript-2015 specification published?', '');

if (year == 2015) {
  alert( 'You guessed it right!' );
} else {
  alert( 'How can you be so wrong?' );
}
```
### Các mệnh đề `else if`

Đôi khi, chúng ta muốn thử một số biến thể của một điều kiện. Các mệnh đề `else if` cho phép chúng ta làm điều đó.

Ví dụ:

```javascript
let year = prompt('In which year was the ECMAScript-2015 specification published?', '');

if (year < 2015) {
  alert( 'Too early...' );
} else if (year > 2015) {
  alert( 'Too late' );
} else {
  alert( 'Exactly!' );
}
```

Sô mệnh đề `else if` không bị giới hạn, mệnh đề `else` có thể có hoặc không có.

## Biểu thức điều kiện `?`

Đôi khi, chúng ta cần gán một biến tùy thuộc vào một điều kiện.

Ví dụ:

```javascript
let accessAllowed;
let age = prompt('How old are you?', '');

if (age > 18) {
  accessAllowed = true;
} else {
  accessAllowed = false;
}

alert(accessAllowed);
```

Ta có thể sử dụng biểu thức điều kiện để thực hiện điều này một cách ngắn gọn và đơn giản hơn.

Biểu thức điều kiện sử dụng toán tử dấu hỏi `?`. Đôi khi toán tử này còn được gọi là *toán tử ba ngôi* vì nó có ba toán hạng. Nó là toán tử duy nhất trong JavaScript có ba toán hạng.

Cú pháp là:

```javascript
let result = condition ? value1 : value2;
```

Giá trị của `condition` được đánh giá: nếu nó là *trung thực* thì `value1` được trả về, nếu nó là *giả dối* thì `value2` được trả về.

Ví dụ:

```javascript
let accessAllowed = (age > 18) ? true : false;
```

Ta có thể bỏ dấu ngoặc đơn khi viết `condtion` bởi `?` có mức độ ưu tiên thấp hơn các toán tử so sánh.

```javascript
let accessAllowed = age > 18 ? true : false;
```

### Nhiều `?`

Ta có thể sử dụng nhiều toán tử `?` trong một biểu thức có nhiều điều kiện:

```javascript
let age = prompt('age?', 18);

let message = (age < 3) ? 'Hi, baby!' :
  (age < 18) ? 'Hello!' :
  (age < 100) ? 'Greetings!' :
  'What an unusual age!';

alert( message );
```

Nó tương đương với lệnh `if..else if..else` sau:

```javascript
if (age < 3) {
  message = 'Hi, baby!';
} else if (age < 18) {
  message = 'Hello!';
} else if (age < 100) {
  message = 'Greetings!';
} else {
  message = 'What an unusual age!';
}
```
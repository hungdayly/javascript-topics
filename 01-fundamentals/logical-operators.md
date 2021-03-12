# Các toán tử lôgic

Có bốn toán tử lôgic trong JavaScript: `||` (HOẶC), `&&` (VÀ), `!` (KHÔNG) và `??`. Ở bài này chúng ta đề cập đến 3 toán tử đầu tiên, `??` được đề cập đến trong bài viết tiếp theo.

Mặc dù chúng được gọi là toán tử "lôgic", chúng có thể được áp dụng cho các giá trị thuộc bất kỳ loại nào, không chỉ kiểu lôgic. Kết quả của chúng cũng có thể thuộc bất kỳ loại nào.

Cùng xem chi tiết nhé.

## `||` (HOẶC)

Toán tử "OR" được biểu thị bằng hai dấu thẳng đứng `||`:

```javascript
result = a || b
```

Trong lập trình cổ điển, phép toán lôgic HOẶC chỉ dùng để thao tác với các giá trị lôgic. Nếu có bất kỳ đối số nào của nó là `true`, nó trả về `true`, ngược lại, nó trả về `false`.

Trong JavaScript, toán tử `||` phức tạp hơn một chút và mạnh mẽ hơn. Nhưng trước tiên, hãy xem điều gì xảy ra với các giá trị lôgic.

Có 4 cách kết hợp có thể có:

```javascript
console.log( true || true );  // true
console.log( false || true );  // true
console.log( true || false );  // true
console.log( false || false );  // false
```

Như chúng ta thấy, kết quả luôn là `true` ngoại trừ trường hợp khi cả hai toán hạng đều `false`.

Nếu một toán hạng không phải là lôgic, nó được chuyển thành kiểu lôgic để đánh giá.

Ví dụ, số `1` được coi là `true`, số `0` xem như `false`:

```javascript
if (1 || 0) { // làm việc như if (true || false)
    console.log( 'truthy' );
}

// Kết quả: truthy
```

Hầu hết thời gian, `||` được dùng trong lệnh `if` để kiểm tra xem có điều kiện nào trong số các điều kiện nhất định được thỏa mãn (có giá trị `true`) không.

Ví dụ:

```javascript
let hour = 9;

if (hour < 10 || hour > 18) {
    console.log( 'The office is closed.' );
}

// Kết quả: The office is closed.
```

Chúng ta có thể kiểm tra nhiều điều kiện hơn:

```javascript
let hour = 12;
let isWeekend = true;

if (hour < 10 || hour > 18 || isWeekend) {
    console.log( 'The office is closed.' );
}

// Kết quả: The office is closed.
```

## `||` tìm giá trị trung thực (truthy) đầu tiên

Lôgic được mô tả ở trên hơi cổ điển. Bây giờ, hãy đưa các tính năng "bổ sung" của JavaScript vào.

Thuật toán mở rộng hoạt động như sau:

Xét phép toán:

```javascript
result = value1 || value2 || value3;
```

Toán tử `||` thực hiện như sau:

- Đánh giá toán hạng từ trái sang phải.
- Đối với mỗi toán hạng, chuyển đổi nó thành kiểu lôgic. Nếu kết quả là `true`, dừng và trả về giá trị ban đầu của toán hạng đó.
- Nếu tất cả các toán hạng đã được đánh giá (tức tất cả đều là `false`), trả về toán hạng cuối cùng.

Giá trị trả về là giá trị trước khi chuyển đổi.

Nói cách khác, một chuỗi toán tử `||` trả về giá trị trung thực (truthy) đầu tiên, hoặc giá trị cuối cùng nếu không tìm thấy giá trị trung thực nào.

Ví dụ:

```javascript
console.log( 1 || 0 );  // 1 (1 là giá trị trung thực đầu tiên)

console.log( null || 1 );  // 1 (1 là giá trị trung thực đầu tiên)
console.log( null || 0 || 1 );  // 1 (1 là giá trị trung thực đầu tiên)

console.log( undefined || null || 0 );  // 0 (0 là giá trị cuối cùng)
```

Điều này dẫn đến một số cách sử dụng thú vị so với toán tử HOẶC "cổ điển".

__1. Nhận giá trị trung thực đầu tiên từ danh sách các biến hoặc biểu thức.__

Ví dụ, chúng ta có `firstName`, `lastName` và `nickName` là các biến, tất cả là tùy chọn (có thể không xác định hoặc có giá trị giả dối).

Hãy sử dụng `||` để chọn cái có dữ liệu và hiển thị nó (hoặc `"Anonymous"` nếu không có gì được đặt):

```javascript
let firstName = "";
let lastName = "";
let nickName = "SuperCode";

console.log( firstName || lastName || nickName || "Anonymous" ); // SuperCoder
```

Nếu tất cả các biến là giả dối (falsy), `"Anonymous"` sẽ hiển thị.

__2.Chạy hay không chạy một lệnh__

Trong ví dụ dưới đây, chỉ có thông báo thứ hai được in:

```javascript
true || console.log("not printed");
false || console.log("printed");
```

Trong dòng đầu tiên, `||` dừng ngay sau khi đánh giá toán hạng đầu tiên khi nhìn thấy `true`, đo đó lệnh `console.log` không chạy.

## Toán tử `&&` (VÀ)

Toán tử VÀ được biểu diễn bằng hai dấu và `&&`:

```javascript
result = a && b;
```

Trong lập trình cổ điển, VÀ trả về `true` nếu hai toán hạng đều `true` và `false` nếu không:

```javascript
console.log( true && true );  // true
console.log( false && true );  // false
console.log( true && false );  // false
console.log( false && false ); // false
```

Một ví dụ với `if`:

```javascript
let hour = 12;
let minute = 30;

if (hour == 12 && minute == 30) {
    console.log( 'The time is 12:30' );
}

// Kết quả: The time is 12:30
```

Cũng giống như `||` bất kỳ giá trị nào cũng được phép làm toán hạng của `&&`:

```javascript
if (1 && 0) { // tương đương if (true && flase)
    console.log( "won't work, because the result is falsy" );
}
```

## `&&` tìm giá trị giả đối (falsy) đầu tiên

Xét phép toán:

```javascript
result = value1 && value2 && value3;
```

Toán tử `&&` thực hiện như sau:

- Đánh giá toán hạng từ trái sang phải.
- Đối với mỗi toán hạng, chuyển đổi nó thành kiểu lôgic. Nếu kết quả là `false`, dừng và trả về giá trị ban đầu của toán hạng đó.
- Nếu tất cả toán hạng đã được đánh giá (tức tất cả đều `true`), trả về toán hạng cuối cùng.

Nói cách khác, `&&` trả về giá trị giả đối đầu tiên hoặc giá trị cuối cùng nếu không tìm thấy giá trị nào.

Các quy tắc trên tương tự như `||`. Sự khác biệt là `&&` trả về giá trị falsy đầu tiên, trong khi `||` trả về giá trị truthy đầu tiên.

Ví dụ:

```javascript
// nếu toán hạng đầu tiên là truthy,
// && trả về toán hạng thứ hai:
console.log( 1 && 0 );  // 0
console.log( 1 && 5 );  // 5

// nếu toán hạng đầu tiên là falsy,
// && trả về nó. Toán hạng thứ hai không được đánh giá
console.log( null && 5 );  // null
console.log( 0 && "no matter what" );  // 0
```

Chúng ta cũng có thể chuyển nhiều giá trị liên tiếp. Xem các nó trả về giá trị giả đối đầu tiên:

```javascript
console.log( 1 && 2 && null && 3 );  // null
```

Khi tất cả đều trung thực (truthy), giá trị cuối cùng được trả về:

```javascript
console.log( 1 && 2 && 3 );  // 3
```

> Mức độ ưu tiên của `&&` cao hơn `||`. Vì vậy `a && b || c && d` giống như `(a && b) || (c && d)`.

## Toán tử KHÔNG `!`

Toán tử lôgic KHÔNG (PHỦ ĐỊNH) được biểu diễn bằng dấu chấm than `!`.

Cú pháp rất đơn giản:

```javascript
result = !value;
```

Toán tử này chấp nhận một đối số và thực hiện như sau:

1. Chuyển đổi các toán hạng về kiểu lôgic.
2. Trả về giá trị nghịch đảo.

Ví dụ:

```javascript
console.log( !true );  // false
console.log( !0 );  // true
```

`!!` đôi khi được dùng để chuyển đổi một giá trị thành kiểu lôgic:

```javascript
console.log( !!"non-empty string" );  // true
console.log( !!null );  // false
```

`!` đầu tiên chuyển đổi giá trị thành kiểu lôgic và trả về giá trị nghịch đảo và `!` thứ hai sẽ đảo ngược lại. Cuối cùng, chúng ta có một cách chuyển đổi giá trị thành kiểu lôgic đơn giản.

Có một cách dài dòng hơn để làm điều tương tự là sử dụng hàm tích hợp `Boolean`:

```javascript
console.log( Boolean("non-empty string" )); // true
console.log( Boolean(null) ); // false
```

> Mức độ ưu tiên của `!` là cao nhất trong các toán tử lôgic, vì vậy nó luôn thực hiện trước `&&` hoặc `||`.
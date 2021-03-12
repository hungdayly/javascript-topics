# Kiểu số

Trong JavaScript hiện đại, có 3 loại số:

1. Các số thông thường trong JavaScript được lưu trữ ở định dạng 64 bit IEEE-754, còn được gọi là "số dấu chấm động có độ chính xác kép". Đây là những con số mà chúng ta đang sử dụng trong hầu hết thời gian và chúng ta sẽ nói về chúng trong bài này.
2. Số nguyên lớn `BigInt`, để biểu diễn các số nguyên có độ dài tùy ý. Chúng đôi khi cần thiết, bởi vì một số thông thường không thể vượt quá 2<sup>53</sup> và nhỏ hơn -2<sup>53</sup>. Vì số nguyên lớn được sử dụng trong một số lĩnh vực đặc biệt, chúng ta sẽ dành cho chúng một bài riêng.

## Các cách khác nhau để viết một số

Hãy tưởng tượng chúng ta cần viết số 1 tỷ. Cách rõ ràng nhất là:

```javascript
let billion = 1000000000;
```

Chúng ta có thể dùng dấu gạch dưới `_` làm dấu phân cách:

```javascript
let billion = 1_000_000_000;
```

Tuy nhiên, trong cuộc sống thực, chúng ta cố gắng tránh viết các dãy số 0 dài. Trong JavaScript, chúng ta có thể rút ngắn các số `0` bằng cách thêm chữ cái `"e"` vào cuối và chỉ định số lượng các chữ số `0`:

```javascript
let billion = 1e9;  // 1 tỷ: số 1 theo sau là 9 số 0

console.log(7.3e9); // 7.3 tỷ: tương đương 7_300_000_000
```

Nói cách khác `MeN` tương đương nhân số `M` với "`1` theo sau là `N` số `0`":

```javascript
1e3 = 1 * 1000 // e3 nghĩa là nhân với 1000
1.23e6 = 1.23 * 1000000 // e6 nghĩa là nhân với 1000000
```

Bây giờ chúng ta hãy viết một cái gì đó rất nhỏ. Giả sử, 1 micro giây (một phần triệu giây):

```javascript
let ms = 0.000001;
```

Cũng giống như trước đây, việc sử dụng `"e"` có thể giúp ích cho chúng ta.

```javascript
let ms = 1e-6;  // 6 số 0 bên trái số 1
```

Nếu chúng ta đếm các số `0` trong `0.000001`, có 6 số như vậy.

Nói cách khác, `Me-N` tương đương chia `M` cho "`1` theo sau là `N` số `0`":

```javascript
// e-3 nghĩa là chia cho 1000
1e-3 = 1 / 1000 (=0.001)

// e-6 nghĩa là chi cho 1000000
1.23e-6 = 1.23 / 1000000 (=0.00000123)
```

### Số nhị phân, bát phân và thập lục phân

Số thập lục phân được sử dụng rộng rãi trong JavaScript để biểu thị màu sắc, mã hóa các ký tự và cho nhiều thứ khác. Vì vậy, tồn tại một cách ngắn gọn hơn để viết chúng: `0x` theo sau là các chữ số thập lục phân.

Ví dụ:

```javascript
console.log(0xff); // 255
console.log(0xFF); // 255
```

Hệ thống số nhị phân và bát phân hiếm khi được sử dụng, nhưng cũng được hỗ trợ bằng cách sử dụng các tiền tố `0b` và `0o`:

```javascript
let a = 0b11111111; // dạng nhị phân của số 255
let b = 0o377; // dạng bát phân của 255

console.log(a == b); // true
```

## Phương thức `.toString(base)`

Phương thức `num.toString(base)` trả về chuỗi biểu diễn số `num` trong hệ có cơ số là `base`.

Ví dụ:

```javascript
let num = 255;

console.log(num.toString(16)); // ff
console.log(num.toString(2)); // 11111111
```

Các `base` có thể thay đổi từ `2` tới `36`. Theo mặc định, nó là `10`.

## Làm tròn số

Một trong những thao tác được sử dụng nhiều nhất khi làm việc với số là làm tròn số.

Có một số hàm tích hợp sẵn dùng để làm tròn:

- **`Math.floor`**: làm tròn xuống số nguyên nhỏ hơn gần nhất, `3.1` trở thành `3` và `-1.1` trở thành `-2`.
- **`Math.ceil`**: làm tròn lên tới số nguyên lớn hơn gần nhất, `3.1` trở thành `4` và `-1.1` trở thành `-1`.
- **`Math.round`**: làm tròn đến số nguyên gần nhất, `3.1` trở thành `3`, `3.6` trở thành `4` và đặc biệt `3.5` trở thành `4` (làm tròn lên được áp dụng trong trường hợp này).
- **`Math.trunc`**: cắt bỏ phần lẻ của một số, chỉ giữ lại phần nguyên, `3.1` trở thành `3`, `-1.1` trở thành `-1`.

Phương thức `num.toFixed(n)` làm tròn số `num` đến `n` chữ số sau dấu chấm và trả về chuổi biểu diễn kết quả.

```javascript
let num = 12.34;
console.log(num.toFixed(1)); // "12.3"
```

Kết quả trả về là một chuỗi, nhưng ta có thể dễ dạng chuyển nó lại thành số bằng hàm chuyển đổi `Number()`: `Number(num.toFixed(1))` hoặc toán tử cộng một ngôi `+`: `+num.toFixed(1)`.

## Số vô hạn và NaN

JavaScript có những số đặc biệt sau:

- Có hai số vô hạn là `Infinity` và `-Infinity`.
- Số `NaN` đại diện cho một lỗi tính toán.

Các số bình thường không thuộc về các số này được gọi là các số "hữu hạn".

Chúng thuộc về kiểu `number` nhưng không phải số "bình thường", vì vậy có các hàm đặc biệt để kiểm tra chúng:

- `isNaN(value)`: chuyển đổi `value` thành số và sau đó kiểm tra xem nó có phải là `NaN` hay không.

```javascript
console.log(isNaN(NaN)); // true
console.log(isNaN("str")); // true
```

Đây là cách duy nhất để kiểm tra một giá trị có phải là `NaN` không, bởi `NaN` không thể so sánh với bất cứ giá trị nào, kể cả chính nó:

```javascript
console.log(NaN === NaN); // false
```

- `isFinite(value)`: chuyển đổi `value` thành số và sau đó kiểm tra xem nó có hữu hạn hay không:

```javascript
console.log(isFinite("15")); // true, bởi "15" -> 15
console.log(isFinite("str")); // false, bởi "str" -> NaN
console.log(isFinite(Infinity)); // false
```

## `parseInt` và `parseFloat`

Chuyển đổi số sử dụng toán tử `+` và hàm `Number()` không mềm dẻo. Nó bắt buộc một chuỗi phải biểu diễn chính xác một số, khi chuỗi có định dạng không phù hợp, chuyển đổi sẽ thất bại:

```javascript
console.log(+"100px"); // NaN
```

Ngoại lệ duy nhất là có thể có các khoảng trắng ở đầu và cuối chuỗi:

```javascript
console.log(Number("   100    ")); // 100
```

Nhưng trong cuộc sống thực, chúng ta thường có các giá trị số kèm theo đơn vị đăng sau như `"100px"`, `"12pt"` trong CSS, hay như `"19€"` ... và ta muốn trích xuất số từ chuỗi đó.

Trong những trường hợp này, chúng ta có thể sử dụng `parseInt` và `parseFloat`.

Những hàm này "phân tích" một chuỗi từ trái sang phải để trích xuất một số hợp lệ từ chuỗi này. Hàm `parseInt` chỉ phân tích số nguyên từ chuỗi, trong khi `parseFloat` có thể phân tích cả các số thực.

```javascript
console.log(parseInt("100px")); // 100
console.log(parseFlaot('12.5em')); // 12.5

console.log(parseInt('12.3')); // 12
console.log(parseFloat('12.3.4')); // 12.3
```

Nếu ngay từ đầu đã gặp phải những ký tự không hợp lệ, quá trình phân tích sẽ dừng lại và trả về `NaN`:

```javascript
console.log(parseInt('a123')); // NaN
```

Đối với `parseInt` còn có đối số thứ hai, đối số này chỉ định cơ số của số cần cần phân tích. Do đó, `parseInt` có thể phân tích các số viết dưới dạng nhị phân, bát phân, thập lục phân...

```javascript
console.log(parseInt('0xff', 16)); // 255
console.log(parseInt('ff', 16)); // 255

console.log(parseInt('2n9c', 36)); // 123456
```

## Các hàm toán học khác

JavaScript có sẵn một đối tượng `Math` chứa nhiều hàm và hằng số toán học.

Một số ví dụ:

**`Math.random()`**: trả về một số ngẫu nhiên từ `0` đến `1` (không bao gồm `1`).

```javascript
console.log( Math.random() ); // 0.1234567894322
console.log( Math.random() ); // 0.5435252343232
```

**`Math.max(a, b, c, ...)` / `Math.min(a, b, c, ...)`**: trả về giá trị lớn nhất/nhỏ nhất từ một số tùy ý các đối số.

```javascript
console.log(Math.max(3, 5, -10, 0, 1)); // 5
console.log(Math.min(1, 2)); // 1
```

**`Math.pow(n, power)`**: trả về `n` mũ `power`.

```javascript
console.log(Math.pow(2, 10)); // 1024 (2 mũ 10)
```

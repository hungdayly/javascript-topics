# Các kiểu dữ liệu

Giá trị trong JavaScript luôn thuộc một loại nhất định. Ví dụ, một chuỗi hoặc một số.

Có 8 kiểu dữ liệu cơ bản trong JavaScript. Ở đây, chúng ta sẽ trình bày tổng quát về chúng và trong các chương tiếp theo chúng ta sẽ nói chi tiết về từng kiểu dữ liệu.

Chúng ta có thể đặt bất cứ kiểu dữ liệu nào vào trong một biến. Ví dụ, một biến tại một thời điểm có thể là một chuỗi và sau đó lưu trữ một số:

```javascript
// không có lỗi
let message = "hello";
message = 123456;
```

Các ngôn ngữ lập trình cho phép như vậy, được gọi là ngôn ngữ có "kiểu dữ liệu động". Nghĩa là tồn tại các kiểu dữ liệu khác nhau, nhưng không tồn tại các biến có một kiểu dữ liệu nhất định.

## Kiểu số

```javascript
let n = 123;
n = 12.345;
```

*Kiểu số* đại diện cho cả số nguyên lẫn số thực dấu phảy động.

Có nhiều phép toán cho các số, ví dụ như nhân `*`, chia `/`, cộng `+`, trừ `-`,v.v.

Bên cạnh các số thông thường, JavaScript có những giá trị số rất đặc biệt, đó là: `Infinity`, `-Infinity` và `NaN`.

- `Infinity`: đại diện cho dương vô cùng trong Toán. Đó là một số đặc biệt, lớn hơn bất kỳ số nào. Ta có thể thu được nó khi chia một số dương cho số `0`:
    ```javascript
    alert( 1 / 0 );  // Infinity
    ```
    Hoặc có thể tham chiếu trực tiếp:
    ```javascript
    alert( Infinity );  // Infinity
    ```
- `NaN`: đại diện cho một lỗi tính toán. Ví dụ: nó là kết quả của một phép toán không hợp lệ, hoặc không xác định:
    ```javascript
    alert( "not a number" / 2 );  // NaN
    ```
    `NaN` được bảo toàn. Bất cứ phép toán nào xuất hiện `NaN` cuối cùng đều trả về `NaN`.
    ```javascript
    alert( "not a number" / 2 + 5 );  // NaN
    ```

## Kiểu BigInt

Trong JavaScript, kiểu số không thể biểu diễn được các số nguyên có độ dài tùy ý.

Kiểu `BigInt` được dùng để biểu diễn các số nguyên có độ dài tùy ý.

Một giá trị `BigInt` được tạo bằng cách thêm hậu tố `n` vào một số nguyên:

```javascript
const bigInt = 1234567890123456789012345678901234567890n;
```

## Kiểu chuỗi

Một chuỗi trong JavaScript được bao quanh bởi dấu nháy.

```javascript
let str = "Hello";
let str2 = 'Single quote are ok too';
let phrase = `can embed another ${str}`;
```

Trong JavaScript có 3 loại dấu nháy.

1. Dấu nháy kép: `"Hello"`
2. Dấu nháy đơn: `'Hello'`
3. Dấu tích ngược: `Hello`

Dấu nháy kép và dấu nháy đơn là những loại dấu nháy đơn giản. Thực tế, không có sự khác biệt giữa chúng trong JavaScript.

Dấu tích ngược là dấu nháy có chức năng mở rộng. Chúng cho phép chúng ta nhúng các biến và biểu thức vào một chuỗi bằng cách gói chúng vào `${...}`, ví dụ:

```javascript
let name = "John";

// nhúng một biến
alert( `Hello, ${name}!`);  // Hello, John!

// nhúng một biểu thức
alert( `the result is ${1 + 2}` );  // the result is 3
```

Biểu thức bên trong `${...}` được chạy và kết quả trả về trở thành một phần của chuỗi. Chúng ta có thể đưa bất cứ thứ gì vào đó: một biến như `name` hoặc một biểu thức số học như `1 + 2` hoặc một cái gì đó phức tạp hơn.

> JavaScript không có kiểu kí tự. Một kí tự vẫn là một chuỗi nhưng có chiều dài là 1.

## Kiểu lôgic

Kiểu lôgic chỉ có hai giá trị: `true` và `false`.

Loại này thường được sử dụng để lưu trữ các giá trị có/không: `true` nghĩa là "có, đúng" và `false` có nghĩa là "không, không chính xác".

Ví dụ:

```javascript
let nameFieldChecked = true;  // có, tên đã được khiểm tra
let ageFieldChekced = false; // không, tuổi chưa được kiểm tra
```

Các giá tri lôgic cũng là kết quả của các phép so sánh:

```javascript
let isGreater = 4 > 1;

alert(isGreater);  // true (so sánh trả về kết quả đúng)
```

## Kiểu "null"

Kiểu `null` là kiểu đặc biệt, chỉ có một giá trị duy nhất, cùng tên: `null`.

```javascript
let age = null;
```

Trong JavaScript, `null` là giá trị đặc biệt, biểu diễn "không có gì", "trống" hay "giá không xác định".

## Kiểu "undefined"

Kiểu `undefined` tương tự với `null`, cũng là kiểu đặc biệt, chỉ có một giá trị duy nhất là `undefined`.

Ý nghĩa của `undefined` là "một giá trị chưa được xác định".

Nếu một biến đã được khai báo, nhưng không được gán, thì giá trị của nó là `undefined`:

```javascript
let age;

alert(age); // hiển thị "undefined"
```

Về mặt kỹ thuật, có thể gán rõ ràng `undefined` cho một biến:

```javascript
let age = 100;

// đổi giá trị thành undefined
age = undefined;

alert(age);  // "undefined"
```

... Nhưng bạn không nên làm như vậy. Thông thường, người ta sử dụng `null` thay vì `undefined` trong trường hợp này. `undefined` được dành riêng làm giá trị ban đầu mặc định cho những biến chưa đƯợc gán giá trị ban đầu.

## Kiểu đối tượng

Kiểu đối tượng là kiểu đặc biệt.

Tất cả những kiểu khác được gọi là kiểu dữ liệu "cơ sở" vì giá trị của chúng chỉ có thể chứa một thứ duy nhất (có thể là một chuỗi, hoặc một số, hoặc bất cứ thứ gì). Ngược lại, các đối tượng được sử dụng để lưu trữ các tập hợp dữ liệu và các thực thể phức tạp hơn.

Là quan trọng như vậy, các đối tượng xứng đáng được đối xử đặc biệt. Chúng ta sẽ tìm hiểu kỹ hơn về chúng ở một chương sau, sau khi ta đã tìm hiểu hết về các kiểu dữ liệu cơ sở.

## Kiểu nhãn (symbol)

Các nhãn hay symbol được sử dụng để tạo ra các định danh duy nhất cho các thuộc tính của đối tượng. Ta trình bày chúng ở đây để cho đầy đủ. Ta sẽ tìm hiểu kỹ hơn về chúng sau khi đã tìm hiểu về các đối tượng.

## Toán tử typeof

Toán tử `typeof` trả về kiểu dữ liệu của toán hạng hoặc đối số của nó. Nó hữu ích khi chúng ta muốn xử lý các giá trị thuộc nhiều loại khác nhau hoặc chỉ muốn kiểm tra nhanh.

Nó hỗ trợ hai loại cú pháp:

1. Như một toán tử: `typeof x`.
2. Như một hàm: `typeof(x)`.

Lệnh gọi `typeof x` trả về một chuỗi chứa tên của kiểu dữ liệu:

```javascript
typeof undefined; // "undefined"

typeof 0;  // "number"

typeof 10n;  // "bigint"

typeof true;  // "boolean"

typeof "foo";  // "string"

typeof Symbol("id");  // "symbol"

typeof Math;  // "object"  (1)

typeof null;  // "object"  (2)

typeof alert;  // "function"  (3)
```

Ba dòng cuối cần giải thích thêm:

1. `Math` là một đối tượng tích hợp, cung cấp các phép toán. Chúng ta sẽ tìm hiểu nó ở một chương khác. Ở đây, nó chỉ đóng vai trò một ví dụ.

2. Kết quả của `typeof null` là `"object"`. Đó là một lỗi được chấp nhận của JavaScript để giữ lại sự tương thích ngược.

3. Kết quả của `typeof alert` là `"function"`, bởi vì `alert` là một hàm. Chúng ta sẽ nghiên cứu các hàm trong các chương tiếp theo, nơi chúng ta biết rằng, không có kiểu nào là kiểu hàm. Các hàm vẫn là các đối tượng. Nhưng `typeof` đối xử với hàm theo một cách đặc biệt, cho kết quả rõ ràng `"function"` thay vì `"object"`. Hành vi này của `typeof` là không đúng, nhưng lại thuận tiện khi làm việc với các hàm, do vậy nó được chấp nhận.

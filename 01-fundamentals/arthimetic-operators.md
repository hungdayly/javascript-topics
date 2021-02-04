# Các toán tử số học

Chúng ta biết nhiều phép toán từ trường học. Chúng là những phép toán như cộng `+`, trừ `-`, nhân `*`, chia `/`,v.v.

Trong bài này, chúng ta sẽ bắt đầu với các toán tử đơn giản, sau đó tập trung vào các khía cạnh dành riêng cho JavaScript, không thuộc số học ở trường học.

## Thuật ngữ: "một ngôi", "hai ngôi", "toán hạng"

Trước khi tiếp tục, hãy nắm bắt một số thuật ngữ phổ biến.

- *Toán hạng* - là đối tượng mà toán tử áp dụng lên. Ví dụ, trong phép nhân `5 * 2` có hai toán hạng: toán hạng bên trái là `5` và toán hạng bên phải là `2`. Đôi khi, mọi người gọi nó là những *đối số* thay vì *toán hạng*.

- Một toán tử được gọi là *một ngôi* nếu nó chỉ cần một toán hạng duy nhất để hoạt động. Ví dụ, toán tử đảo dấu `-` là một toán tử một ngôi:

    ```javascript
    let x = 1;

    x = -x;
    alert( x );  // -1
    ```

- Một toán tử được gọi là *hai ngôi* nếu nó cần hai toán hạng để hoạt động. Dấu trừ cũng tồn tại ở dạng hai ngôi, tức là phép toán trừ:

    ```javascript
    let x = 1, y = 3;
    alert( y - x );  // 2
    ```

## Các phép toán

Các phép toán sau được hỗ trợ:

- Phép cộng: `+`
- Phép trừ: `-`
- Phép nhân: `*`
- Phép chia: `/`
- Chia lấy dư: `%`
- Lũy thừa: `**`

Bốn phép toán đầu tiên rất đơn giản, hai phép toán cuối cần giải thích thêm.

### Chia lấy dư `%`

Phép toán `a % b` là số dư của phép chia `a` cho `b`.

Ví dụ:

```javascript
alert( 5 % 2 );  // 1
alert( 8 % 3 );  // 2
```

### Lũy thừa `**`

Phép toán `a ** b` trả về kết quả là "a mũ b".

Ví dụ:

```javascript
alert( 2 ** 2 );  // 4
alert( 2 ** 3 );  // 8
alert( 2 ** 4 );  // 16
```

Lũy thừa cũng được định nghĩa cho các số không nguyên. Ví dụ căn bậc hai là lũy thừa của `1/2`:

```javascript
alert( 4 ** (1/2) );  // 2
alert( 8 ** (1/3) );  // 2
```

## Toán tử nối chuỗi `+`

Hãy cùng gặp gỡ các tính năng khác của toán tử JavaScript, vượt ra ngoài số học ở trường học.

Thông thường toán tử `+` dùng để cộng hai số.

Nhưng nếu, toán tử `+` áp dụng cho các chuỗi, nó sẽ hợp nhất (nối) chúng.

```javascript
let s = "my" + "string";
alert(s);  // mystring
```

Thực ra chỉ cần một toán hạng là chuỗi, toán hạng kia tự được chuyển thành chuỗi và chúng được nối với nhau.

Ví dụ:

```javascript
alert( '1' + 2 );  // "12"
alert( 2 + '1' );  // "21"

alert( 2 + 2 + '1' );  // "41"
```

Chỉ toán tử `+` mới hỗ trợ thao tác nối chuỗi này. Các toán tử số học khác chỉ làm việc với các số và luôn chuyển đổi toán hạng của chúng thành số.

Ví dụ:

```javascript
alert( 6 - '2' );  // 4
alert( '6' / '2' );  // 3
```

## Toán tử chuyển đổi số `+`

Toán tử `+` còn tồn tại ở dạng một ngôi.

Nếu toán hạng là một số, nó không có tác dụng gì.

Nếu toán hạng không phải số, thì nó chuyển toán hạng này thành số.

Ví dụ:

```javascript
// Không có tác dụng với các số
let x = 1;
alert( +x );  // 1

let y = -2;
alert( +y ); // -2

// Chuyển đổi các toán hạng không phải số
alert( +true );  // 1
alert( +"" );  // 0
```

Nó tương đương với `Number(...)` nhưng ngắn hơn.

## Thứ tự ưu tiên

Nếu một biểu thức có nhiều hơn một toán tử, thứ tự thực hiện được xác định theo *thư tự ưu tiên* của chúng.

Từ trường học, chúng ta đều biết rằng phép nhân đƯợc thực hiện trước phép cộng. Đó chính là *thứ tự ưu tiên*. Phép nhân có *thứ tự ưu tiên* cao hơn phép cộng.

Dấu ngoặc đơn, dùng để thay đổi thứ tự ưu tiên mặc định của các toán tử. Toán tử đặt giữa dấu ngoặc đơn mặc nhiên có thứ tự ưu tiên cao nhất.

Trong các toán tử số học ta đang nói đến, thư tự ưu tiên xếp từ cao xuống thấp như sau:

| Thứ tự | Tên toán hạng | Ký hiệu |
|--------|---------------|---------|
| 17     | Cộng một ngôi | `+`     |
| 17     | Trừ một ngôi  | `-`     |
| 16     | Lũy thừa      | `**`    |
| 15     | Phép nhân     | `*`     |
| 15     | Phép chia     | `/`     |
| 13     | Phép cộng     | `+`     |
| 13     | Phép chia     | `-`     |


## Toán tử gán `=`

Hãy lưu ý rằng, phép gán `=`, thực ra cũng là một toán tử, nó có *thứ tự ưu tiên* là `3`, tức rất thấp.

Đó là lý do tại sao khi chúng ta gán một biến, chẳng hạn như `x = 2 * 2 + 1`, các phép tính được thực hiện trước và sau đó `=` mới chạy và lưu trữ kết quả trong biến `x`.

```javascript
let x = 2 * 2 + 1;

alert(x);  // 5
```

### Toán tử `=` trả về một giá trị

Tất cả các toán tử trong JavaScript đều trả về một giá trị. Nó rất hiển nhiên cho các toán tử `+`, `-`, `*`, `/` v.v. nhưng cũng đúng cho toán tử `=`.

Gọi `x = value` ghi `value` vào `x` và sau đó trả về chính giá trị `value` này.

Đây là ví dụ minh họa điều này:

```javascript
let a = 1;
let b = 2;

let c = 3 - (a = b + 1);

alert( a );  // 3
alert( c );  // 0
```

### Một dãy các lệnh gán

Một tính năng thú vị khác là ta có thể viết một dãy các lệnh gán:

```javascript
let a, b, c;

a = b = c = 2 + 2;

alert( a );  // 4
alert( b );  // 4
alert( c );  // 4
```

Thực tế các toán tử `=` được chạy lần lượt từ phải qua trái.

## Sửa đổi tại chỗ

Chúng ta thường cần áp dụng một toán tử cho một biến và lưu trữ kết quả trong cùng một biến đó.

Ví dụ:

```javascript
let n = 2;
n = n + 5;
n = n * 2;

alert( n );  // 14
```

Ta có thể viết ngắn hơn bằng cách sử dụng các toán tử `+=` và `*=`:

```javascript
let n = 2;
n += 5; // giờ n = 7 (giống như n = n + 5)
n *= 2; // giờ n = 14 (giống như n = n * 2)

alert( n );  // 14
```

Tất cả các toán tử số học đều hỗ trợ dạng kết hợp này, ví dụ `/=`, `-=`, `**=`, `%=`, v.v.

Các toán tử này có thứ tự ưu tiên như toán tử gán thông thường, nên chúng hầu như chạy sau các phép tính khác.

```javascript
let n = 2;

n *= 3 + 5;

alert( n );  // 16
```

## Tăng/giảm

Tăng hoặc giảm một số là một trong những phép toán phổ biến nhất.

Vì vậy, có những toán tử đặc biệt cho nó:

- **Toán tử tăng**: `++` làm tăng một biến số lên `1`:
    ```javascript
    let counter = 2;
    counter++;  // tương đương counter = counter + 1
    alert( counter );  // 3
    ```
- **Toán tử giảm**: `--` làm giảm một biến đi `1`:
    ```javascript
    let counter = 2;
    counter--;  // tương đương counter = counter - 1
    alert( counter );  // 1
    ```

Các toán tử `++` và `--` có thể được đặt trước hoặc sau toán hạng của nó. Khác biệt chỉ là giá trị trả về là giá trị của biến trước hay sau khi thay đổi.

- Khi đặt sau: trả về giá trị trước khi thay đổi, ví dụ `counter++`.

    Ví dụ:
    ```javascript
    let counter = 1;
    let a = ++counter;

    alert( counter );  // 2
    alert( a );  // 2
    ```

- Khi đặt trước: trả về giá trị sau khi thay đổi, ví dụ `++counter`.

    Ví dụ:
    ```javascript
    let counter = 1;
    let a = counter++;

    alert( counter );  // 2
    alert( a );  // 1
    ```

## Toán tử bitwise

Các toán tử bitwise coi các toán hạng là các số nguyên 32 bit và hoạt động ở cấp độ biểu diễn nhị phân của chúng.

Các toán tử này không chỉ JavaScript có. Chúng được hỗ trợ trong hầu hết các ngôn ngữ lập trình.

Danh sách các toán tử bitwise:

- VÀ (`&`)
- HOẶC (`|`)
- HOẶC LOẠI TRỪ (`^`)
- KHÔNG (`~`)
- DỊCH TRÁI (`<<`)
- DỊCH PHẢI (`>>`)


Các toán tử này rất hiếm khi được sử dụng. Nên chúng ta không đề cập tới chúng trong loạt bài này.

## Dấu phảy

Toán tử dấu phảy `,` là một trong những toán tử hiếm sử dụng nhất. Đôi khi nó được sử dụng để viết mã ngắn hơn.

Toán tử dấu phảy cho phép chúng ta chạy một số biểu thức, phân chia chúng bằng dấu phảy `,`. Tất cả các biểu thức được chạy, nhưng chỉ kết quả của biểu thức cuối cùng được trả về.

Ví dụ:

```javascript
let a = (1 + 2, 3 + 4);

alert( a );  // 7
```

Toán tử dấu phảy có thứ tự ưu tiên vô cùng thấp, thấp hơn cả toán tử gán, vì vậy dấu ngoặc cần được sử dụng trong ví dụ trên.
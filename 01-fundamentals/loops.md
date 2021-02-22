# Vòng lặp `while` và `for`

Chúng ta thường cần lặp lại các hành động.

Ví dụ: xuất hàng hóa lần lượt từ một danh sách hoặc chỉ chạy cùng một mã cho mỗi số từ 1 đến 10.

*Vòng lặp* là một cách để lặp lại cùng một mã nhiều lần.

## Vòng lặp "while"

Vòng lặp `while` có cú pháp sau:

```javascript
while (condition) {
    // mã cần lặp lại
    // còn gọi là "thân vòng lặp"
}
```

Khi `conditon` là `true`, thân vòng lặp sẽ được thực thi.

Ví dụ: vòng lặp bên dưới xuất ra `i` khi `i < 3`:

```javascript
let i = 0;
while (i < 3) { // hiện 0, rồi 1, rồi 2
    console.log(i);
    i++;
}
```

Mỗi lần thực thi thân vòng lặp gọi là *một lần lặp*. Vòng lặp trong ví dụ trên thực hiện 3 lần lặp.

Nếu không có `i++` trong thân vòng lặp, vòng lặp sẽ lặp lại (theo lý thuyết) mãi mãi. Thực tế, trình duyệt sẽ phát hiện một vòng lặp vô hạn và tự động dừng nó lại.

Bất kỳ biểu thức hoặc biến nào cũng có thể đóng vai trò điều kiện lặp `condition`: giá trị của biến/biểu thức được chuyển đổi thành giá trị lôgic bởi `while`.

Ví dụ, một cách viết ngắn hơn của `while (i != 0)` là `while (i)`:

```javascript
let i = 3;
while (i) { // khi i trở thành 0, nó trở thành falsy, và vòng lặp dừng
    console.log(i);
    i++;
}
```

> Nếu thân vòng lặp chỉ có một lênh, có thể không cần dùng `{...}`:
> ```javascript
> let i = 3;
> while (i) console.log(i--);
> ```

## Vòng lặp "do..while"

Phần kiểm tra điều kiện có thể di chuyển xuống dưới thân vòng lặp bằng vòng lặp `do..while`, cú pháp là:

```javascript
do {
    // thân vòng lặp
} while (condition)
```

Đầu tiên, vòng lặp sẽ thực hiện phần thân, sau đó kiểm tra điều kiện, khi điều còn là truthy thì thân vòng lặp sẽ được chạy lại nhiều lần.

Ví dụ:

```javascript
let i = 0;
do {
    console.log(i);
    i++;
} while (i < 3)
```

Dạng cú pháp này chỉ nên được sử dụng khi bạn muốn phần thân của vòng lặp phải được thực thi **ít nhất một lần** bất kể điều kiện là truthy hay falsy. Thông thường cú pháp `while (...) {...}` được ưa thích hơn.

## Vòng lặp "for"

Các vòng lặp `for` phức tạp hơn, nhưng nó cũng là vòng lặp thường sử dụng nhất.

Nó trông như thế này:

```javascript
for (begin; condition; step) {
    // body (thân vòng lặp)
}
```

Hãy cùng tìm hiểu ý nghĩa của những phần này bằng ví dụ.

Ví dụ bên dưới chạy `console.log(i)` cho `i` từ `0` đến (nhưng không bao gồm) `3`.

```javascript
for (let i = 0; i < 3; i++) { // hiện 0, rồi 1, rồi 2
    console.log(i);
}
```

Hãy xem từng phần của câu lệnh `for` trên:

| Phần | Nội dung | Ý nghĩa |
|------|----------|---------|
| begin | `i = 0` | Thực thi một lần khi bắt đầu vòng lặp |
| condition | `i < 3` | Được kiểm tra trước mỗi lần lặp lại thân vòng lặp |
| body | `console.log(i)` | Thân vòng lặp, chạy đi chạy lại khi điều kiện là truthy |
| step | `i++` | Thực thi sau mỗi lần lặp lại thân vòng lặp |

Nói chung, thuật toán của vòng lặp `for` như sau:

```javascript
Chạy begin
-> (nếu condition -> chạy body và step)
-> (nếu condition -> chạy body và step)
-> (nếu condition -> chạy body và step)
-> ...
```

Có thể viết lại ví dụ trên bằng lệnh `if` như sau:

```python
// for (let i = 0; i < 3; i++) console.log(i)

// chạy begin
let i = 0;
// nếu condition -> chạy body và step
if (i < 3) { console.log(i); i++ }
// nếu condition -> chạy body và step
if (i < 3) { console.log(i); i++ }
// nếu condition -> chạy body và step
if (i < 3) { console.log(i); i++ }
// ...kết thúc, bởi vì giờ i == 3
```

> **Biến của vòng lặp**
> Ở đây, biến đếm `i` được khai báo bên trong vòng lặp. Các biến như vậy chỉ hiển thị trong vòng lặp.
> ```javascript
> for (let i = 0; i < 3; i++) {
>   console.log(i); // 0, 1, 2
> }
> console.log(i); // error, no such variable
> ```
> Thay vì định nghĩa một biến, chúng ta có thể sử dụng một biến hiện có:
> ```javascript
> let i = 0;
>
> for (i = 0; i < 3; i++) { // sử dụng biến đã tồn tại
>   console.log(i); // 0, 1, 2
> }
>
> console.log(i); // 3
> ```

### Bỏ qua các phần

`for` có thể bỏ qua bất cứ phần nào của nó.

Ví dụ, chúng ta có thể bỏ qua `begin` nếu chúng ta không cần phải làm gì khi bắt đầu vòng lặp.

Chẳng hạn:

```javascript
let i = 0;

for (; i < 3; i++) {
    console.log(i); // 0, 1, 2
}
```

Chúng ta cũng có thể bỏ phần `step`:

```javascript
let i = 0;

for (; i < 3;) {
    console.log(i++);
}
```

Vòng lặp `for` lúc này giống hệt như `while (i < 3)`.

Chúng ta có thể bỏ qua mọi thứ, tạo ra một vòng lặp vô hạn:

```javascript
for (;;) {
    // lặp lại mãi mãi
}
```

## Kết thúc vòng lặp

Thông thường, vòng lặp chỉ bị kết thúc khi điều kiện trở nên sai.

Nhưng chúng ta có thể buộc vòng lặp kết thúc bất cứ lúc nào bằng lệnh đặc biệt `break`.

Ví dụ: vòng lặp bên dưới yêu cầu người dùng nhập một chuỗi số, kết thúc ngay vòng lặp nếu không có số nào được nhập:

```javascript
let sum = 0;

while (true) {
    let value = +prompt("Enter a number", '');

    if (!value) break;

    sum += value;
}

console.log('Sum: ' + sum);
```

## Kết thúc lần lặp

Khác với `break` lệnh `continue` không kết thúc toàn bộ vòng lặp mà chỉ kết thúc lần lặp hiện tại và chuyển ngay sang lần lặp tiếp theo (nếu điều kiện vẫn đúng).

Chúng ta thường dùng nó trong trường hợp công việc ở lần lặp hiện tại đã hoàn tất và muốn chuyển nhanh sang lần lặp tiếp theo.

Vòng lặp bên dưới sử dụng `continue` để xuất ra các số lẻ:

```javascript
for (let i = 0; i < 10; i++) {
    // nếu đúng, bỏ qua các lệnh phía sau
    if (i % 2 == 0) continue;

    console.log(i); // 1, rồi 3, 5, 7, 9
}
```

## Tạo nhãn cho break/continue

Đôi khi chúng ta cần kết thúc nhiều vòng lặp lồng nhau một lúc.

Ví dụ, trong đoạn mã dưới đây, chúng ta lặp lại `i` và `j` và yêu cầu người dùng nhập các giá trị đối với các tọa độ `(i, j)` từ `(0, 0)` đến `(2, 2)`:

```javascript
for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        let input = prompt(`Value at coords (${i},${j})`, '');

        // làm sao để kết thúc ở đây?
    }
}

console.log('Done');
```

Bình thường `break` (và `continue`) chỉ phá vỡ luồng thực thi của vòng lặp trực tiếp chứa nó.

Một *nhãn* là một định danh theo sau là một dấu hai chấm và đặt trước một vòng lặp:

```javascript
labelName: for (...) {
    // thân vòng lặp
}
```

Câu lệnh `break <labelName>` trong vòng lặp kết thúc vòng lặp có nhãn là `labelName`.

```javascript
outer: for (let i = 0; i < 3; i++) {
    for (let j = 0; j < 3; j++) {
        let input = prompt(`Value at coords (${i}, ${j})`, '');

        // nếu không nhập thì kết thúc cả hai vòng lặp
        if (!input) break outer;

        // nếu nhập thì thực hiện gì đó với giá trị được nhập
    }
}

console.log('Done');
```

Tương tự `continue <labeName>` kết thúc lần lặp hiện tại của vòng lặp có nhãn `labelName`.
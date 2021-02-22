# Lệnh switch

Một câu lệnh `switch` có thể thay cho nhiều lần kiểm tra `if`.

## Cú pháp

Một lệnh `switch` có nhiều khối `case` và một khối `default` không bắt buộc.

Nó trông như thế này:

```javascript
switch (x) {
    case 'value1': // if (x === 'value1')
        ...
        [break]
    case 'value2': // if (x === 'value2')
        ...
        [break]
    ...

    case 'valueN': // if (x === 'valueN')
        ...
        [break]
    default:
        ...
        [break]
}
```

- Giá trị của `x` được kiểm tra xem có bằng nghiêm ngặt (`===`) từ giá trị đầu tiên của `case` (tức `value1`) đến giá trị cuối cùng của `case` (tức `valueN`).
- Nếu thấy bằng nhau, `switch` bắt đầu thực thi mã từ `case` tương ứng cho đến khi gặp lệnh `break` (hoặc đến cuối `switch` nếu không gặp `break` nào).
- Nếu không thấy bằng nhau ở `case` nào thì `default` được thực thi (nếu nó tồn tại).

## Một ví dụ

```javascript
let a = 2 + 2;

switch (a) {
    case 3:
        console.log('Too small');
        break;
    case 4:
        console.log('Exactly!');
        break;
    case 5:
        console.log('To big');
        break;
    default:
        console.log("I don't know such values");
}
```

Ở ví dụ này `switch` bắt đầu so sánh `a` từ `case` đầu tiên (tức so sánh với `3`), thấy không khớp.

Sau đó `switch` so sánh với `case` tiếp theo (so sánh với `4`), thấy khớp nên `switch` bắt đầu thực thi khối các lệnh từ `case 4:` trở đi cho đến khi gặp `break`.

Trong ví dụ này lệnh duy nhất được thực thi là `console.log('Exactly!')`.

Đây là câu chuyện xảy ra khi không có `break`:

```javascript
let a = 2 + 2;

switch (a) {
    case 3:
        console.log('To small!');
    case 4:
        console.log('Exactly!')
    case 5:
        console.log('To big');
    default:
        console.log("I dont' know such values");
}
```

Do không gặp "chướng ngại vật" (tức lệnh `break`) nào, nên `switch` chạy tất cả các lệnh từ `case 4:` trở đi. Cụ thể là chạy các lệnh sau:

```javascript
console.log('Exactly!');
console.log('To big');
console.log("I don't know such values")
```

> **Cả `switch` lẫn `case` cho phép bất cứ biểu thức nào**
> Ví dụ:
> ```javascript
> let a = "1";
> let b = 0;
>
> switch (+a) {
>   case b + 1:
>       console.log("this runs, because +a is 1, exactly equals b+1");
>       break;
>   default:
>       console.log("this doesn't run")
> }
> ```

## Nhóm nhiều case với nhau

Nếu có nhiều `case` cùng chia sẻ một đoạn mã, chúng ta nên nhóm chúng với nhau.

Ví dụ: nếu chúng ta muốn chạy cùng một mã với `case 3` và `case 5`:

```javascript
let a = 3;

switch (a) {
    case 4:
        console.log('Right!');
        break;
    
    case 3:
    case 5:
        console.log('Wrong!');
        console.log("Why don't you take a match class?");
        break;

    default:
        console.log('The result is strange. Really.');
}
```
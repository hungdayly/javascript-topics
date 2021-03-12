# So sánh

Chúng ta đã biết nhiều toán tử so sánh từ Toán học:

Trong JavaScript, chúng được viết như thế này:

- Lớn hơn/nhỏ hơn: `a > b`, `a < b`.
- Lớn hơn/nhở hơn hoặc bằng: `a >= b`, `a <= b`.
- Bằng nhau: `a == b`.
- Không bằng nhau: `a != b`.

Trong bài này, chúng ta sẽ tìm hiểu thêm về các kiểu toán tử so sánh, các JavaScript thực hiện chúng, bao gồm cả những đặc thù quan trọng.

## Giá trị lôgic là kết quả

Tất cả các toán tử so sánh đều trả về một giá trị lôgic:

- `true` - nghĩa là "có", "đúng" hoặc "sự thật".
- `false` - nghĩa là "không", "sai" hoặc "không phải sự thật".

Ví dụ:

```javascript
console.log( 2 > 1 );  // true (đúng)
console.log( 2 == 1 );  // false (sai)
console.log( 2 != 1 );  // true (đúng)
```

Kết quả so sánh có thể gán cho một biến, giống như bất cứ giá trị nào khác:

```javascript
let result = 5 > 4;
console.log( result ); // true
```

## So sánh chuỗi

Để xem liệu một chuỗi có lớn hơn chuỗi khác hay không, JavaScript sử dụng cái gọi là thứ tự "từ điển" hoặc "từ điển".

Nói cách khác, các chuỗi được so sánh từng chữ cái với nhau.

Ví dụ:

```javascript
console.log( 'Z' > 'A' ); // true
console.log( 'Glow' > 'Glee' ); // true
console.log( 'Bee' > 'Be' ); // true
```

Thuật toán để so sánh hai chuỗi rất đơn giản:

1. So sánh ký tự đầu tiên của cả hai chuỗi.
2. Nếu ký tự đầu tiên từ chuỗi đầu tiên lớn hơn (hoặc nhỏ hơn) so với chuỗi thứ hai, thì chuỗi đầu tiên lớn hơn (hoặc nhỏ hơn) chuỗi thứ hai.
3. Ngược lại, nếu các kí tự đầu tiên của cả hai chuỗi giống nhau, tiếp tục so sánh các kí tự thứ hai của hai chuỗi theo cùng một cách như trên.
4. Lặp lại cho đến khi kết thúc một trong hai chuỗi.
5. Nếu cả hai chuỗi kết thúc ở cùng độ dài, thì chúng bằng nhau. Nếu không, chuỗi dài hơn sẽ lớn hơn.

Trong ví dụ đầu tiên ở trên, phép so sánh `'Z' > 'A'` có được kết quả ở bước đầu tiên.

So sánh thứ hai `Glow` và `Glee` cần nhiều bước hơn vì các chuỗi được so sánh từng ký tự:

1. `G` giống như `G`
2. `l`giống như `l`
3. `o` lớn hơn `e`. Dừng ở đây. Chuỗi đầu tiên sẽ lớn hơn.

> **Không phải thứ tự từ điển, mà là thự tự Unicode**
> 
> Thuật toán so sánh được đưa ra ở phần trên gần tương đương với thuật toán được sử dụng trong từ điển hoặc danh bạ điện thoại, nhưng không hoàn toàn giống.
> 
> Ví dụ, về cách viết hoa, thường. Một chữ `"A"` viết hoa không bằng chữ `"a"` viết thường. Cái nào lớn hơn? Đó là chữ thường `"a"`. Tại sao? Vì ký tự viết thường có chỉ số lớn hơn trong bảng mã Unicode (JavaScript sử dụng bảng mã Unicode).

## So sánh khác kiểu

Khi so sánh các giá trị khác kiểu, JavaScript sẽ **chuyển đổi chúng thành số**.

Ví dụ:

```javascript
console.log( '2' > 1 ); // true, '2' thành số 2
console.log( '01' == 1 ); // true, '01' thành số 1
```

Một ví dụ khác, trong đó `true` trở thành `1` và `false` trở thành `0`.

```javascript
console.log( true == 1 ); // true
console.log( false == 0 ); // true
```

## So sánh nghiêm ngặt

So sánh bằng thông thường bằng toán tử `==` có một vấn đề. Nó không thể phân biệt được `0` và `false`:

```javascript
console.log( 0 == false );  // true
```

Điều tương tự sảy ra với `''` và `false`:

```javascript
console.log( '' == false );  // true
```

Điều này sảy ra do các toán hạng của `==` được chuyển đổi thành số. Một chuỗi trống `''` và giá trị lôgic `false` đều được chuyển thành số `0`.

Phải làm gì, nếu muốn phân biệt `0` với `false`?

**Toán tử `===` kiểm tra sự bằng nhau của hai toán hạng mà không thực hiện chuyển đổi kiểu.**

Nói cách khác, nếu `a` và `b` khác kiểu, `===` coi chúng luôn khác nhau.

```javascript
console.log( 0 === false );  // false
```

Ngược với `===` là `!==` cũng không thực hiện chuyển đổi:

```javascript
console.log( 0 !== false );  // true
```

## So sánh với `NaN`, `null` và `undefined`

### So sánh với `NaN`

`NaN` là một giá trị đặc biệt trả về `false` cho mọi loại so sánh, ngay cả khi so sánh với chính nó:

```javascript
console.log( NaN == NaN );  // false
```

### So sánh với `undefined`

Khi so sánh nghiêm ngặt, `undefined` chỉ bằng chính nó:

```javascript
console.log( undefined === undefined );  // true
```

Khi so sánh thông thường, `undefined` cũng bằng `null`, ngoài ra không bằng giá trị nào khác.

```javascript
console.log( undefined == null );  // true
```

Tất cả các trường hợp còn lại, `undefined` chuyển thành `NaN`, vậy nên không thể so sánh với bất cứ giá trị nào (giống `NaN`):

```javascript
console.log( undefined > 0 );  // false
console.log( undefined < 0 );  // false
console.log( undefined == 0 );  // false
```

### So sánh với `null`

Khi so sánh nghiêm ngặt, `null` chỉ bằng chính nó:

```javascript
console.log( null === null );  // true
```

Khi so sánh thông thường, `null` cũng bằng `undefined`, ngoài ra không bằng giá trị nào nữa:

```javascript
console.log( null == undefined );  // true
```

Tất cả các trường hợp còn lại, `null` chuyển thành `0`:

```javascript
console.log( null > 0 );  // false, giống 0 > 0
console.log( null >= 0 );  // true, giống 0 >= 0

// nhưng
console.log( null == 0 );  // false
```
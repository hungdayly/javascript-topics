# Đối tượng

Như chúng ta đã biết, có tám kiểu dữ liệu trong JavaScript. Bảy trong số đó là các kiểu dữ liệu cơ sở, bởi vì giá trị của chúng chỉ chứa một thứ duy nhất (có thể là một chuỗi hoặc một số hoặc bất cứ thứ gì).

Ngược lại, các đối tượng được sử dụng để lưu trữ các bộ sưu tập có khóa gồm nhiều dữ liệu khác nhau và các thực thể phức tạp hơn. Trong JavaScript, các đối tượng thâm nhập vào hầu hết mọi khía cạnh của ngôn ngữ. Vì vậy, chúng ta phải hiểu chúng trước khi đi sâu vào bất cứ phần nào khác của ngôn ngữ.

Một đối tượng có thể được tạo bằng dấu ngoặc `{...}` với danh sách các thuộc tính. Thuộc tính là một cặp "key: value" ("khóa: giá trị"), trong đó khóa phải là một chuỗi (còn được gọi là "tên thuộc tính") và giá trị có thể là bất cứ thứ gì.

Có thể tạo một đối tượng trống bằng một trong hai cú pháp:

```javascript
let user = new Object();
let user = {};
```

Thông thường `{}` được sử dụng nhiều hơn.

## Literal và thuộc tính

```javascript
let user = {        // một đối tượng
    name: "John",   // key "name" lưu giá trị "John"
    age: 30,        // key "age" lưu giá trị 30
};
```

Một thuộc tính có một khóa (key) còn được gọi là tên của thuộc tính đặt trước dấu hai chấm `":"` và một giá trị ở bên phải của nó.

Trong đối tượng `user`, có hai thuộc tính:

1. Thuộc tính đầu tiên có tên `"name"` và giá trị `"John"`.
2. Thuộc tính thứ hai có tên `"age"` và giá trị `30`.

Chúng ta có thể thêm, xóa và đọc các thuộc tính bất kỳ lúc nào.

Các giá trị thuộc tính có thể truy cập bằng ký hiệu dấu chấm:

```javascript
// truy cập thuộc tính của đối tượng
console.log(user.name); // John
console.log(user.age);  // 30
```

Giá trị có thể thuộc bất kỳ loại nào. Hãy thêm một giá trị lôgic:

```javascript
// thêm thuộc tính cho đối tượng
user.isAdmin = true;
```

Để xóa một thuộc tính, chúng ta có thể sử dụng toán tử `delete`:

```javascript
// xóa thuộc tính của đối tượng
delete user.age;
```

Tên thuộc tính khi có nhiều từ phân cách nhau bởi khoảng trắng, chúng ta phải viết nó như chuỗi:

```javascript
let user = {
    name: "John",
    age: 30,
    "likes birds": true
};
```

Thuộc tính cuối cùng có thể kết thúc bởi dấu phảy (dấu phảy treo):

```javascript
let user = {
    name: "John",
    age: 30
};
```

Dấu phảy treo giúp cho việc thêm/bớt/di chuyển các thuộc tính trở nên dễ dàng hơn vì tất cả các dòng đều giống nhau.

## Dấu ngoặc vuông

Đối với thuộc tính có nhiều từ cách nhau bởi khoảng trắng, chúng ta không thể sử dụng dấu chấm `.` để truy cập thuộc tính:

```javascript
// nó dẫn đến lỗi cú pháp
user.likes birds = true;
```

JavaScript không hiểu điều đó. Nó nghĩa rằng chúng ta truy cập `user.likes`, và dẫn tới lỗi cú pháp khi gặp từ không mong đợi là `birds`.

Dấu chấm yêu cầu tên thuộc tính phải là một định danh hợp lệ. Tức là tên thuộc tính phải không chứa khoảng trắng, không bắt đầu bằng chữ số và không bao gồm các ký tự đặc biệt (ngoại trừ `$` và `_`).

Có kí hiệu dấu ngoặc vuông thay thế hoạt động của dấu chấm với bất kỳ chuỗi nào:

```javascript
let user = {};

// cài đặt thuộc tính
user["likes birds"] = true;

// lấy giá trị thuộc tính
console.log(user["likes birds"]); // true

// xóa
delete user["likes birds"];
```

Dấu ngoặc vuông cũng cung cấp cách lấy tên thuộc tính là kết quả của bất kỳ biểu thức nào:

```javascript
let key = "likes birds";

// giống như user["likes birds"] = true;
user[key] = true;
```

Ở đây, biến `key` có thể được tính toán tại thời điểm chạy hoặc phụ thuộc vào đầu vào của người dùng. Và sau đó chúng ta sử dụng nó để truy cập thuộc tính. Điều đó mang lại cho chúng ta rất nhiều sự linh hoạt.

Ví dụ:

```javascript
let user = {
    name: "John",
    age: 30,
};

let key = prompt("What do you want to know about the user?", "name");

// truy cập bởi biến key
console.log(user[key]); // John (nếu nhập "name")
```

Không thể sử dụng ký hiệu dấu chấm theo cách tương tự:

```javascript
let user = {
    name: "John",
    age: 30,
};

let key = "name";
console.log(user.key); // undefined
```

### Thuộc tính được tính toán

Chúng ta có thể sử dụng dấu ngoặc vuông trong một đối tượng theo nghĩa đen, khi tạo một đối tượng. Đó được gọi là *thuộc tính được tính toán*.

Ví dụ:

```javascript
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
    [fruit]: 5, // tên thuộc tính được lấy tử biến fruit
};

console.log(bag.apple); // 5 nếu fruit="apple"
```

Về cơ bản nó hoạt động như:

```javascript
let fruit = prompt("Which fruit to buy?", "apple")
let bag = {};

bag[fruit] = 5;
```

...nhưng trông đẹp hơn.

Chúng ta có thể sử dụng các biểu thức phức tạp hơn bên trong dấu ngoặc vuông:

```javascript
let fruit = "apple";

let bag = {
    [fruit + 'Computers']: 5  // bag.appleComputers = 5
};
```

Dấu ngoặc vuông mạnh hơn nhiều so với dấu chấm. Chúng cho phép bất kỳ tên thuộc tính và biến nào. Nhưng chúng cũng khó viết hơn.

Vì vậy, hầu hết thời gian, khi tên thuộc tính được biết trước và đơn giản, dấu chấm được ưu tiên sử dụng. Và nếu chúng ta cần một cái gì đó phức tạp hơn, thì chúng ta chuyển sang dấu ngoặc vuông.

## Giá trị thuộc tính viết tắt

Trong các mã thực tế, chúng ta thường sử dụng các biến hiện có làm tên cho thuộc tính.

Ví dụ:

```javascript
function makeUser(name, age) {
    return {
        name: name,
        age: age,
        // ...các thuộc tính khác
    };
}

let user = makeUser("John", 30);
console.log(user.name); // John
```

Thay vì `name: name` chúng ta chỉ cần viết `name`, như thế này:

```javascript
function makeUser(name, age) {
    return {
        name, // giống như name: name
        age,  // giống như age: age
    };
}
```

## Tên thuộc tính có thể giống từ khóa

Không giống tên biến, tên thuộc tính có thể trùng với từ khóa:

```javascript
// các thuộc tính này hợp lệ
let obj = {
    for: 1,
    let: 2,
    return: 3
};

console.log(obj.for + obj.let + obj.return); // 6
```

> **Tên thuộc tính luôn là một chuỗi**
> Ví dụ số `0` trở thành chuỗi `"0"` khi được sử dụng làm khóa cho thuộc tính:
> ```javascript
> let obj = {
>   0: "test" // giống như "0": "test"
> };
> ```

## Toán tử `in`

Toán tử `in` dùng để kiểm tra sự tồn tại của thuộc tính trong đối tượng.

Cú pháp là:

```javascript
"key" in object
```

Ví dụ:

```javascript
let user = { name: "John", age: 30 };

console.log("age" in user); // true
console.log("blabla" in user); // false
```

> **Khi truy cập các thuộc tính không tồn tại, giá trị thu được là `undefined`**
> Nó khác với trường hợp một thuộc tính có tồn tại nhưng mang giá trị `undefined`.
> ```javascript
> let obj = {
>   test: undefined
> };
> console.log(obj.test); // undefined
> console.log(obj.blabla); // undefined
> console.log("test" in obj); // true
> console.log("blabla" in obj); //false
> ```

## Vòng lặp `for..in`

Để lặp qua các khóa của các thuộc tính trong một đối tượng, chúng ta có thể sử dụng vòng lặp `for..in`.

Cú pháp:

```javascript
for (key in object) {
    // lặp lại với một khóa của các thuộc tính của object
}
```

Ví dụ, hãy xuất tất cả các thuộc tính của `user`:

```javascript
let user = {
    name: "John",
    age: 30,
    isAdmin: true,
};

for (let key in user) {
    // các khóa
    console.log(key); // name, age, isAdmin

    // các giá trị
    console.log(user[key]); // John, 30, true
}
```
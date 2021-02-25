# Hàm tạo và toán tử "new"

Cú pháp `{...}` cho một ta tạo một đối tượng. Nhưng thường thì chúng ta cần tạo nhiều đối tượng giống nhau, như tạo nhiều người dùng hoặc nhiều mục trong menu...

Điều đó có thể thực hiện được bằng cách sử dụng các hàm khởi tạo (*constructor*), gọi tắt là *hàm tạo* và toán tử "new".

## Hàm tạo

Về mặt kỹ thuật, hàm tạo là các hàm thông thường. Tuy nhiên, có hai quy ước:

- Chúng được đặt tên bằng chữ cái in hoa trước mỗi từ.
- Chúng chỉ nên được gọi với toán tử `new`.

Ví dụ:

```javascript
function User(name) {
    this.name = name;
    this.isAdmin = false;
}

let user = new User("Jack");

console.log(user.name); // Jack
console.log(user.isAdmin); // false
```

Khi một hàm được thực thi với `new`, nó sẽ thực hiện các bước sau:

1. Một đối tượng trống được tạo mới và gán cho `this`.
2. Phần thân hàm được thực thi. Thông thường nó sẽ sửa đổi `this`, bổ sung các thuộc tính mới cho nó.
3. Giá trị `this` cuối cùng được trả về.

Nói cách khác `new User(...)` làm một cái gì đó như:

```javascript
function User(name) {
    // this = {}; (thực hiện ngầm)

    // thêm thuộc tính tới this
    this.name = name;
    this.isAdmin = false;

    // trả về this
    return this;
}
```

Vì vậy, `let user = new User("Jack")` cho kết quả tương tự như:

```javascript
let user = {
    name: "Jack",
    isAdmin: false
}
```

Bây giờ, nếu chúng ta muốn tạo một người dùng khác, chúng ta có thể gọi `new User("Ann")`, `new User("Alice")`... Ngắn hơn nhiều so với việc sử dụng `{...}` nhiều lần, và cũng dễ đọc hơn.

Đó là mục đích chính của các hàm tạo - để triển khai mã tạo đối tượng có thể tái sử dụng.

Hãy lưu ý một lần nữa - về mặt kỹ thuật, bất kỳ hàm nào cũng có thể được sử dụng như một hàm tạo. Đó là: có thể chạy bất cứ hàm nào với `new` và nó sẽ thực thi thuật toán trên. Viết hoa chữ cái đầu tiên của mỗi từ, chỉ là một quy ước chung, phân biệt một hàm tạo (được chạy với `new`) với một hàm bình thường.

## new.target

Bên trong một hàm, chúng ta có thể kiểm tra nó được chạy với toán tử `new` hay không, bằng cách sử dụng một thuộc tính đặc biệt là `new.target`.

Nó là `undefined` với cách gọi hàm thông thường và bằng chính hàm này nếu được gọi bằng `new`:

```javascript
function User() {
    console.log(new.target);
}

// gọi không qua "new"
User(); // undefined

// gọi thông qua "new"
new User(); // function User {...}
```

Nhờ `new.target` ta có thể viết một hàm chỉ thực hiện chức năng hàm tạo bất kể gọi có hay không có `new`:

```javascript
function User(name) {
    if (!new.target) { // nếu bạn chạy tôi không dùng new
        return new User(name);
    }

    this.name = name;
}

let john = User("John");
console.log(john.name); // John
```

Cách sử dụng này đôi khi được sử dụng trong các thư viện để làm cho cú pháp linh hoạt hơn. Vì vậy, mọi người có thể gọi hàm có hoặc không có `new`, và nó vẫn hoạt động.

Mặc dù vậy, có lẽ đây không phải là một điều tốt để sử dụng ở mọi nơi, bởi vì việc bỏ qua `new` làm cho mã ít rõ ràng hơn một chút. Với `new`, tất cả chúng ta đều biết rằng mình đang tạo ra một đối tượng.

## Giá trị trả về của hàm tạo

Thông thường, các hàm tạo không có `return`. Nhiệm vụ của chúng là thay đổi `this` và `this` tự động trở thành kết quả trả về.

Nhưng nếu sử dụng `return`, thì quy tắc rất đơn giản, như sau:

- Nếu `return` trả về một đối tượng, thì đối tượng này được trả về thay cho `this`.
- Nếu `return` trả về một giá trị kiểu cơ sở, giá trị cơ sở này bị bỏ qua, `this` được trả về thay cho nó.

Nói cách khác, `return` với một đối tượng sẽ trả về đối tượng đó, trong khi tất cả các trường hợp khác, `this` được trả về.

Ví dụ:

```javascript
function BigUser() {
    this.name = "John";

    return { name: "Godzilla" };  // <-- trả về đối tượng này
}

console.log(new BigUser().name); // Godzilla
```

Và đây là ví dụ với `return` trống (hoặc có thể trả về một giá trị cơ sở như chuỗi, số...):

```javascript
function SmallUser() {
    this.name = "John";

    return; // <-- trả về this
}

console.log(new SmallUser().name); // John
```

> **Bỏ qua dấu ngoặc đơn**
>
> Nếu không có đối số, ta có thể bỏ đi dấu ngoặc đơn trống:
> ```javascript
> let user = new User; // <-- không có dấu ngoặc đơn
> // giống như
> let user = new User();
> ```

## Tạo phương thức bằng hàm tạo

Chúng ta có thể thêm vào `this` không chỉ các thuộc tính, mà còn cả các phương thức.

Ví dụ: `new User(name)` bên dưới tạo một đối tượng mới với thuộc tính `name` và phương thức `sayHi`:

```javascript
function User(name) {
    this.name = name;

    this.sayHi = function() {
        console.log("My name is: " + this.name);
    };
}

let john = new User("John");

john.sayHi(); // My name is: John
```
# Chuyển đổi đối tượng thành các kiểu cơ sở

Điều gì xảy ra khi ta cộng hai đối tượng: `obj1 + obj2`, trừ hai đối tượng: `obj1 - obj2`, hoặc in ra bằng cách sử dụng `console.log(obj)`?

Trong trường hợp đó, các đối tượng được tự động chuyển đổi thành kiểu cơ sở, và sau đó phép toán được thực hiện.

Đối với chuyển đổi thành kiểu lôgic, mọi đối tượng trở thành `true`.

Đối tượng được chuyển đổi thành số khi thực hiện các phép toán số học trên đối tượng.

Đối tượng được chuyển đổi thành chuỗi khi một hàm hay toán tử cần một giá trị chuỗi để hoạt động.

## Nguyên tắc chuyển đổi chung

**Để thực hiện chuyển đổi đối tượng sang kiểu số hoặc chuỗi, JavaScript cố gắng tìm và gọi ba phương thức:**

1. Gọi `obj[Symbol.toPrimitive](hint)` - phương thức `Symbol.toPrimitive` (là một symbol hệ thống), nếu phương thức đó được định nghĩa. `hint` là gợi ý chuyển đổi, có thể là:
   1. `"string"`: trong những tình huống đối tượng phải được chuyển thành chuỗi.
   2. `"number"`: trong những tình huống đối tượng phải được chuyển thành số.
   3. `"default"`: trong những tình huống không rõ ràng.
2. Nếu không có phương thức `Symbol.toPrimitive` và `hint` là `"string"` thì:
   1. Gọi `obj.toString()` nếu nó được định nghĩa
   2. Gọi `obj.valueOf()` nếu `obj.toString()` không được định nghĩa.
3. Nếu không có phương thức `Symbol.toPrimitive` là `hint` là `"number"` hoặc `"default"` thì:
   1. Gọi `obj.valueOf()` nếu nó được định nghĩa
   2. Gọi `obj.toString()` nếu `obj.valueOf()` không được định nghĩa.

**Tóm lại**

- Nếu `hint` là `"string"` thì thứ tự ưu tiên gọi như sau:
  1. `obj[Symbol.toPrimitive](hint)`
  2. `obj.toString()`
  3. `obj.valueOf()`
- Nếu `hint` là `"number"` hoặc `"default"` thì thứ tự ưu tiên gọi như sau:
  1. `obj[Symbol.toPrimitive](hint)`
  2. `obj.valueOf()`
  3. `obj.toString()`

## Symbol.toPrimitive

Hãy bắt đầu bằng phương thức đầu tiên. Nó được đặt tên bằng symbol hệ thống `Symbol.toPrimitive`. Nó được định nghĩa như sau:

```javascript
obj[Symbol.toPrimitive] = function(hint) {
    // phải trả về một giá trị kiểu cơ sở
    // hint bằng một trong các giá trị "string", "number", "default"
}
```

Ví dụ:

```javascript
let user = {
    name: "John",
    money: 1000,

    [Symbol.toPrimitive](hint) {
        console.log(`hint: ${hint}`);
        return hint == "string" ? `{name: "${this.name}"}` : this.money;
    }
};

console.log(user); // hint: string -> {name: "John"}
console.log(+user); // hint: number -> 1000
console.log(user + 50); // hint: default -> 1500
```

## toString/valueOf

Phương thức `toString` và `valueOf` có từ rất lâu. Chúng không phải là các symbol, mà là các phương thức có tên là chuỗi "thông thường". Chúng cung cấp cách thức cũ để triển khai chuyển đổi.

Nếu không có `Symbol.toPrimitive` thì JavaScript cố gắng tìm chúng theo thứ tự:
- `toString -> valueOf` nếu `hint` là `"string"`
- `valueOf -> toString` nếu `hint` là `"number"` hoặc `"default"`

Các phương thức này phải trả về một giá trị cơ sở.

Theo mặc định một đối tượng có sẵn phương thức `toString` trả về một chuỗi có dạng `"[object Object]"`, và có sẵn phương thức `valueOf()` trả về chính đối tượng, và do đó sẽ bị bỏ qua. Như vậy, trong mọi trường hợp phương thức `toString` được sử dụng nếu ta không triển khai phiên bản `toString/valueOf` riêng.

```javascript
let user = {name: "John"};

console.log(user); // [object Object]
console.log(user.valueOf() === user);  // true
```

Đây là ví dụ triển khai `toString` và `valueOf` thay vì sử dụng `Symbol.toPrimitive`:

```javascript
let user = {
    name: "John",
    money: 1000,

    // cho hint = "string"
    toString() {
        return `{name: "${this.name}"}`;
    },

    // cho hint = "number" hoặc "default"
    valueOf() {
        return this.money;
    }
};

console.log(user); // toString -> {name: "John"}
console.log(+user); // valueOf -> 1000
console.log(user + 500); // valueOf -> 1500
```

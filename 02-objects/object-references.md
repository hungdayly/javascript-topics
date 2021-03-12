# Tham chiếu

Một trong những điểm khác biệt cơ bản của đối tượng so với các giá trị kiểu cơ sở là các đối tượng được lưu trữ và sao chép dưới dạng các "tham chiếu", trong khi các giá trị cơ sở (chuỗi, số, giá trị lôgic,...) được lưu trữ và sao chép dưới dạng các "giá trị".

Hãy bắt đầu với một giá trị kiểu cơ sở, chẳng hạn như một chuỗi.

Ở đây chúng ta đặt một bản sao của `message` cho `phrase`:

```javascript
let message = "Hello!";
let phrase = message;
```

Kết quả là chúng ta có hai biến độc lập, mỗi biến lưu trữ một chuỗi `"Hello!"`.

Đối tượng không phải như vậy.

**Khi gán một đối tượng cho một biến, biến không lưu trữ đối tượng mà là "địa chỉ" trong bộ nhớ của nó - hay còn gọi là "tham chiếu" tới đối tượng.

Hãy xem một ví dụ về một biến như vậy:

```javascript
let user = {
    name: "John"
};
```

Đối tượng thực sự đang được lưu trữ ở đâu đó trong bộ nhớ, trong khi `user` lưu "tham chiếu" tới đối tượng này.

Chúng ta có thể nghĩa về một biến đối tượng, chẳng hạn `user` như một tờ giấy có ghi địa chỉ đối tượng trên đó.

Khi chúng ta thực hiện các hành động đối với đối tượng, ví dụ: lấy một thuộc tính `user.name`, JavaScript tìm đến địa chỉ đối tượng được lưu trong `user` và thực hiện thao tác trên đối tượng thực.

**Khi một biến đối tượng được sao chép, tham chiếu sẽ được sao chép, nhưng bản thân đối tượng không được sao chép.**

Ví dụ:

```javascript
let user = { name: "John" };

let admin = user;  // sao chép tham chiếu
```

Bây giờ chúng ta có hai biến: `user` và `admin`, cả hai đều lưu trữ tham chiếu đến cùng đối tượng.

Chúng ta có thể sử dụng một trong hai biến này để truy cập và sửa đổi nội dung của đối tượng:

```javascript
let user = { name: "John" };

let admin = user;

admin.name = "Pete";  // thay đổi thông qua biến admin

alert(user.name); // Pete
```

Nó giống như thể chúng ta có một chiếc tủ với hai chìa khóa và sử dụng một trong số chúng (`admin`) để vào đó và thực hiện thay đổi. Sau đó, nếu sau này chúng ta sử dụng một khóa khác (`user`), chúng ta vẫn đang mở cùng một tủ và có thể truy cập nội dung đã thay đổi.

## So sánh hai đối tượng

Hai đối tượng chỉ bằng nhau, nếu chúng chứa cùng một tham chiếu, tới cùng một đối tượng.

Ví dụ, ở đây `a` và `b` tham chiếu cùng một đối tượng, do đó chúng bằng nhau:

```javascript
let a = {};
let b = a; // sao chép tham chiếu

console.log(a == b); // true
console.log(a === b); // true
```

Và ở đây, hai đối tượng độc lập không bằng nhau, mặc dù chúng trông giống nhau (cả hai đều trống):

```javascript
let a = {};
let b = {}; // hai đối tượng độc lập

console.log(a == b); // false
```

Với các so sánh giống như `obj1 > obj2` hoặc so sánh với giá trị cơ sở `obj == 5`, các đối tượng được chuyển đổi thành kiểu cơ sở. Chúng ta sẽ sớm nghiên cứu cách chuyển đổi đối tượng thành kiểu cơ sở, nhưng nói thật là rất hiếm khi ta cần đến những so sánh như vậy - thường chúng xuất hiện do lỗi lập trình.

## Nhân bản và hợp nhất các đối tượng

Sao chép đơn giản không tạo ra một đối tượng mới, chỉ tạo ra một tham chiếu mới.

Nhưng nếu ta cần nhân bản một đối tượng, tạo một bản sao độc lập, một bản sao thì phải làm sao?

JavaScript không hỗ trợ phương pháp có sẵn nào để thực hiện điều này. Tuy nhiên, chúng ta hiếm khi có nhu cầu đó - sao chép các tham chiếu là đủ trong hầu hết thời gian.

Nhưng nếu chúng ta thực sự muốn điều đó, thì chúng ta cần tạo một đối tượng mới và sao chép cấu trúc của đối tượng hiện có bằng cách lặp lại các thuộc tính của nó và sao chép ở mức giá trị cơ sở.

Chẳng hạn:

```javascript
let user = {
    name: "John",
    age: 30,
};

let clone = {}; // đối tượng trống mới

// cùng sao chép tất cả các thuộc tính của user sang clone
for (let key in user) {
    clone[key] = user[key];
}

// giờ clone hoàn toàn độc lập với user và có nội dung giống hệt
clone.name = "Pete"; // thay đổi dữ liệu trong clone

console.log(user.name); // John (user không bị ảnh hưởng)
```

Một phương pháp phổ biến là sử dụng phương thức `Object.assign`.

Cú pháp:

```javascript
Object.assign(dest, [src1, src2, src3...])
```

- `dest`: đối tượng đích
- `src1, ..., srcN` là các đối tượng nguồn
- Nó sao chép tất cả các thuộc tính của tất cả các đối tượng nguồn `src1, ..., srcN` vào `dest`.
- Phương thức này trả về `dest`.

Ta sử dụng `Object.assign` thay cho vòng lặp `for..in` ở trên như sau:

```javascript
let user = {
    name: "John",
    age: 30
};

let clone = Object.assign({}, user);
```

Chúng ta có thể dùng nó để hợp nhất nhiều đối tượng thành một:

```javascript
let user = { name: "John" };

let permission1 = { canView: true };
let permission2 = { canEdit: true };

Object.assign(user, permission1, permission2);

// giờ user = { name: "John", canView: true, canEdit: true }
```

Nếu thuộc tính được sao chép đã tồn tại, nó sẽ bị ghi đè:

```javascript
let user = { name: "John" };

Object.assign(user, { name: "Pete" });

console.log(user.name); // Pete
```

## Nhân bản sâu

Cho đến bây giờ, chúng ta đã giả định rằng tất cả các thuộc tính của `user` có kiểu cơ sở. Nhưng các thuộc tính có thể chứa một tham chiếu tới đối tượng khác. Làm gì với chúng đây?

```javascript
let user = {
    name: "John",
    sizes: {
        height: 182,
        width: 50
    }
};

console.log(user.sizes.height); // 182
```

Bây giờ nếu sao chép `clone.sizes = user.sizes` thì tham chiếu tới đối tượng được sao chép. Vì vậy `clone` và `user` có cùng thuộc tính `sizes`:

```javascript
let user = {
    name: "John",
    sizes: {
        height: 182,
        width: 50
    }
};

let clone = Object.assign({}, user);

console.log(usre.sizes === clone.sizes); //  true

user.sizes.width++;
console.log(clone.sizes.width); // 51
```

Để khắc phục, chúng ta nên sử dụng một vòng lặp để kiểm tra từng giá trị `user[key]` và nếu đó là đối tượng thì lại tái tạo cấu trúc của nó. Đó được gọi là "nhân bản sâu".

Chúng ta có thể dùng đệ quy để thực hiện nó. Hoặc sử dụng một cách triển khai hiện có, chẳng hạn như [_.cloneDeep](https://lodash.com/docs#cloneDeep) từ thư viện [lodash](https://lodash.com/).

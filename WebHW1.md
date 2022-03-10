# Ex1
```Javascript
const obj1 = { x: 20, y: 30 };

function cloneDeep(obj) {
    return {...obj}
}
const obj2 = cloneDeep(obj1)
obj2.x = 10

console.log("obj1: ") 
console.log(obj1) // {x: 20, y: 30}
console.log("obj2: ")
console.log(obj2) // {x: 10, y: 30}
```

# Ex2
```Javascript
const macbooks = ['macbook2015', { model: 'macbook2014' }, 'macbook2017'];
const apples = [...macbooks];
apples[0] = 'air';
apples[1].model = 'm1';

console.log(macbooks)
console.log(apples)
```
Kết quả của macbook vẫn là array gồm 3 phần tử, tuy nhiên phần tử thứ 2 là m1 thay vì macbook2014. Đầu tiên, apples là 1 array gồm 3 phần tử với phần tử thứ 2 là một object, object đó và object ở array macbooks đều trỏ thẳng vào chung 1 ô nhớ và có chung một địa chỉ. Vì vậy, khi gọi apples[1].model = 'm1', trường model của object đó được thay đổi thành m1 và m1 sẽ được update tại cả 2 array.

String là kiểu dữ liệu nguyên thủy của javascript (khác với Java khi mà trong Java bản thân String là 1 Object). Tại vị trí đầu tiên của array apple trỏ vào một dãy bit thể hiện cho giá trị 'macbook2015', nên khi gán giá trị mới là 'air' thì đơn thuần dãy bit đó được thay đổi để thể hiện giá trị 'air'. Chuỗi macbooks  không có sự thay đổi gì vì tại vị trí đầu của macbooks đang trỏ vào một chuỗi bit thể hiện cho giá trị macbook2015.

```Javascript
# Ex3
var text = 'outside';
function show() {
  console.log(text) //1
  var text = 'inside';
}
```
Đây là cơ chế variable hoisting trong javascript khi mà Javascript tạo sẵn một ô nhớ cho một biến trước khi biến đó được khởi tạo và gán giá trị. Lí do vì sao text k chứa giá trị 'outside' thì bản thân em nghĩ rằng vì javascript phát hiện ra biến text đang được khởi tạo và gán giá trị trong cùng 1 function, hay nói cách khác là javascript đang ưu tiên function scope hơn là global scope nên biến text được ưu tiên áp dụng cơ chế hoisting.

```Javascript
# Ex4
let arr = [1, 2, 3, 4, 5, 6, 7];

function inBetween(num1, num2){
    return function(result){
        return result >= num1 && result <= num2
    }
}

function inArray(arr){
    return function(result){
        return arr.includes(result);
    }
}

alert( arr.filter(inBetween(3, 6)) ); // 3,4,5,6
alert( arr.filter(inArray([1, 2, 10])) ); // 1,2
```

# Ex5
```Javascript
function Counter() {
  let count = 0;

  this.up = function() {
    return ++count;
  };
  this.down = function() {
    return --count;
  };
}

let counter = new Counter();

alert( counter.up() ); // ?
alert( counter.up() ); // ?
alert( counter.down() ); // ?
```
Kết quả: 1, 2, 1
Khi counter.up() được gọi thì function bên trong function counter() được thực thi, tăng biến count lên 1 đơn vị trước khi in ra. Ngược lại, khi counter.down() được gọi thì biến count được giảm 1 đơn vị trước khi được in ra. Biến count của hàm counter() có thể được access từ các hàm bên trong.

# Ex6
```Javascript
console.log("hello");

setTimeout(() => console.log("world"), 0);

console.log("hi");
```
Biến hello luôn được in ra đầu tiên vì Javascript là ngôn ngữ đơn luồng nên khi gặp lệnh in hello thì Javascript sẽ thực thi đầu tiên. Khi hàm setTimeout() được gọi, Javascript sẽ đẩy code của setTimeout() sang callback queue kể cả khi thời gian là 0ms thì javascript vẫn sẽ thực thi điều đó. Event loop lúc đó sẽ chạy liên tục và kiểm tra xem trên main stack có còn lệnh nào chưa được thực thi hay không, nếu còn thì main stack sẽ thực thi chúng. Chính vì vậy, "hi" được in ra tiếp theo. Sau khi in "hi" ra console thì main stack trở nên empty, và main stack lúc đó mới kiểm tra sang callback queue. Callback queue đẩy lệnh console.log("world") về cho main stack và khi đó world mới được in ra console cho người dùng.

# WebHW1
#H1
const obj1 = { x: 20, y: 30 };

function cloneDeep(obj) {
    return {...obj}
}
const obj2 = cloneDeep(obj1)
obj2.x = 10

console.log("obj1: ")
console.log(obj1)
console.log("obj2: ")
console.log(obj2)

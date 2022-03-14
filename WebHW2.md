# Ex 1
```Javascript
const fs = require('fs');
fs.writeFile('numbers.txt', '1 8 5 7 2', (err) => {
    if(err){
        console.log(err);
    }
});
```
# Ex 2
```Javascript
const writeFile = (path, data) => {
    return new Promise((reject, resolve) => {
        fs.writeFile(path, data, (err) =>{
            if(err){
                return reject("err", err);
            }
            resolve("ok");
        })
    })
  }
  
const writeFileToDisk = async (path, data) => {
    try {
      const isSuccess = await writeFile(path, data);
      console.log(isSuccess) // true
    } catch (err) {
      console.log(err) // 'Lỗi'
    }
  }

writeFileToDisk('numbers2.txt', '1 0 0 1 5 10')
```
# Ex 3
```Javascript
fs.readFile('numbers.txt', 'utf-8', (err, data) => {
    let count = 0;
    if(err){
        console.log(err);
    }else{
        data = data.split(' ');
        for(let letter of data){
            if(parseInt(letter) % 2 != 0){
                count++;
            };
        }
    }
    fs.writeFile('numbers.txt', count.toString(), (err) => {
        if(err){
            console.log(err);
        }
    })
})
```
# Ex 4
```Javascript
async function wait(sec) {
    await new Promise((resolve) => {
        setTimeout(resolve, sec);
    });
}

async function go() {
  console.log('Starting');
  await wait(2000);
  console.log('running');
  await wait(200);
  console.log('ending');
}

go();
```

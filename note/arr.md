# 1.找出数组 arr 中重复出现过的元素
    function duplicates(arr) {
    var dupArr = [];
    arr.forEach(function(item){
        if(arr.indexOf(item) != arr.lastIndexOf(item) && dupArr.indexOf(item) == -1){
            dupArr.push(item)
        }
    })
    return dupArr;
    }
# 2.数组转字符串
    let arr = [1,2,3,4];
    let arr = str.join(''); //1234
# 3.字符串转化成数组
    let str = 'hello';
    let arr = str.split(''); // ['h','e','l','l','o']
# 4.数组的浅拷贝
 ## -1 slice
    arr.slice();
 ## -2 concat
    arr.concat();
 ## -3 JSON
    JSON.parse(JSON.stringify(arr))
 ## -4 ...
    let arr2 = [...arr]
 ## -5 Array.from()
    let arr2 = Array.from(arr)
 ## -6 push 
    let arr1 = [4,4,5,5,6]
    let newArr = [];
    Array.prototype.push.applay(newArr,arr1);
    newArr //[4,4,5,5,6]
 ## -7 map
    let arr2 = arr.map(()=>{return item})
# 一.五大基本数据类型
 ## 1.Undefined
    -1 声明但未赋值的变量
    -2 不存在的对象属性
    -3 未声明的变量 
        console.log(a) //a is not defined
        console.log(typeof a) // undefined
 ## 2.Null
    -1 typeof null //'object'
    -2 null == undefined //true
    -3 
 ## 3.Number
    -1 判断变量是否为数字
        isNaN()
        但是isNaN又一个缺陷：未传值时被当作0
        function isNumber(str){
            console.log(isNaN(str))
        }
        isNumber() //true
        所以应该为 typeof(str) === 'number' && !isNaN(str)
 ## 4.String
 ## 5.Boolean
# 二，JS 的非空判断
    //空引用 空字符串 空输入
    if(typeof(s) != 'undefined' && s != null && s.trim() != "")
# 三，typeof的返回值
    共有6个：
    'undefined'
    'string'
    'boolean'
    'number'
    'object'
    'function'
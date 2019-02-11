# 1.定时器函数
    setInterval 和 setTimeout 的区别：
    setInterval:函数A(执行时间)+间隔=1s —— 函数B(执行时间)+间隔=1s —— 函数C(执行时间)+间隔=1s
    setTimeout:函数A(执行) —— 1s —— 函数B(执行) —— 1s //防止连续执行函数
    一般用setTimeout()代替setInterval()
    setTimeout(function show(){
        //执行的函数体
        setTimeout(show,1000)
    },1000)
    -1 this指向：非严格模式指向window,严格模式指向undefined
    -2 
# 2.递归调用
    在调用递归函数时，使用函数表达式
# 3.闭包 
    闭包连接：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Closures
    在函数的外部获得函数内部变量。实现的方法：在函数内部返回函数
# 4.arguments
    arguments 是一个对应于传递给函数的参数的类数组对象。
    arguments对象不是一个 Array 。它类似于Array，但除了length属性和索引元素之外没有任何Array属性。例如，它没有 pop 方法。但是它可以被转换为一个真正的Array：[...arguments] 或者 Array.prototype.slice.call(arguments)
# 5.箭头函数的this指向
    var x=11;
    var obj={
     x:22,
     say:()=>{
       console.log(this.x);
     }
    }
    obj.say(); //11

    思路：箭头函数的this绑定的是父执行上下文；上例中箭头函数与say平级，箭头函数所在的对象是obj,obj所在的父执行上下文是window,因此this.x指的是window.x

    意义：由于this在箭头函数中已经按照词法作用域绑定了，所以，用call()或者apply()调用箭头函数时，无法对this进行绑定，即传入的第一个参数被忽略：

    var a=11
    function test1(){
      this.a=22;
      let b=()=>{console.log(this.a)};
      b();
    }
    var x=new test1(); //22

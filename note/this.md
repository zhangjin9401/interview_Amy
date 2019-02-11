哎呀妈呀，脑阔疼！！！！！
参考链接：https://segmentfault.com/a/1190000004581945
    https://segmentfault.com/a/1190000013045741
# 一，call()和apply()
 ## 1.改变函数内部this指向，即实现继承；
    function animal(name,food) {
        this.name = name,
        this.food = food,
        this.say = function() {
            console.log(name +" likes " + this.food + '.');
        }
    }

    function rabbit(name,food) {
       animal.call(this,name,food); //继承了animal的所有属性和方法；
    }

    var Judy = new rabbit('Judy','carrot');

    Judy.say();// >>> Judy likes carrot.

    call()的参数：
        第一个是一个对象，这个对象将代替Function类里原本的this对象，我们传入的是this，记住，这个this在rabbit函数里指的是未来将要实例化这个函数的对象，当声明了Judy的时候，这个this指的就是Judy。
        除了第一个参数，后面所有的参数都是传给父函数本身使用的参数
    
    
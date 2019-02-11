# 一，Vue
 ## 1.vue的核心：
    声明式渲染：用简洁的模版语法声明式地将数据渲染进DOM系统；
 ## 2.系统是响应式的：
    验证方法：打开chrome控制台，修改app.message,发现数据相应更新；
 ## 3.Vue组件：
    -1 Vue组件的实质就是一个拥有预定义选项的Vue实例；
    -2 组件是可复用的Vue实例，有一个名字(推荐字母全小写且包含连接符)，可以在一个new Vue创建的根实例中，将组件作为自定义元素使用；
    -3 组件的data选项必须是一个函数，每个实例可以维护一份被返回对象的独立拷贝；
    -4 全局注册：Vue.component() // 局部注册：components；全局注册组件的行为只能在根实例创建之前完成；
 ## 4.父子组件的传值：
    -1 父传子：props;
    -2 子改父：this.$emit();
 ## 5.非父子组件传值：
    -1 通过第三方变量，达到改变值的目的(最好的方式是：使用vuex)；
    -2 新建busEvent.js ,导出一个Vue 实例；
        import Vue from 'vue';
        let busEvent = new Vue();
        export default busEvent;
    -3 在组件A中，指定事件：
        handleClick(){
            busEvent.$emit('addCount');
        }
    -3 在组件B中，监听事件:
        mounted(){
            busEvent.$on('addCount',()=>{
                this.count+=1;
            })
        },
 ## 6.Vue的方法：
    -1 Vue.component()：会隐式调用Vue.extend();
    -2 Vue.component('my-name',myOptions) == Vue.component('my-name',Vue.extend(myOptions)) == Vue.component('my-name',myExtend);
    -3 Vue.extend():返回一个扩展实例的构造器：
        1.let baseOptions = {

        }
 ## 7，props
    -1 如果 prop 是一个对象或数组，在子组件内部改变它会影响父组件的状态。
    -2 必须在子组件修改prop时，用Object.assign({},prop),返回一个全新的对象。或者自己用js做一个深度拷贝器；
 ## 8.v-model
    -1 v-model是一个语法糖，可以实现 <input :value="message" @input="message = $event.target.value"/>
 ## 9.插槽slot分发内容
    -1 普通插槽
    -2 具名插槽
    -3 作用域插槽
        使用场景：官方的例子，一个列表，不同的场景有不同的具体展示方式，但数据是相同的。这时可以把列表定义成抽象的，类似interface，具体的implement在使用的时候(parent中)确定。
        <list-comp>
            <ul>
                <slot name="item" v-for="item in items" :text="item.text">
                    <!-- 具体的列表展示形式在parent中使用slot -->
                </slot>
            </ul>
        <list-comp>
 ## 10.动态组件
    -1 通过使用保留的 <component> 元素，并对其 is 特性进行动态绑定，你可以在同一个挂载点动态切换多个组件：
    -2 如果把切换出去的组件保留在内存中，可以保留它的状态或避免重新渲染。为此可以添加一个 keep-alive 指令参数：
        <keep-alive>
            <component :is="isCurrent"></component>
        </keep-alive>
 ## 11.杂项
    -1 refs:仅仅是一个直接操作子组件的应急方案——应当避免在模板或计算属性中使用 $refs。
        <child-component refs="child"></child-component>
 ## 12.计算属性缓存vs方法
    -1 计算属性当依赖改变时才重新计算
 ## 13.计算属性vs监听watch
    -1 通常使用计算属性优于命令式的watch
    -2 计算属性默认只有getter,自己可以根据需要提供setter
        fullName:{
            get(){
                return this.firstName +' '+this.lastName;
            },
            set(newVal){
                let names = newVal.split(' ');
                this.firstName = names[0];
                this.lastName = names[1];
            }
        }
    -3 普通属性的监听
        watch: {
            fiestName(newVal,oldVal){
                console.log(newVal)
            }
        }
    -4 对象的监听
        watch: {
            searchInputValue:{
                handler: 'fetchPostList', //处理的方法
                deep:true,//深层遍历
                immediate: true //组件创建之处立即执行
            }
        }
        涉及对象的属性还可以用 
        'Person.name':function(newVal,oldVal){}
 ## 14.基础
    -1 vue实例提供和暴露一些属性和方法，以$开头，用以区分用户定义的属性；
 ## 15.生命周期
    -1 生命周期钩子函数禁用箭头函数；
    -2 beforeCreate: 实例初始化之后，数据观测 (data observer) 和 event/watcher 事件配置之前被调用。
        beforeCreate: function () {
            console.group('===== beforeCreate 创建前==== =====');
            console.log("%c%s", "color:red", "el     : " + this.$el); //undefined
            console.log("%c%s", "color:red", "data   : " + this.$data); //undefined 
            console.log("%c%s", "color:red", "message: " + this.message)//undefined
            console.groupEnd();
        },
        created: 实例创建完成后被立即调用。在这一步，实例已完成以下的配置：数据观测 (data observer)，属性和方法的运算，watch/event 事件回调。然而，挂载阶段还没开始，$el 属性目前不可见。
        created: function () {
            console.group('===== created 创建完毕==== =====');
            console.log("%c%s", "color:red", "el     : " + this.$el); //undefined
            console.log("%c%s", "color:red", "data   : " + this.$data); //已被初始化 
            console.log("%c%s", "color:red", "message: " + this.message); //已被初始化
            console.groupEnd();
        },
        beforeMount: 在挂载开始之前被调用：相关的 render 函数首次被调用。
        mounted: el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。（不会承诺所有的子组件也都一起被挂载。如果你希望等到整个视图都渲染完毕，可以用 vm.$nextTick 替换掉 mounted ）;
        beforeUpdate: 数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前;
        updated: 组件 DOM 已经更新（ 不会承诺所有的子组件也都一起被重绘）;
        actived: keep-alive 组件激活时调用。
        deactived: keep-alive 组件停用时调用。
        beforeDestory: 实例销毁之前调用。在这一步，实例仍然完全可用。
        destroyed: Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。
 ## 16.Vue.nextTick
    描述： 在下次 DOM 更新循环结束之后执行延迟回调。在修改数据之后立即使用这个方法，获取更新后的 DOM。vue 官网官方提供了一种写法， vm.$nextTick，用 this 自动绑定到调用它的实例上
    created() {
      setTimeout(() => {
        this.number = 100
        this.$nextTick(() => {
          console.log('nextTick', document.getElementsByTagName('p')[0])
        })
      }, 100)
    }
    在什么时候用？
    为什么在 Vue 生命周期的 created() 钩子函数进行的 DOM 操作一定要放在 Vue.nextTick() 的回调函数中？
    -1 原因是在 created() 钩子函数执行的时候 DOM 其实并未进行任何渲染，而此时进行 DOM 操作无异于徒劳，所以此处一定要将 DOM 操作的 js 代码放进 Vue.nextTick()的回调函数中。与之对应的就是 mounted 钩子函数，因为该钩子函数执行时所有的 DOM 挂载和渲染都已完成，此时在该钩子函数中进行任何 DOM 操作都不会有问题 。
    -2 在数据变化后要执行的某个操作，而这个操作需要使用随数据改变而改变的 DOM 结构的时候，这个操作都应该放进 Vue.nextTick() 的回调函数中。
    
# 二，数组的方法
 ## 1.push
        返回新增的
# 三，对象的方法
 ## 1.
# 四，引用类型
 ## （一）Object
  ### 1.对象的深拷贝
    -1.for循环
    -2.Object.assign({},obj)
    -3.JSON.parse(JSON.stringify(obj))
    -4.es6的扩展运算符...
 ## （二）Array
  ### 1. 数组的深拷贝
    -1.简单实现：for循环
    -2.基本数据类型的数组：slice,concat
    -3.含有引用类型值的：JSON.parse(JSON.stringify(Arr))
    -4.es6的扩展运算符...

# 五，ES6
 ## 1.let
    -1 块级作用域；
    -2 不允许重复声明（报错）；
    -3 没有声明提升；
    -4 只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。
    在块级作用域里声明函数的规则：
        -1 允许在块级作用域内声明函数。
        -2 函数声明类似于var，即会提升到全局作用域或函数作用域的头部。
        -3 同时，函数声明还会提升到所在的块级作用域的头部。
        -4 考虑到环境导致的行为差异太大，应该避免在块级作用域内声明函数。如果确实需要，也应该写成函数表达式，而不是函数声明语句。
 ## 2.const
    -1 const声明的变量不得改变值，这意味着，const一旦声明变量，就必须立即初始化，不能留到以后赋值。
    -2 只在所声明的块级作用域有效。
    -3 不可以重复声明。
    -4 尽量不用const声明对象。
 ## 3.数组
    扩展运算符的应用
    -1 复制数组
    -2 合并数组
    -3 解构赋值
    -4 将字符串转为真正的数组
 Array.from():将类似数组的数据转为真正的数组，可以接收第二个参数为函数；
 Array.of():将一组值，转为数组；
 copyWithin(target,start,end);
 find(callback):找出第一个符合条件的数组成员；
 findIndex(callback):返回第一个符合条件的数组成员的位置；
 fill(target,start,end):填充数组；
 entries()，keys()和values()——用于遍历数组，返回的对象用for...of进行遍历；
 includes(): 方法返回一个布尔值，表示某个数组是否包含给定的值;
 返回新数组：
    flat：用于将嵌套数组拉平；
    flatMap()方法对原数组的每个成员执行一个函数，然后对返回值组成的数组执行flat()方法。该方法返回一个新数组，不改变原数组；

# 六，this的指向
 ## 1.对象里的调用：指向调用这个方法的对象
    var obj = {
        name:"bob",
        sayHello :sayHello
    }

    function sayHello() {
        console.log(this.name);
    }

    obj.sayHello(); 
 ## 2.箭头函数的this:
    function foo(){
        let _this = this;
        setTimeout(function(){
            console.log(_this)
        },1000)
    }

    即等于
    function foo(){
        setTimeout(()=>{console.log(this)},1000)
    }

    var obj = {
        name:'jin',
        say:()=>{
            console.log(this.name)
        }
    }
    obj.say() //undefined
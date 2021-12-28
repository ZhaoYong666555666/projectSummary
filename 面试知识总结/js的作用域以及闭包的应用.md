## js的作用域

###作用域说明：一般理解指一个变量的作用范围
1.全局作用域
（1）全局作用域在页面打开的时候创建，页面关闭时被销毁
（2）编写在script标签中的变量和函数，作用域为全局，在页面任意位置都可以访问到
（3）在全局作用域中有全局对象window，代表一个浏览器窗口，由浏览器创建，可以直接调用
（4）全局作用域中声明的变量和函数会作为window对象的属性和方法保存

2.函数作用域
（1）调用函数时，函数作用域被创建，函数执行完毕，函数作用域被销毁
（2）每调用一次函数就会创建一个新的函数作用域，他们之间是相互独立的
（3）在函数作用域中可以访问到的全局作用域的变量，在函数外是无法访问的
（4）在函数作用域中访问变量，函数时，会先在自身作用域中寻找，若没有找到，则会到函数上一级作用域中寻找
，一直到全局作用域

```javascript
function get(){
    var a = 1;
    a++;
    console.log(a);
}
// 函数创建作用域生成，执行完毕就销毁
get();
get();
```

###作用域的深层次理解
+执行期的上下文
-当函数代码执行的前期，会创建一个执行期上下文的内部对象 AO（作用域）
-这个内部的函数时预编译的时候创建出来的，因为当函数被调用的时候，会先进行预编译
-在全局代码执行的前期会创建一个执行期的上下文的对象GO

###函数作用域的预编译
1.创建AO对象 AO{}
2.找形参和变量声明 将变量和形参名 当做 AO对象的属性名 值作为undefined
3.实参形参相统一
4.在函数体里面找函数声明 值赋予函数体
###全局作用域的预编译
1.创建 GO对象
2.找变量声明 将变量名作为GO对象的属性名 值是undefined
3.找函数声明 值赋予函数体

```javascript
// 阿里面试题
function fn(a,c){
    console.log(a); //function a(){}
    var a = 123;
    console.log(a); //123
    console.log(c); //function c(){}
    function a(){}  //这样的叫做函数声明
    if(false){
        var d = 678;
    }
    console.log(d); //undefined
    console.log(b); //undefined
    var b = function(){}   //这样的叫做函数表达式
    console.log(b); //function (){}
    function c(){}
    console.log(c); //function c(){}
}
fn(1,2);
// 通过预编译
// AO = {
//     a:undefined 1 123 function a(){},
//     c:undefined 2 function c(){},
//     b:undefined function(){},
//     d:undefined, 
// }

```

###闭包的经典应用
-闭包产生的根本原因在于作用域链
####闭包的经典案例

#防抖函数
+当持续触发事件 一定时间内没有再触发事件 时间处理函数才会执行一次
如果设定的时间到来之前 有一次触发了时间 就重新开始延时
>关键词：触发事件 一段时间内 没有出发 实践之星 肯定是定时器
>（在设定的时间内 又一次触发了事件 重新开始延时 代表的就是重新开始定时器）
>（那么意味着上一次还没有结束的定时器要清除掉 重新开始）
```javascript
// 防抖
function debounce(fun,delay){
    let timer;
    return function(args){
        clearInterval(timer);
        timer = setTimeout(function(){
            fun(args);
        },delay)
    }
}

function inputFun(value){
    console.log(`你输出的结果是${value}`);
}

const input = document.getElementById('input');
const debounceInput = debounce(inputFun,1000);
input.addEventListener('keyup',function(e){
    debounceInput(e.target.value);
})
```



```javascript
// 节流
function throttle(func, wait) {
    let timerOut;
    return function () {
        if (!timerOut) {
            timerOut = setTimeout(function () {
                timerOut = null;
                func();
            }, wait);
        }
    }
}

function handle() {
    console.log(Math.random());
}

document.getElementById('button').onclick = throttle(handle, 1000);
```

##防抖函数的实际应用
-使用echarts时，改变浏览器宽度时，希望重新渲染，echarts的图像，
可以使用次函数，提升性能（虽然echarts里有自带的resize函数）
-典型的案例1、就是输入搜索：输入结束后n秒才进行搜索请求，n秒内又输入
的内容，就重新计算，解决搜索的bug
-典型的案例2、防抖节流函数适用于图片懒加载 

##节流函数的实际应用
-当持续触发事件的时候 保证一段时间内 只调用一次事件处理函数
一段时间内 只做一件事情
-典型的案例就是鼠标不断点击触发，在规定时间内多次点击只生效一次

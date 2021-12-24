## js与ts中的函数重载
一、ES5中并没有原生实现重载

二、手动实现原理
 
1、需要有某个容器去记录我载入了那些方法。

2、需要在传入参数的时候，根据载入记录，去判断应该执行哪一个方法。

3、明确this指向。

三、实现方案

1、定义一个专门用于存放重载函数的对象。

2、定义一个管理重载函数的方法。

```javascript
const obj = {};
function addReLoadFn(obj, key, fn) {
    const oldFn = obj[key];
    obj[key] = function () {
        if (fn.length === arguments.length) {
           return fn.apply(this, arguments);
        }
        return oldFn.apply(this, arguments);
    }
}
```

说明：

1、先判断fn是因为，fn是最后注册的函数，而oldFn是以前绑定的函数，需要从后向前对比参数，就需要先判断最后注册的函数。

2、需要返回执行结果，因为原函数可能需要return值。

3、this指向需要绑定到obj。

四、调取方法
```javascript
// 1.先载入函数
addReLoadFn(obj, 'fn', function (a) {
    return a;
});
addReLoadFn(obj, 'fn', function () {
    return 'c';
});

// 2.再调用函数
const n = obj.fn();
console.log(n);

const a = obj.fn(21);
console.log(a);
```

五、ts函数重载
```javascript
interface User {
    name: string;
    age: number;
}

declare function test(para: User): number;
declare function test(para: number, flag: boolean): number;
```

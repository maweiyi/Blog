JavaScript中的函数不仅是一种类似于Java中方法的语言功能，它还可以作为对象存在

### 上下文

函数的每次调用都会拥有一个特殊值——本次调用的上下文（context）——这就是this关键字的值。 如果函数挂载在一个对象上，作为对象的一个属性，就称它为对象的方法。当通过这个对象来调用函数时，该对象就是此次调用的上下文， 也就是该函数的this的值。


*和变量不同，关键字this没有作用域的限制，嵌套的函数不会从调用它的函数中继承this。 - 如果嵌套函数作为方法调用，其this的值指向调用它的对象。 - 如果嵌套函数作为函数调用，其this的值不是全局对象（非严格模式下）就是undefined（严格模式下）。*

```
var o = {
  m: function() {
    var self = this;
    console.log(this==o); // true
    f();

    function f() {
      console.log(this === o); // false，this的值是全局对象或undefined
      console.log(self === o); // true
    }
  }
}
```

### call() And apply()

```
var o = {
    name: "Maweiyi"
};

function f() {
    console.log(this.name);

}

f();//undefined

f.call(o);//Maweiyi
f.apply(o,[]);//实参放在一个数组中
```

*call()和apply()可以看作为某个对象的方法，通过调用方法的形式来间接调用函数。 它们的第一个参数是要调用函数的母对象，它是调用上下文，在函数体内通过this来获得对它的引用。 apply()方法和call()方法的作用相同，只不过函数传递的方式不一样，它的实参都放入在一个数组中。*

### bind()

方法的主要作用就是将函数绑定到某个对象

当在函数f()上调用bind()方法并后窜入一个对象o作为参数，这个方法将返回一个新函数： （以函数调用的方式）调用新的函数将会把原始的函数f()作为o的方法来调用.

```
function f(y) {
  return this.x + y;
}

var o = {
  x: 1
};

var g = f.bind(o);  // 通过调用 g(x) 来调用 o.f(x)
g(2); // 3



function pp(x) {
    console.log(this.y);
    console.log(x);

}


var o = {
    y: "Maweiyi"
};

(pp.bind(o, 2))();
```



### ES7的async/await


```
const f = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(123);
    }, 2000);
  });
};

const testAsync = async () => {
  const t = await f();
  console.log(t);
};

testAsync();
```

```
const f = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(123);
    }, 2000);
  });
};

const testAsync = () => {
  f().then((t) => {
    console.log(t);
  });
};

testAsync();
```


### 异常处理

```
/*代码片段中将 f 方法中的 resolve 改为 reject，在 testAsync 中，通过 catch 可以捕获到 reject 的数据，输出 err 的值为 234。try/catch 使用时也要注意范围和层级。如果 try 范围内包含多个 await，那么 catch 会返回第一个 reject 的值或错误。*/
const f = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject(234);
    }, 2000);
  });
};

const testAsync = async () => {
  try {
    const t = await f();
    console.log(t);
  } catch (err) {
    console.log(err);
  }
};
```

```
/*
testAsync 函数体中 try 有两个 await 函数，而且都分别 reject，那么 catch 中仅会触发 f1 的 reject，输出的 err 值是 111。
*/
const f1 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject(111);
    }, 2000);
  });
};

const f2 = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      reject(222);
    }, 3000);
  });
};

const testAsync = async () => {
  try {
    const t1 = await f1();
    console.log(t1);
    const t2 = await f2();
    console.log(t2);
  } catch (err) {
    console.log(err);
  }
};
```

### async
async:表示这是一个async函数, await只能用在这个函数里面
await:表示在这里等待promise返回结果再继续执行,await 后面跟着的应该是一个promise对象

--harmony_async_await
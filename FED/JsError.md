# 前端代码异常监控

[相关链接](https://zhuanlan.zhihu.com/p/31979395)

## JS 异常处理

对于 Javascript 而言，我们面对的仅仅只是异常，异常的出现不会直接导致 JS 引擎崩溃，最多只会使当前执行的任务终止。

1. 当前`代码块`将作为一个任务压入任务队列中，JS 线程会不断地从任务队列中提取任务执行。
2. 当任务执行过程中出现异常，且异常没有捕获处理，则会一直沿着调用栈一层层向外抛出，最终终止当前任务的执行。
3. JS 线程会继续从任务队列中提取下一个任务继续执行。


### try-catch 异常处理

ry-catch 在我们的代码中经常见到，通过给代码块进行 try-catch 进行包装后，当代码块发生出错时 catch 将能捕捉到错误的信息，页面也将可以继续执行。

但是 try-catch 处理异常的能力有限，只能捕获捉到运行时`非异步错误`，对于`语法错误`和`异步错误`就显得无能为力，捕捉不到。

### window.onerror 异常处理

window.onerror 捕获异常能力比 try-catch 稍微强点，无论是`异步`还是`非异步`错误，onerror 都能捕获到运行时错误。  

然而 window.onerror 对于`语法错误`还是无能为力，所以我们在写代码的时候要尽可能避免语法错误的，不过一般这样的错误会使得整个页面崩溃，还是比较容易能够察觉到的。

### Promise 错误

通过 Promise 可以帮助我们解决异步回调地狱的问题，但是一旦 Promise 实例抛出异常而你没有用 catch 去捕获的话，onerror 或 try-catch 也无能为力，无法捕捉到错误。  




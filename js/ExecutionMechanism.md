# JavaScript代码执行机制---Event Loop
### javascript是一门单线程语言
* 同步任务
* 异步任务
### 当我们打开网站时，网页的渲染过程就是一大堆同步任务，比如页面骨架和页面元素的渲染。而像加载图片音乐之类占用资源大耗时久的任务，就是异步任务
* 同步和异步任务分别进入不同的执行"场所"，同步的进入主线程，异步的进入Event Table并注册函数
* 当指定的事情完成时，Event Table会将这个函数移入Event Queue
* 主线程内的任务执行完毕为空，会去Event Queue读取对应的函数，进入主线程执行
* 上述过程会不断重复，也就是常说的Event Loop(事件循环)
### 我们不禁要问了，那怎么知道主线程执行栈为空啊？js引擎存在monitoring process进程，会持续不断的检查主线程执行栈是否为空，一旦为空，就会去Event Queue那里检查是否有等待被调用的函数
* macro-task（宏任务）：包括整体代码script，setTimeout，setInterval
* micro-task（微任务）：Promise，process.nextTick
### 事件循环的顺序，决定js代码的执行顺序。进入整体代码(宏任务)后，开始第一次循环。接着执行所有的微任务。然后再次从宏任务开始，找到其中一个任务队列执行完毕，再执行所有的微任务

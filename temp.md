产品DFX泛指产品所有非功能特性，如稳定性、可用性、性能等。
当前软件DFX能力建立在对软件运行状态的观测以及故障的管理，主要受益人为平台以及应用开发。
编程语言与运行平台是2个关联却不耦合的概念，如何度量一个编程语言在一个平台的DFX能力的完备程度?
这里尝试从2个方面出发回答这个问题：
1.语言运行时DFX能力，语言针对开发者错误预防、检测的设计以及维测支持
这里同时包含开发态以及运行态的能力
##编码规范及静态检测工具，能够检测常见的编码错误，例如未判空，未加锁

##动态检测(语言接口提供的资源)
资源类（提供申请接口，需提供必要的维测能力包括DUMP/TRACE/STACK)：
文件句柄，线程，GlobalRef、LocalRef
并发类：ConcurrentModificationException
内存类：ASAN/HWASAN，支持Java堆内存问题的检测

##异常处理
同步异常：直接抛出
异步异常(kotlin)：await时抛出
协程异常(kotlin)：CoroutineExceptionHandler
重抛异常：NestedException、包含原始异常调用栈及重抛调用栈
未处理异常：java/lang/Thread/UncaughtExceptionHandler
跨语言异常：未定义

##运行时维测：
堆栈：
跨语言堆栈回溯(Java/kotlin/native)
在线/离线符号解析
GC：gcstats
对象:heapdump
异常终止(RuntimeException)：加载失败、GlobalRef满

2.平台DFX集成，语言对该平台上的DFX能力的实现
平台接口对接：
维测接口：
LOG：android/util/Log
TRACE：android/os/Trace
EVENT：android/util/EventLog

平台异常：android/util/AndroidException
https://developer.android.com/reference/android/util/AndroidException

平台故障日志：
NativeCrash(tombstone)：包含跨语言堆栈(Java/Kotlin/Native)
ANR：包含跨语言堆栈(Java/Kotlin/Native)以及虚拟机信息导出
JavaCrash:仅包含语言异常堆栈

平台工具对接：
simpleperf:能够同时打印java、native指令数，支持采样率最高1KHz
perffeto:trace/heap profiler包含native以及java


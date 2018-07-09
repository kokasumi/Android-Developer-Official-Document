## Android平台架构

> 来源：[ Platform Architecture][platform-architecture]
>
> 翻译参与者：[Mnilg](https://github.com/mnilg/)

Android是一个基于Linux的开源软件栈，下图展示了Android的平台架构：

![Android软件栈](https://developer.android.google.cn/guide/platform/images/android-stack_2x.png)

- **Linux内核层**：内核负责与设备的硬件连接，为系统的其余部分提供服务，执行如管理设备CPU和内存之类的任务。Android是基于Linux内核，借助Linux内核服务实现硬件设备驱动，进程和内存管理，网络协议栈，电源管理，无限通信等核心功能，对Linux内核层做部分修改，作为硬件和软件栈之间的抽象层。
- **硬件抽象层(HAL)**： [硬件抽象层(HAL)](hardware-abstraction-layer)提供标准接口，将设备硬件功能暴露给更高层次的[Java API框架](java-api-framework)。HAL由多个库模块组成，每个库模块都实现特定类型硬件组件接口，如[Camera](camera)和[Bluetooth](bluetooth)模块。当框架API访问硬件设备时，Android系统加载该硬件组件的库模块。
- **Android运行时**：对于Android 5.0(API 21)及以上版本设备，每个应用都有一个自己的[Android运行时(Android Runtime，ART)](android-runtime)并且运行在自己的进程。ART能够在低内存设备上运行多个执行DEX格式的虚拟机，DEX是一种专为Android设计的优化最小内存占用的字节码格式。对于Android 5.0以下的设备，Dalvik时Android运行时，能够在ART上运行良好的应用，也能够在Dalvik上运行良好，反之则不一定。ART相比较Dalvik主要具有以下特性：
  - 预编译(Ahead-of-time，AOT)以及即时编译(Just-in-time，JIT)。
  - 优化垃圾回收(GC)。
  - 更好的调试模式，包含专用的采样分析器，详细的诊断异常和奔溃报告，并且能够设置观察点以监控特定的字段。
- **C/C++本地库**：许多Android系统组件或者服务是由C/C++编写的本地代码编译构建的，Android提供了一些Java框架API暴露一些本地库给应用。应用可以使用C/C++代码开发，使用[Android NDK](android-ndk)可以访问一些[本地平台库](native-platform-library)。
- **Java API框架**：通过Java API，Android操作系统的整个功能集对于应用都可用。这些API简化了重用核心、模块化系统组件及服务来创建Android应用，包括以下几个方面：
  - 丰富可扩展的[视图系统](view-system)，可用于构建应用UI。
  - [资源管理器](resource-manager)，提供对非代码资源的访问。如字符串，布局文件等。
  - [通知管理器](notification-manager)，能够让应用在状态栏显示自定义通知。
  - [Activity管理器](activity-manager)，管理应用生命周期并提供常用[返回任务栈](navigation-back-stack)。
  - [Content Provider](content-provider)：能够提供数据给其他应用，如联系人应用。
- **系统应用**：Android系统自身附带了一系列的应用程序，如电子邮件/短信/浏览器等。



[hardware-abstraction-layer]: https://source.android.google.cn/devices/index.html#Hardware%20Abstraction%20Layer	"Handware abstraction layer"
[java-api-framework]: https://developer.android.google.cn/guide/platform/#api-framework	"Java API Framework"
[camera]: https://source.android.google.cn/devices/camera/index.html	"Camera"
[bluetooth]: https://source.android.google.cn/devices/bluetooth.html	"Bluetooth"
[android-runtime]: http://source.android.google.cn/devices/tech/dalvik/index.html	"Android Runtime"
[android-ndk]: https://developer.android.google.cn/ndk/index.html	"Android NDK"
[native-platform-library]: https://developer.android.google.cn/ndk/guides/stable_apis.html	"Native Platform Library"
[view-system]: https://developer.android.google.cn/guide/topics/ui/overview.html	"View System"
[resource-manager]: https://developer.android.google.cn/guide/topics/resources/overview.html	"Resource Manager"
[notification-manager]: https://developer.android.google.cn/guide/topics/ui/notifiers/notifications.html	"Notification Manager"
[activity-manager]: https://developer.android.google.cn/guide/components/activities.html	"Activity Manager"
[navigation-back-stack]: https://developer.android.google.cn/guide/components/tasks-and-back-stack.html	"Natigation back stack"
[content-provider]: https://developer.android.google.cn/guide/topics/providers/content-providers.html	"Content provider"
[platform-architecture]: https://developer.android.google.cn/guide/platform/	"Platform Architecture"
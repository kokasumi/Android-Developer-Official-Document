## 使用Pseudolocales测试应用

> 来源：[Test your app with pseudolocales](https://developer.android.google.cn/guide/topics/resources/pseudolocales)
>
> 翻译参与者：[Mnilg](https://github.com/mnilg/)

Pseudolocale是一种模拟翻译应用时导致UI，布局以及其他翻译相关问题的语言环境。Pseudolocale是即时翻译的并且自动翻译成可读的本地化英语消息，能够帮助在开发阶段调试本地化造成的UI文本以及布局问题。Android平台提供了2种Pseudolocale分别代表Left-to-right(LTR)和Right-to-left(RTL)语言：

- **English(XA)**：在基础英语UI文本上加上拉丁音调，通过添加非重音文本和每个消息单元括号来扩展原始文本，以此来暴露扩展文本种的潜在问题。暴露的问题可能是布局损坏或者格式错误的消息语法。具体如下图所示：

  ![English (XA) pseudolocale](https://developer.android.google.cn/images/develop/pseudo-locale-example-app_2x.png) 

- **AR(XB)**：将原始消息从左到右的文本方向改变为从右到左，反转了原始消息种的字符。具体效果如下图所示：

  ![AR (XB) pseudolocale](https://developer.android.google.cn/images/develop/pseudo-locale-example-app-rtl_2x.png) 

### 启用pseudolocales

Pseudolocales通常在开发构建阶段使用，必须运行在Android 4.3(API 18)及以上版本并且启用了开发者选项。

1. 首先在项目`build.gradle`进行以下配置：

   ```groovy
   android {
     ...
     buildTypes {
       debug {
         pseudoLocalesEnabled true
       }
     }
   ```

2. 编译并运行应用。

3. 根据Android系统版本选择pseudolocale。

### Pseudolocale发现本地化问题

Pseudolocales提供一种省时有效的方式来发现以下潜在问题：

- 硬编码字符串，不能被翻译，在pseudolocale种显示为非重音文字方便用户察觉。
- 由文本扩展引起的UI布局问题，显示UI因文本长度中断。
- 字符串连接，显示为2条或者多条以`{}`分隔的消息。这就使得翻译困难，因为翻译人员会单独翻译每个模块，无法连续翻译相关的部分。字符串连接也使得无法正确翻译，因为不同的语言可能具有不同的部分顺序或者完全不同的句子结构。
- 双向(BIDI)文本问题，如一个文本方向上的内容包括相反文本方向的内联短语时，使得字符串难以阅读。
- 从右到左的问题(RTL)，如UI元素没有向左移动，文本没有反转向左移动或者标点符号错位，"pseudolocales rule! "应该显示为"!elur selacoloduesp"，但实际上显示为"elur selacoloduesp! "。
## Activity简介

> 来源：[Introduction to Activities](https://developer.android.google.cn/guide/components/activities/intro-activities)
>
> 整理者：[Mnilg](https://github.com/mnilg/)

Activity提供了与用户进行交互的UI窗口，通常的应用都包含多个Activity。Android应用中一般都有一个**主Activity**，**主Activity**主要是指从主屏幕进入的第一个Activity，并不是说每次进入应用都从主Activity进入；Android提供了多入口机制，每个Activity都可以作为进入应用的入口，比如说，当从主屏幕进入邮件应用时，应用首先打开的是邮件列表的页面，而如果从社交应用打开邮件应用，可能就直接进入发送邮件的页面。

### Activity的Manifest配置

必须在Manifest文件中配置了Activity，应用才能够使用。一般配置Activity需要按照以下步骤进行：

1.**声明Activity**：在`<application>`标签中添加`<activity>`子标签并使用Activity的类名定义`android:name`，这样就添加了一个Activity声明。

```xml
<manifest ... >
  <application ... >
      <activity android:name=".ExampleActivity" />
      ...
  </application ... >
  ...
</manifest >
```

2.**声明Intent Filter(可选)**：一般的Activity都只能显示启动，也就是说必须指明想要启动的Activity。如果想要隐式启动Activity，就必须在声明Intent Filter，这样系统才能根据启动条件筛选符合条件的Activity组件。在`<activity>`标签中使用`<intent-filter>`标签声明过滤条件，其中必须包含`<action>`标签以及可选的`<category>`和`<data>`标签。

```xml
<activity android:name=".ExampleActivity" android:icon="@drawable/app_icon">
    <intent-filter>
        <action android:name="android.intent.action.SEND" />
        <category android:name="android.intent.category.DEFAULT" />
        <data android:mimeType="text/plain" />
    </intent-filter>
</activity>
```

```java
// Create the text message with a string
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND);
sendIntent.setType("text/plain");
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
// Start the activity
startActivity(sendIntent);
```

3.**声明权限**：Activity可以设置访问权限，只有具有相关权限的应用才能够启动该Activity。`<activity>`标签中的`android:permission`属性来设置访问权限，如果想要启动该Activity，就需要在应用中使用`<uses-permission>`标签添加相关权限请求。

```xml
<manifest>
<activity android:name="...."
   android:permission=”com.google.socialapp.permission.SHARE_POST”

/>
```

```xml
<manifest>
   <uses-permission android:name="com.google.socialapp.permission.SHARE_POST" />
</manifest>
```

### Activity声明周期

![activity_lifecycle](https://developer.android.google.cn/guide/components/images/activity_lifecycle.png) 


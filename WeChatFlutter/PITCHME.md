---

# We Chat @color[#84CDF4](Flu)@color[#6DB8F2](tt)@color[#2F5993](er)
- catsuo
- 2018.07.06

---

- @color[#84CDF4](About Flutter)
 - UI Framework
 - Tools
- @color[#84CDF4](About Dart)
 - 单线程模型
 - Asynchrony
 - JIT & AOT

---

**@color[#84CDF4](About Flutter)**
<br><br>
@ul
- Google开发的跨平台移动应用开发SDK，同时也将是Google Fuchsia下开发应用的主要工具
- 第一个版本被称作“天空”。 于2015年的Flutter开发者会议上被公布，目标为实现120FPS的渲染性能
- v0.5.6  --  10 days ago
@ulend

---

**@color[#84CDF4](UI Framework)**
<br><br>
@ul
- Widget
- Element
- RenderObject
@ulend

---

**@color[#84CDF4](Widget)**
<br><br>
[Everything's a Widget!](https://flutter.io/widgets/)

+++

@ul
- 用Widget构建UI，重写build方法
- Widget只是一个配置容器，其本身是静态的不可变的
- Widget分类
 - StatefulWidget @color[#84CDF4](逻辑组件)
 - StatelessWidget @color[#84CDF4](逻辑组件)
 - RenderObjectWidget @color[#84CDF4](物理组件)
@ulend

+++

**@color[#84CDF4](StatefulWidget)**
<br><br>
@ul
- 没有实际布局意义，其作用主要是将其他组件组合在一起通过build方法返回一个整体的结构
- 与一个可变的State绑定在一起
@ulend
+++

```dart
class SampleAppPage extends StatefulWidget {
  SampleAppPage({Key key}) : super(key: key);

  @override
  _SampleAppPageState createState() => new _SampleAppPageState();
}

class _SampleAppPageState extends State<SampleAppPage> {
  // Default placeholder text
  String textToShow = "I Like Flutter";

  void _updateText() {
    setState(() {
      // update the text
      textToShow = "Flutter is Awesome!";
    });
  }

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Sample App"),
      ),
      body: new Center(child: new Text(textToShow)),
      floatingActionButton: new FloatingActionButton(
        onPressed: _updateText,
        tooltip: 'Update Text',
        child: new Icon(Icons.update),
      ),
    );
  }
 }
```
@[1,4-5](自定义一个派生自StatefulWidget的类，并重写其createState方法返回一个与该Widget绑定的状态对象)
@[8,19-32](自定义一个派生自State的类，重写其build方法返回与该State对应的自定Widget结构)
@[26-30](为floatingActionButton设置一些列的属性，其中包括一个onPressd事件处理函数_updateText)
@[12-17](在这个方法内调用State类的setState方法，参数是一个无参的匿名函数，匿名函数中更新textToShow)
@[25](自定义的Widget结构中有用到textToShow，onPressed事件处理后文本内容发生变化)


+++

@ul
- State用来封装Widget中用到的需要在生命周期中改变的内容
- 通过更新State中的内容，并将更新动作传递给State类的setState方法来通知Flutter Framework
- Flutter Framework会重新调用State类的build方法，进而刷新界面
@ulend

+++

**@color[#84CDF4](StatelessWidget)**
<br><br>
@ul
- 没有实际布局意义，其作用主要是将其他组件组合在一起通过build方法返回一个整体的结构
- 没有与之绑定的State，描述一个不可变的静态的布局结构
@ulend

+++

```dart
class SampleApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Sample App',
      theme: new ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: new SampleAppPage(),
    );
  }
}
```
@[3-12](重写StatelessWidget类的build方法，返回自定义的Widget结构。它没有可变的State，在UI刷新时如果不是add/remove，系统可以忽略该部分信息)

+++

**@color[#84CDF4](RenderObjectWidget)**
<br><br>
@ul
- 具有实际的布局意义，这类型组件会创建一个对应的RenderObject
- RenderObject用来渲染对应的Widget（layout paint）
- 系统已经提供了很多RenderObjectWidget的实现可以满足大部分应用场景
@ulend

---

**@color[#84CDF4](Element & RenderObject)**
<br><br>

- Widget定义UI的描述信息
- 系统使用Widget定义的描述信息生成与之对应的Element，并由众多Element组成Elements Tree
- 物理组件会对应自己的RenderObject实现，RenderObject用于定义对应Widget的渲染方式（Layout & Paint）
- 逻辑组件没有与其对应的RenderObject，因为对他们layout和paint没有实际意义

+++?image=assets/chatflutter/img/Flutter_DrawFrame.png&size=auto 80%

+++?image=assets/chatflutter/img/WidgetTree1.png&size=70% auto

+++?image=assets/chatflutter/img/WidgetTree2.png&size=auto 80%

+++

@ul
- RenderObject的默认实现是RenderBox
- RenderBox实现一个基于笛卡尔坐标的布局和绘制算法
- 我们愿意的话可以派生RenderObject实现自己的渲染算法
@ulend

+++

![image](assets/chatflutter/img/RenderObject_Extend.png)


+++

![image](assets/chatflutter/img/layout.png)

+++

**@color[#84CDF4](Graphics Pipeline)**
<br><br>

+++?image=assets/chatflutter/img/graphics_pipeline.png&size=auto 80%

+++?image=assets/chatflutter/img/graphics_pipeline2.png&size=auto 80%

---

**Widget @color[#5d5d5d](advanced xml in Android)** 
<br><br>
**Element @color[#5d5d5d](part of view in Android)** 
<br><br>
**RenderObject @color[#5d5d5d](part of view in Android)** 

---

**@color[#84CDF4](About Flutter - Tools)**
<br><br>
Flutter Plugin for AS
<br>
![Performance Profiling](assets/chatflutter/img/visual_debugging.png)

+++

![Performance Profiling](assets/chatflutter/img/performance-overlay-green.png)

+++

![Performance Profiling](assets/chatflutter/img/performance-overlay-jank.png)

---

**@color[#84CDF4](About Dart)**
<br><br>
@ul
- 单线程模型
- Asynchrony
- JIT & AOT
@ulend

---

**@color[#84CDF4](单线程模型)**
<br><br>
@ul
- Dart是一个单线程模型语言
- Dart其实没有线程的概念，取而代之是Isolate（Thread/Proc）
<br>

+++

@ul
- Isolate与线程类似，也是程序的最小执行单元
- 但是与线程不同的是，Isolate之间不共享任何内存
- Isolate之间通过port通信，通信的消息在接受方也会先做一次Copy操作
@ulend

+++?image=assets/chatflutter/img/Dart_Isolate.png&size=auto 80%

+++

@ul
- Dart也是基于Event-Looper及Event-Queue模型
- 一个Isolate中包含一个Event-Looper和两个Queue
@ulend

+++

两个Queue
@ul
- Event Queue
- Microtask Queue
@ulend

+++

@ul
- Event Queue中主要包含用户的交互，文件I/O，计时器的触发等事件
- Microtask Queue用于协助完成Event Queue中事件的收尾工作
@ulend

+++?image=assets/chatflutter/img/event_loop2.png&size=auto 80%

---

**@color[#84CDF4](Asynchroy)**
<br><br>
@ul
- Future 
 - 一个表示其结果可能在将来某个时间点才会返回的类。
 - 新建一个Future意味着往Event Queue队尾插入一个Event
 - 等到该事件被处理后会回调Future的回调方法
- async & await
 - Dart1.9加入的语法糖
 - 以同步的写法来实现异步操作
@ulend

+++

**@color[#84CDF4](Future)**
<br><br>
```dart
import 'dart:async';

main() {
  printDailyNewsDigest();
  printWinningLotteryNumbers();
}

printWinningLotteryNumbers() {
  print('Winning lotto numbers: [23, 63, 87, 26, 2]');
}

printDailyNewsDigest() {
  final future = gatherNewsReports();
  future.then((news) => print(news));
}

const news = '<gathered news goes here>';

const oneSecond = Duration(seconds: 1);
final newsStream = new Stream.periodic(oneSecond, (_) => news);

// Imagine that this function is more complex and slow. :)
Future<String> gatherNewsReports() => newsStream.first;
```
@[3-6](程序入口)
@[8-10,12-15](定义两个业务方法)
@[13-14](调用gatherNewsReports方法，该方法返回一个Future类型,被认为是一个异步方法，于是可以使用返回的future的一些列api注册回调)
@[17-23](模拟耗时操作，在1s后gatherNewsReport方法完成其真正的工作)
@[14](这时候前面用Future.then方法注册的回调将会执行)

+++

**@color[#84CDF4](async & await)**
<br><br>
```dart
import 'dart:async';

main() {
  printDailyNewsDigest();
  printWinningLotteryNumbers();
}

printWinningLotteryNumbers() {
  print('Winning lotto numbers: [23, 63, 87, 26, 2]');
}

printDailyNewsDigest() async {
  String news = await gatherNewsReports();
  print(news);
}

const news = '<gathered news goes here>';

const oneSecond = Duration(seconds: 1);
final newsStream = new Stream.periodic(oneSecond, (_) => news);

// Imagine that this function is more complex and slow. :)
Future<String> gatherNewsReports() => newsStream.first;
```
@[3-6](程序入口)
@[8-10,12-15](定义两个业务方法。printDailyNewsDigest方法用async声明，表明这是一个异步方法)
@[13-14](调用gatherNewsReports方法，该方法返回一个Future类型,被认为是一个异步方法。与之前直接处理返回的Future对象不同，此处使用await关键字调用异步方法)
@[17-23](模拟耗时操作，在1s后gatherNewsReport方法完成其真正的工作)

+++

**@size[8em]("Asynchroy")**
<br><br>
@ul
- 无法发挥CPU多核的优势
- 多个Isolate，实现真正的异步
@ulend

---

**@color[#84CDF4](JIT & AOT)**
<br><br>
@ul
- JIT
 - 在开发阶段采用JIT方式编译，提升开发体验。尤其是其引以为傲的hot reload
- AOT
 - 在发布阶段采用AOT方式编译，直接将代码编译为本地代码。提高代码运行效率
@ulend

---

# @color[#84CDF4](END) 
## @color[#84CDF4](THANK YOU)




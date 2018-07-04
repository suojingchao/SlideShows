---

# We Chat @color[#84CDF4](Flu)@color[#6DB8F2](tt)@color[#2F5993](er)
- catsuo
- 2018.07.06

---

- @color[#84CDF4](About Flutter)
 - UI Framework
 - Tools
- @color[#84CDF4](About Dart)

---

**@color[#84CDF4](UI Framework)**
<br>
@ul
- Widget
- Element
- RenderObject
@ulend

+++

- Widget定义UI的视图信息
- 系统使用Widget中定义的描述信息生成与之对应的Element，并由众多Element组成Elements Tree
- RenderObject由Element管理，完成整个树的Layout和Paint

+++?image=assets/chatflutter/img/Flutter_DrawFrame.png&size=auto 80%

---

**@color[#84CDF4](Widget)**
<br>
@ul
- 用Widget构建UI，重写build方法
- Widget只是一个配置容器，其本身是不可变的
- Widget分类
 - StatefulWidget @color[#84CDF4](逻辑组件)
 - StatelessWidget @color[#84CDF4](逻辑组件)
 - RenderObjectWidget @color[#84CDF4](物理组件)
@ulend

+++?image=assets/chatflutter/img/catalog_widgets.png&size=auto 80%

[Click Me](https://flutter.io/widgets/)

+++

**@color[#84CDF4](StatefulWidget)**
<br>
没有实际布局意义，其作用主要是将其他组件组合在一起通过build方法返回一个整体的结构
build方法返回的才是其对应的物理组件

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
@[24](自定义的Widget结构中有用到textToShow，onPressed事件处理后文本内容发生变化)


+++

- State用来封装Widget中用到的需要在生命周期中改变的内容
- 通过更新State中的内容，并将更新动作传递给State类的setState方法来通知Flutter Framework
- Flutter Framework会重新调用State类的build方法，进而刷新界面

+++

**@color[#84CDF4](StatelessWidget)**
<br>
没有实际布局意义，其作用主要是将其他组件组合在一起通过build方法返回一个整体的结构
build方法返回的才是其对应的物理组件

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
<br>
具有实际的布局意义，这类型组件会对应一个具体的RenderObject
RenderObject用于对组件对应的Element进行layout和paint

---

**@color[#84CDF4](Element)**
<br>
与一个Widget对应，Widget会用自身的配置信息创建Element实例，同一个Widget有可能对应多个不同的Element实例
在每一次屏幕刷新的build phase阶段会为所有Widget生成对应的Element，所有Element形成一个Elements Tree

+++

![Elements Tree](assets/chatflutter/img/elements.png)

---

**@color[#84CDF4](RenderObject)**
<br>
真正负责Widget内容的layout和paint
在每一次屏幕刷新的build phase阶段会为所有Widget生成对应的RenderObhect，所有RenderObhect形成一个RenderObhects Tree
@ul
但 Elements Tree  !=  RenderObjects Tree
@ulend

+++

逻辑组件没有与其对应的RenderObject，因为对他们layout和paint没有实际意义

+++

RenderObject的默认实现是RenderBox
RenderBox实现一个基于笛卡尔坐标的布局和绘制算法
我们愿意的话可以实现自己的RenderObject

+++?image=assets/chatflutter/img/RenderObject_Extend.png&size=auto 60%


+++?image=assets/chatflutter/img/layout.png&size=auto 80%

+++

**@color[#84CDF4](Graphics Pipeline)**
<br>

+++?image=assets/chatflutter/img/graphics_pipeline.png&size=auto 80%

+++?image=assets/chatflutter/img/graphics_pipeline2.png&size=auto 80%

---

**Widget @color[#5d5d5d](advanced xml in Android)** 
<br>
**Element @color[#5d5d5d](part of view in Android)** 
<br>
**RenderObject @color[#5d5d5d](part of view in Android)** 

---

**@color[#84CDF4](About Flutter - Tools)**
<br>
Flutter Plugin for AS
![Performance Profiling](assets/chatflutter/img/visual_debugging.png)

+++

![Performance Profiling](assets/chatflutter/img/performance-overlay-green.png)

+++

![Performance Profiling](assets/chatflutter/img/performance-overlay-jank.png)

---

**@color[#84CDF4](About Dart)**
<br>
@ul
- 单线程模型
- Isolate
- Asynchrony
- JIT & AOT
@ulend

---

**@color[#84CDF4](单线程模型)**
<br>
所有Dart代码运行在同一Isolate(默认情况下)
One Event-Loop,  Two Queues

+++?image=assets/chatflutter/img/event_loop2.png&size=auto 80%

---

**@color[#84CDF4](Isolate?)**
<br>
它类似于线程，也表示程序的最小执行单元
但不与其他Isolate共享内存

+++?image=assets/chatflutter/img/Dart_Isolate.png&size=auto 80%

---

**@color[#84CDF4](Asynchroy in Dart)**
<br>
@ul
- Future 
 - 一个表示其结果可能在将来某个时间点才会返回的类。可以通过为其设置回调，回调方法会在其相关的任务完成后调用
- async & await
 - Dart1.9加入的语法糖，本质也是实现异步操作
@ulend

+++

**@color[#84CDF4](Future)**
<br>
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
<br>
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

**@color[#84CDF4]("Asynchroy")**
<br>
一个Isolate， 一个Event-loop
@ul
无法发挥CPU多核的优势
多个Isolate，实现真正的异步
@ulend

---

**@color[#84CDF4](JIT & AOT)**
<br>
@ul
- JIT
 - 在开发阶段采用JIT方式编译，提升开发体验。尤其是其引以为傲的hot reload
- AOT
 - 在发布阶段采用AOT方式编译，直接将代码编译为本地代码。提高代码运行效率
@ulend

---





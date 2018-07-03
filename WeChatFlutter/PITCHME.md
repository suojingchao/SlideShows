---

# We Chat @color[#84CDF4](Flu)@color[#6DB8F2](tt)@color[#2F5993](er)
- catsuo
- 2018.07.06

---

- About UI Framework
- About Dart

---

**About UI Framework**
<br>
@ul
- Widget
- Element
- RenderObject
@ulend

+++

- Widget定义UI的视图信息
- Flutter Framework使用Widget中定义的描述信息生成与之对应的Element，并由众多Element组成Elements Tree
- RenderObject由Element管理，完成整个树的Layout和Paint

---

**About Widget**
<br>
@ul
- 用Widget构建UI
- Widget只是一个配置容器，其本身是不可变的
 - advanced xml布局文件
- Everything's a Widget
 - StatefulWidget
 - StatelessWidget
@ulend

+++

![Stateful and Stateless](assets/chatflutter/img/stateful_stateless.png)

+++

![Widget catalog](assets/chatflutter/img/catalog_widgets.png)
[Click Me](https://flutter.io/widgets/)

---

**StatefulWidget**
<br>
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

---

**StatelessWidget**
<br>
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

---

**About Elements**
<br>
An instantiation of a Widget at a particular location in the tree
(View in Android)
![Elements Tree](assets/chatflutter/img/elements.png)

---

**About RenderObject**
<br>
![Layout Data Flow](assets/chatflutter/img/layout.png)

+++

**Graphics Pipeline**
<br>
![Graphics Pipeline](assets/chatflutter/img/graphics_pipeline.png)

+++

![Graphics Pipeline2](assets/chatflutter/img/graphics_pipeline2.png)

---

**About Dart**
<br>
@ul
- 单线程模型
- Isolate
- Asynchrony
- JIT & AOT
@ulend

---

**单线程模型**
<br>
All code run in the same isolate (defualt)
One Event-Loop,  Two Queues

+++

![Event-Loop and Queues](assets/chatflutter/img/event_loop2.png)

---

**What's @color[#6DB8F2](Isolate)?**
<br>
Isolate   Thread or Process
![Isolate memory]()

+++

without shared memory
without locks

---

**Asynchroy in Dart**
<br>
@ul
- Future 
 - A Future represents a means for getting a value sometime in the future
- async & await
 - added in Dart 1.9, Syntactic sugar
@ulend

+++

**Usage of Future**
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

**async & await Simple**
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

**"Asynchroy"**
<br>
一个Isolate， 一个Event-loop
无法发挥CPU多核的优势
(Android: handler.sendDelayMessage)

+++

多个Isolate，实现真正的异步

---

**JIT & AOT**
<br>
@ul
- JIT
 - 在开发阶段使用JIT方式编译，方便我们实现很棒的开发体验。尤其是其引以为傲的hot reload
- AOT
 - 在发布阶段使用AOT方式编译，直接将代码编译为本地代码。大大提高代码运行效率
@ulend

---





---

# We Chat @color[84CDF4](Flu)@color[6DB8F2](tt)@color[2F5993](er)
- Widget
- About Dart

---

## Everything's a Widget
@ul
- StatefulWidget
- StatelessWidget
@ulend
+++
![Stateful and Stateless](assets/chatflutter/img/stateful_stateless.png)
+++
![Widget catalog](assets/chatflutter/img/catalog.png)

---

## Usage of StatefulWidget
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
@[1,4-5](override createState method to return a State)
@[8,19-32](override build method to return a custom StatefulWidget)
@[26](when floatingActionButton pressed, call _updateText method)
@[12-17](upadte textToShow)
@[24](refresh display content)

---

## Usage of StatelessWidget
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
@[3-12](override build method to return custom StatelessWidget)

---

## How Widgets Work
A widget is an immutable @color[6DB8F2](description) of part of a UI. Widgets can be inflated into @color[6DB8F2](elements), which manage the underlying @color[6DB8F2](render tree)

+++

## Widgets
Describes the configuration for an Element

+++

## Elements
An instantiation of a Widget at a particular location in the tree
![Elements Tree](assets/chatflutter/img/elements.png)

+++

## RenderObject
![Layout Data Flow](assets/chatflutter/img/layout.png)

+++

## Graphics Pipeline
![Graphics Pipeline](assets/chatflutter/img/graphics_pipeline.png)

+++

![Graphics Pipeline2](assets/chatflutter/img/graphics_pipeline2.png)

---

## About Dart
@ul
- Single thread
- Isolate
- Asynchrony
- JIT & AOT
@ulend

---

## Single thread
All code run in the same isolate (defualt)
One Event-Loop,  Two Queues

+++

![Event-Loop and Queues](assets/chatflutter/img/event_loop2.png)

---

## What's @color[6DB8F2](Isolate)?
Isolate Thread Process
![Isolate memory]()

---

## Asynchroy in Dart
@ul
- Future 
 - A Future represents a means for getting a value sometime in the future
- async & await
 - added in Dart 1.9, Syntactic sugar
@ulend

+++

## Future Simple
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
@[3-6](program entry)
@[8-10,12-15]()
@[17-23]()

+++

## async & await Simple
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
@[3-6](program entry)
@[8-10,12-15]()
@[17-23]()

+++

## "Asynchroy"
In One Isolate, One Event-Loop

---

## JIT & AOT






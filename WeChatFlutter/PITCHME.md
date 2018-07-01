---
@size[26em](Something @color[blue](Flutter))
@size[20em](Widget)
@size[20em](About Dart)

---
@size[26em](Everything's a Widget)
与分离View，View Controlers，Layout和其他属性的其他UI框架不同，Flutter具有一致的统一对象模型：Widget
@ul
- StatefulWidget
- StatelessWidget
@ulend
+++
![Stateful and Stateless]()
+++
![Widget catalog]()
---
@size[26em](Usage of StatefulWidget)
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
@size[26em](Usage of StatelessWidget)
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
@size[26em](How Widgets Work)
A widget is an immutable @color[blue](description) of part of a UI. Widgets can be inflated into @color[blue](elements), which manage the underlying @color[blue](render tree)
+++
### Widgets
Describes the configuration for an Element
+++
### Elements
An instantiation of a Widget at a particular location in the tree
![Elements Tree]()
+++
### RenderObject
![Layout Data Flow]()
+++
### Graphics Pipeline
![Graphics Pipeline]()
+++
![Graphics Pipeline2]()
---
### About Dart
@ul
- Single thread
- Isolate
- Asynchrony
- JIT & AOT
@ulend
---
### Single thread
All code run in the same isolate (defualt)
One Event-Loop,  Two Queues
+++
![Event-Loop and Queues]()
---
### What's @color[blue](Isolate)?
Isolate Thread Process
![Isolate memory]()
---
### Asynchroy in Dart
@ul
- Future
- async & await
@ulend
+++
### Future Simple
+++
### async & await Simple
+++
### "Asynchroy"





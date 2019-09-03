# FLUTTER INHERITED WIDGET
 How to implement Inherited Widget in Flutter

## Introduction:
 This Article explains how state will be managed in flutter. There is a method you already know about is provider, scoped model, redux etc. Inherited Widget is also a state management technique. Inherited Widget is fit in some cases where we want to manage state but in complex structure it is not recommended to use it. Now let’s see Inherited Widgets in Flutter in detail.

## Steps:
 Step 1
 First and basic step to create new application in flutter. If you are a beginner in flutter then you can check my blog Create a first app in Flutter. I have created an app named as “flutter_inherited_widget”.

 Step 2
 Now you can see that you will have counter app by default now our purpose is to make the same app using inherited widget.

 Step 3
 Now Create a new file named as count_provider.dart. In this file we will implement class named  as Counter which stores count variable and an increment() which increment count variable. There is another class which is inherited widget called CountProvider which will be accessible to other class where we need count variable. Following is the programming implementation of that.

```
import 'package:flutter/widgets.dart';
 
class CountProvider extends InheritedWidget {
 final Widget child;
 final Counter counter;
 CountProvider({Key key, this.child, this.counter})
     : super(key: key, child: child);
 
 static CountProvider of(BuildContext context) {
   return (context.inheritFromWidgetOfExactType(CountProvider)
       as CountProvider);
 }
 
 @override
 bool updateShouldNotify(CountProvider oldWidget) {
   return true;
 }
}
 
class Counter {
 int count;
 Counter(this.count);
 increment() {
   count++;
 }
}
```

 Step 4
 Now in main.dart file we will access the inherited widget using counterProvider = CountProvider.of(context);  following is the programming implementation of that.

```
import 'package:flutter/material.dart';
import 'package:flutter_inherited_widget/count_provider.dart';
 
void main() => runApp(MyApp());
 
class MyApp extends StatelessWidget {
 @override
 Widget build(BuildContext context) {
   return MaterialApp(
     theme: ThemeData(
       primarySwatch: Colors.blue,
     ),
     home: CountProvider(
       counter: Counter(0),
       child: MyHomePage(),
     ),
   );
 }
}
 
class MyHomePage extends StatefulWidget {
 MyHomePage({Key key, this.title}) : super(key: key);
 final String title;
 
 @override
 _MyHomePageState createState() => _MyHomePageState();
}
 
class _MyHomePageState extends State<MyHomePage> {
 var counterProvider;
 void _incrementCounter() {
   setState(() {
     counterProvider.counter.increment();
   });
 }
 
 @override
 Widget build(BuildContext context) {
   counterProvider = CountProvider.of(context);
   return Scaffold(
     appBar: AppBar(
       title: Text('Flutter Inherited Widget'),
     ),
     body: Center(
       child: Column(
         mainAxisAlignment: MainAxisAlignment.center,
         children: <Widget>[
           Text(
             'You have pushed the button this many times:',
           ),
           Text(
             '${counterProvider.counter.count}',
             style: Theme.of(context).textTheme.display1,
           ),
         ],
       ),
     ),
     floatingActionButton: FloatingActionButton(
       onPressed: _incrementCounter,
       tooltip: 'Increment',
       child: Icon(Icons.add),
     ),
   );
 }
}
```

 Hurrey…. Run the app and Test It on emulator/simulator or device :)))

 Conclusion:
  State Management is one of the key parts of performance improvement of the app and Inherited Widget is one of the approach of it.

 Git Repo: https://github.com/myvsparth/flutter_inherited_widget
 ## Related to Tags: Flutter, State Management, Inherited Widget

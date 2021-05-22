# Flutter navigation

A Route is an abstraction for a “screen” or “page” of an app, and a Navigator is a widget that manages routes. 

***

In Flutter, you have a couple options to navigate between pages:

Specify a Map of route names. (using MaterialApp)
Directly navigate to a route. (using WidgetsApp)

```dart
void main() {
 runApp(MaterialApp(
   home: MyAppHome(), // Becomes the route named '/'.
   routes: <String, WidgetBuilder> {
     '/a': (BuildContext context) => MyPage(title: 'page A'),
     '/b': (BuildContext context) => MyPage(title: 'page B')
 ));
}
``` 

```dart
Navigator.of(context).pushNamed('/b');
``` 

## What is the equivalent of startActivityForResult()?

```dart
Map coordinates = await Navigator.of(context).pushNamed('/location');

``` 

```dart
Navigator.of(context).pop({"lat":43.821757,"long":-79.226392});

``` 
## Typical Widget and async operation

```dart
import 'dart:convert';

import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

void main() {
  runApp(SampleApp());
}

class SampleApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Sample App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: SampleAppPage(),
    );
  }
}

class SampleAppPage extends StatefulWidget {
  SampleAppPage({Key key}) : super(key: key);

  @override
  _SampleAppPageState createState() => _SampleAppPageState();
}

class _SampleAppPageState extends State<SampleAppPage> {
  List widgets = [];

  @override
  void initState() {
    super.initState();
    loadData();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Sample App'),
      ),
      body: ListView.builder(
        itemCount: widgets.length,
        itemBuilder: (BuildContext context, int position) {
          return getRow(position);
        },
      ),
    );
  }

  Widget getRow(int i) {
    return Padding(
      padding: EdgeInsets.all(10.0),
      child: Text("Row ${widgets[i]["title"]}"),
    );
  }

  Future<void> loadData() async {
    String dataURL = 'https://jsonplaceholder.typicode.com/posts';
    http.Response response = await http.get(dataURL);
    setState(() {
      widgets = jsonDecode(response.body);
    });
  }
}

``` 

## HTTP


To use the http package, add it to your dependencies in pubspec.yaml:
dependencies:



```dart
// ...http: ^0.11.3+16
import 'dart:convert';

import 'package:http/http.dart' as http;

Future<void> loadData() async {
  String dataURL = 'https://jsonplaceholder.typicode.com/posts';
  http.Response response = await http.get(dataURL);
  setState(() {
    widgets = jsonDecode(response.body);
  });
}
``` 

This is [HOW TO SHOW PROGRESS OF TASK](https://flutter.dev/docs/get-started/flutter-for/android-devs#how-do-i-show-the-progress-for-a-long-running-task "Progress") inline link.

## Assets
You can then access your images using AssetImage:

```dart
AssetImage('images/my_icon.jpeg');
``` 

```dart
@override
Widget build(BuildContext context) {
  return Image.asset('images/my_image.png');
}
``` 

## Layouts

> In Android, a LinearLayout is used to lay your widgets out linearly—either horizontally or vertically. In Flutter, use the Row or Column widgets to achieve the same result.

```dart
  @override
  Widget build(BuildContext context) {
    return Row(
      mainAxisAlignment: MainAxisAlignment.center,
      children: <Widget>[
        Text('Row One'),
        Text('Row Two'),
        Text('Row Three'),
        Text('Row Four'),
      ],
    );
  }
``` 





  





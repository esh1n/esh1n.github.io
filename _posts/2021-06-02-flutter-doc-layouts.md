# Flutter layouts

The core of Flutter’s layout mechanism is widgets. In Flutter, almost everything is a widget—even layout models are widgets. The images, icons, and text that you see in a Flutter app are all widgets. But things you don’t see are also widgets, such as the rows, columns, and grids that arrange, constrain, and align the visible widgets.. 

![](https://flutter.dev/assets/ui/layout/sample-flutter-layout-46c76f6ab08f94fa4204469dbcf6548a968052af102ae5a1ae3c78bc24e0d915.png)
***

## Material apps
For a Material app, you can use a `Scaffold` widget; it provides a default banner, background color, and has API for adding `drawers, snack bars, and bottom sheets`. Then you can add the Center widget directly to the body property for the home page.

## Aligning widgets
You control how a row or column aligns its children using the `mainAxisAlignment` and `crossAxisAlignment` properties. For a row, the main axis runs horizontally and the cross axis runs vertically. For a column, the main axis runs vertically and the cross axis runs horizontally.

![](https://flutter.dev/assets/ui/layout/row-diagram-ad51795e19e3e1d412815b287c9caa694ad357892e3ab8b3ef1da0c4c6e011db.png)

![](https://flutter.dev/assets/ui/layout/column-diagram-4e2ce8e33c32a09d090280fb7b2925baaf58f6de7876a551c207ab904e2fafc6.png)

### Space Evenly

```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  children: [
    Image.asset('images/pic1.jpg'),
    Image.asset('images/pic2.jpg'),
    Image.asset('images/pic3.jpg'),
  ],
);
```
compiles to :

![](https://flutter.dev/assets/ui/layout/row-spaceevenly-visual-bae00ee7fc0b8a0fbe46d74b113f9f0e4e4942e55609cf263cefca81f986d871.png)


and 

```dart
Column(
  mainAxisAlignment: MainAxisAlignment.spaceEvenly,
  children: [
    Image.asset('images/pic1.jpg'),
    Image.asset('images/pic2.jpg'),
    Image.asset('images/pic3.jpg'),
  ],
);
```

compiles to 

![](https://flutter.dev/assets/ui/layout/column-visual-075205bae7b5e6e5ee7be85a1a3ded9bdb52319b41c75d83710c0216d4084904.png)


## Standard widgets
- `Container`: Adds padding, margins, borders, background color, or other decorations to a widget.
- `GridView`: Lays widgets out as a scrollable grid.
- `ListView`: Lays widgets out as a scrollable list.
- `Stack`: Overlaps a widget on top of another.

## Material widgets
- `Card`: Organizes related info into a box with rounded corners and a - drop shadow.
- `ListTile`: Organizes up to 3 lines of text, and optional leading and trailing icons, into a row.


### Summary (Container)
1. Add padding, margins, borders
1. Change background color or image
1. Contains a single child widget, but that child can be a Row, Column, or even the root of a widget tree

![](https://flutter.dev/assets/ui/layout/margin-padding-border-9616dd0d7af45b95e6fcface25cd933b6b4a0fda51c1ab1bb9287bc8ed92c356.png)

### Examples (Container)

```dart
Widget _buildImageColumn() => Container(
      decoration: BoxDecoration(
        color: Colors.black26,
      ),
      child: Column(
        children: [
          _buildImageRow(1),
          _buildImageRow(3),
        ],
      ),
    );
    
   Widget _buildDecoratedImage(int imageIndex) => Expanded(
      child: Container(
        decoration: BoxDecoration(
          border: Border.all(width: 10, color: Colors.black38),
          borderRadius: const BorderRadius.all(const Radius.circular(8)),
        ),
        margin: const EdgeInsets.all(4),
        child: Image.asset('images/pic$imageIndex.jpg'),
      ),
    );

Widget _buildImageRow(int imageIndex) => Row(
      children: [
        _buildDecoratedImage(imageIndex),
        _buildDecoratedImage(imageIndex + 1),
      ],
    ); 
```

compiles to:
![](https://flutter.dev/assets/ui/layout/container-c31fce287ed0d6c2b0de32af625b2351bd8a08c236a2e60578f940c7b4aceece.png)


## Samples : different item types

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    MyApp(
      items: List<ListItem>.generate(
        1000,
            (i) => i % 6 == 0
            ? HeadingItem('Heading $i')
            : MessageItem('Sender $i', 'Message body $i'),
      ),
    ),
  );
}

class MyApp extends StatelessWidget {
  final List<ListItem> items;

  MyApp({Key? key, required this.items}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    final title = 'Mixed List';

    return MaterialApp(
      title: title,
      home: Scaffold(
        appBar: AppBar(
          title: Text(title),
        ),
        body: ListView.builder(
          // Let the ListView know how many items it needs to build.
          itemCount: items.length,
          // Provide a builder function. This is where the magic happens.
          // Convert each item into a widget based on the type of item it is.
          itemBuilder: (context, index) {
            final item = items[index];

            return ListTile(
              title: item.buildTitle(context),
              subtitle: item.buildSubtitle(context),
            );
          },
        ),
      ),
    );
  }
}

/// The base class for the different types of items the list can contain.
abstract class ListItem {
  /// The title line to show in a list item.
  Widget buildTitle(BuildContext context);

  /// The subtitle line, if any, to show in a list item.
  Widget buildSubtitle(BuildContext context);
}

/// A ListItem that contains data to display a heading.
class HeadingItem implements ListItem {
  final String heading;

  HeadingItem(this.heading);

  @override
  Widget buildTitle(BuildContext context) {
    return Text(
      heading,
      style: Theme.of(context).textTheme.headline5,
    );
  }

  @override
  Widget buildSubtitle(BuildContext context) => SizedBox();
}



/// A ListItem that contains data to display a message.
class MessageItem implements ListItem {
  final String sender;
  final String body;

  MessageItem(this.sender, this.body);

  @override
  Widget buildTitle(BuildContext context) => Text(sender);

  @override
  Widget buildSubtitle(BuildContext context) => Text(body);
}
```    

## Managing stateful widget

```dart
class _FeedImagesScreenState extends State<FeedImagesScreen> {
  final List<String> _saved = [];

  void _toggleFavorite(ImageItem planet) {
    setState(() {
      String name = planet.name;
      final alreadySaved = _saved.contains(name);
      if (alreadySaved) {
        _saved.remove(name);
      } else {
        _saved.add(name);
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.start,
          mainAxisSize: MainAxisSize.max,
          crossAxisAlignment: CrossAxisAlignment.stretch,
          children: <Widget>[
            Expanded(child: _justList()),
          ],
        ),
      ),
    );
  }

  Widget _justList() {
    return ImageList(
        planets: widget.images,
        namesOfSaved: widget.saved,
        onTapPlanet: (planet) => widget.onTapped(planet),
        onTapFavorite: (planet) => widget.onFavouriteTapped(planet));
    // onTapFavorite: (planet) => _toggleFavorite(planet));
  }
}
```

## Func with closure

```dart
void main() {
  int Function(int) closure() => (int x) => x + 1;
  int Function(int) func = (int x) => x + 1;
  print('closure ${closure()(3)} func ${func(3)}');
}
```
    


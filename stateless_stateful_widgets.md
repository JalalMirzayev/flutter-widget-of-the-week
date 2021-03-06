# Stateless Widgets

This file explains how to extract a stateless widget as a reusable component. Let us have a look at the code. There are three positions in the code.
CODE01 is followed by a `DecoratedBox`. CODE02 does the same thing as the `DecoratedBox` by using the stateful widget CODE03.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(new DogApp());
}

class DogApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        title: 'My Dog App',
        home: Scaffold(
          appBar: AppBar(
            title: Text('Yellow Lab'),
          ),
          body: Center(
            child: Column(
              children: [
                // This is position CODE01.
                DecoratedBox(
                    decoration: BoxDecoration(color: Colors.lightBlueAccent),
                    child: Padding(
                      padding: const EdgeInsets.all(8.0),
                      child: Text('Nico'),
                    )),
                SizedBox(
                  height: 8.0,
                ),
                // This is position CODE02.
                DogName(name: 'Nico'),
              ],
            ),
          ),
        ));
  }
}

// This is position CODE03.
class DogName extends StatelessWidget {
  final String name;
  
  // The @required annotation is use to show that the optional parameter is required.
  // Normall we only have to use this for multiple named parameters.
  const DogName({@required this.name}): assert(name != null);

  @override
  Widget build(BuildContext context) {
    return DecoratedBox(
        decoration: BoxDecoration(color: Colors.lightBlueAccent),
        child: Padding(
          padding: const EdgeInsets.all(8.0),
          child: Text(name),
        ));
  }
}
```

# Stateful Widgets

```dart
import 'package:flutter/material.dart';

class ItemCount extends StatelessWidget {
  final String name;
  final int count;

  const ItemCount({@required this.name, @required this.count})
      : assert(name != null),
        assert(count != null);

  @override
  Widget build(BuildContext context) {
    return Container(
      child: Text('My name is ${this.name} and the count is ${this.count}.'),
    );
  }
}

class ItemCounter extends StatefulWidget {
  final String name;

  const ItemCounter({this.name});

  @override
  _ItemCounterState createState() => _ItemCounterState();
}

class _ItemCounterState extends State<ItemCounter> {
  int count = 0;
  @override
  Widget build(BuildContext context) {
    return GestureDetector(
        onTap: () {
          setState(() {
            count++;
          });
        },
        child: Text('${widget.name}: $count'));
  }
}
```

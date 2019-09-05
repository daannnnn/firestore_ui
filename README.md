# firestore_ui

[![pub package](https://img.shields.io/pub/v/firestore_ui.svg)](https://pub.dartlang.org/packages/firestore_ui)

This project started as a [Pull Request](https://github.com/flutter/plugins/pull/757) to the official [cloud_firestore](https://pub.dartlang.org/packages/cloud_firestore) plugin, but unfortunately they are still polishing the main features and this had to be postponed.

But fear not, my fellow Cloud Firestore users, this is a package that extracted the main code from that PR and now it's available to use!

Check out the example for more info, it should be pretty straight forward since it's just a port of [firebase_database](https://pub.dartlang.org/packages/firebase_database)'s version.

# How to use

All the examples below are from the actual `example` folder, please run that to see how it behaves!

## List

Just set it up as you would with a `ListView.builder`:

```dart
FirestoreAnimatedList(
    query: query,
    itemBuilder: (
        BuildContext context,
        DocumentSnapshot snapshot,
        Animation<double> animation,
        int index,
    ) => FadeTransition(
            opacity: animation,
            child: MessageListTile(
            index: index,
            document: snapshot,
            onTap: _removeMessage,
        ),
    ),
);
```

## Grid

Just set it up as you would with a `GridView.count`, alongside the necessary `crossAxisCount`, all the other parameters from the `SliverGridDelegateWithFixedCrossAxisCount` are also available:

```dart
FirestoreAnimatedGrid(
    query: query,
    crossAxisCount: 2,
    mainAxisSpacing: 4.0,
    childAspectRatio: 1.0,
    crossAxisSpacing: 4.0,
    itemBuilder: (
        BuildContext context,
        DocumentSnapshot snapshot,
        Animation<double> animation,
        int index,
    ) => FadeTransition(
        opacity: animation,
        child: MessageGridTile(
            index: index,
            document: snapshot,
            onTap: _removeMessage,
        ),
    ),
);
```

## Staggered

Just set it up as you would with a `StaggeredGridView.countBuilder`, alongside the necessary `crossAxisCount` and the `staggeredTileBuilder`:

```dart
FirestoreAnimatedStaggered(
    query: query,
    staggeredTileBuilder: (index) => StaggeredTile.count(2, index.isEven ? 2 : 1),
    crossAxisCount: 4,
    mainAxisSpacing: 4.0,
    crossAxisSpacing: 4.0,
    itemBuilder: (
        BuildContext context,
        DocumentSnapshot snapshot,
        Animation<double> animation,
        int index,
    ) => FadeTransition(
        opacity: animation,
        child: MessageGridTile(
            index: index,
            document: snapshot,
            onTap: _removeMessage,
        ),
    ),
);
```

# overlay_support_example

exmaple for overlay_support

## Simple Usage

popup a notification or toast:

```dart
showSimpleNotification(context,
                      Text("this is a message from simple notification"),
                      background: Colors.green);

toast(context, 'this is a message from toast');

```

## popup a custom notification

you can custom your notification widget to popup, for example:

```dart
 NotificationEntry entry;
 entry = showOverlayNotification(context, (_) {
   return MessageNotification(
     onReplay: () {
       entry.dismiss();
       showDialog(
           context: context,
           builder: (context) {
             return SimpleDialog(
               title: Text('message'),
             );
           });
     },
   );
 }, duration: Duration(milliseconds: 4000));
 ```
 
```dart MessageNotification Class
class MessageNotification extends StatelessWidget {
  final VoidCallback onReplay;

  const MessageNotification({Key key, this.onReplay}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Card(
      margin: const EdgeInsets.symmetric(horizontal: 4),
      child: SafeArea(
        child: ListTile(
          leading: SizedBox.fromSize(
              size: const Size(40, 40),
              child: ClipOval(child: Image.asset('assets/avatar.png'))),
          title: Text('Lily MacDonald'),
          subtitle: Text('Do you want to see a movie?'),
          trailing: IconButton(
              icon: Icon(Icons.reply),
              onPressed: () {
                ///TODO i'm not sure it should be use this widget' BuildContext to create a Dialog
                ///maybe i will give the answer in the future
                if (onReplay != null) onReplay();
              }),
        ),
      ),
    );
  }
}
```

## popup a custom overlay

for example, we need create a iOS Style Toast.

```dart
  showOverlay(context, (_, t) {
    return Theme(
      data: Theme.of(context),
      child: Opacity(
        opacity: t,
        child: IosStyleToast(),
      ),
    );
  });
```

```dart IosStyleToast
class IosStyleToast extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return SafeArea(
      child: DefaultTextStyle(
        style: Theme.of(context).textTheme.body1.copyWith(color: Colors.white),
        child: Padding(
          padding: const EdgeInsets.all(16),
          child: Center(
            child: ClipRRect(
              borderRadius: BorderRadius.circular(10),
              child: Container(
                color: Colors.black87,
                padding: const EdgeInsets.symmetric(
                  vertical: 8,
                  horizontal: 16,
                ),
                child: Column(
                  mainAxisSize: MainAxisSize.min,
                  children: <Widget>[
                    Icon(
                      Icons.check,
                      color: Colors.white,
                    ),
                    Text('Succeed')
                  ],
                ),
              ),
            ),
          ),
        ),
      ),
    );
  }
}

```

## End

if you have some suggestion or advice, please open an issue to let me known. 
This will greatly help the improvement of the usability of this project.
Thanks.

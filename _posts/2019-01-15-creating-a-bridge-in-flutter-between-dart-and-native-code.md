---
layout: post
title:  "Creating a bridge in Flutter between Dart and native code"
author: atul
categories: [ programming, technology ]
image: assets/images/2019-01-15-creating-a-bridge-in-flutter-between-dart-and-native-code-3.png
featured: false
hidden: false
---
Flutter allows us to call platform-specific APIs available in Java or Kotlin code on Android, or in ObjectiveC or Swift code on iOS.

Flutter’s platform-specific API works with message passing.

From Flutter app we have to send messages to a host on iOS or Android parts of the app over a platform channel.
The host listens on the platform channel, and receives the message. It then uses any platform-specific APIs using the native programming language and sends back a response to the Flutter portion of app.

## Architectural overview
<figure>
  <img src="{{site.baseurl}}/assets/images/2019-01-15-creating-a-bridge-in-flutter-between-dart-and-native-code-3.png" alt="Architecture"/>
  <figcaption>Architecture</figcaption>
</figure>

Messages are passed between the Flutter Code(UI) and host (platform) using platform channels. Messages and responses are passed asynchronously and the user interface remains responsive.

On Dart side using MethodChannel(API) we sends a message which is corresponding to a method call. On the Android side MethodChannel Android (API) and on the iOS side FlutterMessageChannel (API) is used for receiving method calls and sending back result. These classes allow us to develop a platform plugin with a very simple code.

If require, method calls can also be sent in the reverse direction, with the Android/IOS platform acting as client and method implemented in Dart.

## Data types supported by Platform Channel
The standard platform channel uses standard message codec that supports efficient binary serialization of simple JSON-like values of types boolean, number, String, byte buffer, list and map. The serialization and deserialization of these values to and from messages happens automatically when we send and receive values.
<figure>
  <img src="{{site.baseurl}}/assets/images/2019-01-15-creating-a-bridge-in-flutter-between-dart-and-native-code-2.png" alt="Data types"/>
  <figcaption>Supported Data Types</figcaption>
</figure>

## Creating flutter app that calls iOS and Android code
Now we will create a flutter app with a method call that will be implemented in Android (java) and iOS (Objective C) respectively.

### Step 1: Create a new app project

In a terminal run:

flutter create flutter_to_native

By default, Flutter supports writing Android code in Java  and iOS code in Objective C. If you want to use Kotlin and Swift, create project with the following command.

flutter create -i swift -a kotlin flutter_to_native

### Step 2: Create a platform Channel

The client and host sides of the channel are connected through the channel name passed in the channel constructor. All channel names used in a single app must be unique. In our example we are creating the channel name flutter.native/helper

```
class _MyHomePageState extends State<MyHomePage> {
  static const platform = const MethodChannel('flutter.native/helper');
```

### Step 3:Invoke method on platform Channel

Invoke a method on the method channel, specifying the concrete method to call via the String identifier. In the code below, it is helloFromNativeCode

```
String response = "";
  try {
    final String result = await  platform.invokeMethod('helloFromNativeCode');
    response = result;
  } on PlatformException catch (e) {
    response = "Failed to Invoke: '${e.message}'.";
  }
```

Use the returned response to update the user interface state inside setState.

```
setState(() {
  _responseFromNativeCode = response;
});
```

### Step 4: Create method implementation in Android using java

In Android Studio open Flutter app and select the android folder inside it. Open the file MainActivity.java

Now we have to create a MethodChannel with the same name that we have created in Flutter App.

```
public class MainActivity extends FlutterActivity {
  private static final String CHANNEL = "flutter.native/helper";
  .....
}
```

We have to create a MethodCallHandler in onCreate method

```
new MethodChannel(getFlutterView(), CHANNEL).setMethodCallHandler(
        new MethodChannel.MethodCallHandler() {
          @Override
          public void onMethodCall(MethodCall call, MethodChannel.Result result) {
            if (call.method.equals("helloFromNativeCode")) {
              String greetings = helloFromNativeCode();
              result.success(greetings);
            }
}});
```

### Step 4: Create method implementation in iOS using Objective C

Open the file AppDelegate.m of your Flutter app in Xcode. Now we have to create a FlutterMethodChannel with the same name that we have created in Flutter App.

```
FlutterViewController* controller = (FlutterViewController*)self.window.rootViewController;
        FlutterMethodChannel* nativeChannel = [FlutterMethodChannel
        methodChannelWithName:@"flutter.native/helper"
        binaryMessenger:controller];
```

Create method call handler

```
[nativeChannel setMethodCallHandler:^(FlutterMethodCall* call, FlutterResult result) {
        if ([@"helloFromNativeCode"  isEqualToString:call.method]) {
        NSString *strNative = [weakSelf helloFromNativeCode];
        result(strNative);
        } else {
        result(FlutterMethodNotImplemented);
        }
        }];
```

## Complete Code

### Complete Android Native code

```
import android.os.Bundle;
import io.flutter.app.FlutterActivity;
import io.flutter.plugin.common.MethodCall;
import io.flutter.plugin.common.MethodChannel;
import io.flutter.plugins.GeneratedPluginRegistrant;
public class MainActivity extends FlutterActivity {
  private static final String CHANNEL = "flutter.native/helper";
  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    GeneratedPluginRegistrant.registerWith(this);
    new MethodChannel(getFlutterView(), CHANNEL).setMethodCallHandler(
            new MethodChannel.MethodCallHandler() {
              @Override
              public void onMethodCall(MethodCall call, MethodChannel.Result result) {
                if (call.method.equals("helloFromNativeCode")) {
                  String greetings = helloFromNativeCode();
                  result.success(greetings);
                }
              }});
  }
  private String helloFromNativeCode() {
    return "Hello from Native Android Code";
  }
```
}

### Complete IOS native code

```
#include "AppDelegate.h"
        #include "GeneratedPluginRegistrant.h"

@implementation AppDelegate

        - (BOOL)application:(UIApplication *)application
        didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

        FlutterViewController* controller = (FlutterViewController*)self.window.rootViewController;
        FlutterMethodChannel* nativeChannel = [FlutterMethodChannel
        methodChannelWithName:@"flutter.native/helper"
        binaryMessenger:controller];
        __weak  typeof(self) weakSelf = self;
        [nativeChannel setMethodCallHandler:^(FlutterMethodCall* call, FlutterResult result) {
        if ([@"helloFromNativeCode"  isEqualToString:call.method]) {
        NSString *strNative = [weakSelf helloFromNativeCode];
        result(strNative);
        } else {
        result(FlutterMethodNotImplemented);
        }
        }];

        [GeneratedPluginRegistrant  registerWithRegistry:self];
        return [super  application:application didFinishLaunchingWithOptions:launchOptions];
        }
        - (NSString *)helloFromNativeCode {
        return  @"Hello From Native IOS Code";
        }

@end
```

### Complete Flutter code

```
import 'package:flutter/material.dart';
import 'dart:async';
import 'package:flutter/services.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      home: new HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: const Text('Native Code from Dart'),
      ),
      body: new MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  MyHomePage({Key key, this.title}) : super(key: key);

  final String title;

  @override
  _MyHomePageState createState() => new _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  static const platform = const MethodChannel('flutter.native/helper');
  String _responseFromNativeCode = 'Waiting for Response...';

  Future<void> responseFromNativeCode() async {
    String response = "";
    try {
      final String result = await platform.invokeMethod('helloFromNativeCode');
      response = result;
    } on PlatformException catch (e) {
      response = "Failed to Invoke: '${e.message}'.";
    }

    setState(() {
      _responseFromNativeCode = response;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Material(
      child: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.spaceEvenly,
          children: [
            RaisedButton(
              child: Text('Call Native Method'),
              onPressed: responseFromNativeCode,
            ),
            Text(_responseFromNativeCode),
          ],
        ),
      ),
    );
  }

}
```

### Result

Run the code on Android and iOS devices. Click on the Button “Call Native Method”
<figure>
  <img src="{{site.baseurl}}/assets/images/2019-01-15-creating-a-bridge-in-flutter-between-dart-and-native-code-1.png" alt="Result"/>
  <figcaption>Result</figcaption>
</figure>


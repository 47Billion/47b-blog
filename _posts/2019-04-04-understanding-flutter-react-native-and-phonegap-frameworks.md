---
layout: post
title:  "Understanding Flutter, React native and Phonegap frameworks"
author: atul
categories: [ technology, mobile development ]
image: assets/images/2019-04-04-understanding-flutter-react-native-and-phonegap-frameworks-1.png
featured: true
hidden: false
---

Most inexperienced mobile app developers decide on a programming language to use based on their previous experience and comfort. With proliferation of options of frameworks and languages now mainly for "write once, run everywhere" kind of mobile development, it is important to understand the core concepts behind each ogf them and make a conscious decision about which one to use based on their advantages and disadvantages. 

### Native Apps

Native app development involves using native programming languages of the devices to build the app. For iPhone, the native programming language is Objective C and the new Swift. For Android, the native programming language is Java and the new Kotlin.

### Phonegap

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-04-04-understanding-flutter-react-native-and-phonegap-frameworks-2.png" alt="Phonegap"/>
  <figcaption>Phonegap</figcaption>
</figure>

These are hybrid apps that are developed using web technologies: HTML5, CSS and JavaScript, then put inside a native container such as Adobe PhoneGap. These native containers run the web application code and package it into an app.

Both hybrid (HTML5, CSS and Javascript) and native apps are downloadable from Google Play or apple iTunes app Store.

Both the platform Android and IOS have WebView, a component in their library to render HTML content. Phonegap makes use of this WebView to run the entire application. All the components like button, checkbox, list, image etc. are created using HTML tags and CSS and action on these components are handled in JavaScript. Phonegap allows building both, standard Android and IOS apps. Developers need to put their HTML contents in assets folder of the application. Within the App, developers have to specify the entry point of the App that is generally index.html

Simple apps that need some forms or data displayed in various formats can be easily developed using Phonegap. The apps that need features which use smart phones camera, sensor, gps and various other hardware have phonegap plugins for different types of such hardware.

The biggest issue with phonegap based apps is the UI it doesn not have the look-and-feel of the native apps.

### React Native

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-04-04-understanding-flutter-react-native-and-phonegap-frameworks-3.png" alt="React Native"/>
  <figcaption>React Native</figcaption>
</figure>

React Native apps have native look-and-feel, since they render "native" components of the platform. Web developers familiar with React framework can write native apps quickly without need to learn  native programming languages like Java or Objective-C. 

As React Native apps render native views, they can show smooth, and fast nimations and undoubtedly faster response times. React Native tags are mapped with real native components instead of a WebView. This means React Native components have native code associated with them. Whenever we install any react native plugin, it comes with native code for iOS and Android. We have to link the react native plugin to our app just like linking any external library in the native code. Some of the plugin are linked via npm commands but some plugins require manual linking. So knowledge of native language (Java/Swift/Objective C) and IDE (Xcode/Android Studio) is required.

### Flutter

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-04-04-understanding-flutter-react-native-and-phonegap-frameworks-4.png" alt="Flutter"/>
  <figcaption>Flutter</figcaption>
</figure>

Google launched Flutter SDK (Software Development Kit) for easier cross-platform app development. Flutter SDK can be used to develop apps that give native UI experience for both Android and iOS platforms. To write apps using Flutter, you will have to use Dart programming language.

Instead of utilising web view or relying on the device’s OEM widgets, Flutter renders every view component using its own high-performance rendering engine. This allows building applications with native-like performance characteristics. The engine’s C/C++ code is compiled with NDK on Android and LLVM on iOS. Any Dart code is AOT-compiled to native code during compilation.

Flutter app is composed of Widgets (Stateless or Stateful). Flutter selects Canvas as a component from native Android and iOS libraries and draw all its components (Widgets) on that canvas. It means Flutter has its own components in place of native components of platform library. Flutter apps look like native iOS or Android apps, because they use platform-specific themes. Cupertino is a theme for iOS, and Material is a theme for Android.

### Conclusion

Basic difference between the approach of phonegap, react native and flutter to create cross platform app is the how they render the views on device.

Phonegap uses WebView as its main component from native library.

React Native maps its Tags with native components of Android and iOS.

Flutter draw its own components (widgets) on Canvas from the native library. 

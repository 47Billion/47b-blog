---
layout: post
title:  "Animating widgets in Flutter"
author: atul
categories: [ programming, technology ]
image: assets/images/2019-03-03-animating-widgets-in-flutter-1.gif
featured: false
hidden: false
---
Flutter is Google’s mobile app SDK for crafting high-quality native interfaces on iOS and Android in record time. Flutter’s animation support makes it easy to implement a variety of animation types. This article describes how to animate widgets in Flutter.

### Animation types

**Tween animation**

In tween animation, we have to define the start and end points of animation, timeline, and curve that defines the timing and speed of the transition. The framework calculates intermediate values from the start point to the end point.

**Physics-based animation**

In physics-based animation, motion resembles real-world behavior. When we throw a ball at an angle from the ground, it will follow the projectile motion. All the calculations like time of the flight and distance of travel will be calculated according to the laws of physics.

### Preparing classes for animation

We create a widget and update its state repeatedly at certain time intervals to animate it.

To create a widget we write a class that extends the *StatefulWidget* class and override its *createState()* method. This method returns a *State* instance.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-03-03-animating-widgets-in-flutter-2.png" alt="Extend StatefulWidget Class"/>
  <figcaption>Extend StatefulWidget Class</figcaption>
</figure>

The state object that is associate with our stateful widget must extend the *State* class, and also use a mixin called *SingleTickerProviderStateMixin*. We override the build method in which we create our widget object that we are going to animate.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-03-03-animating-widgets-in-flutter-3.png" alt="Override build method"/>
  <figcaption>Override build method</figcaption>
</figure>


### Creating Tween animation

In tween animation we need to provide two different values: a begin value and an end value. Flutter will then automatically generate a set of intermediate values. We apply these intermediate values to any property of widget to animate it.

Let us create a simple tween animation that moves a widget from left edge of the screen to the right edge of the screen. For this we have to animate the left property of a widget. All intermediate values are assigned to leftproperty of the widget.

To create and control the animation, we need an *Animation* object and an *AnimationController* object.

```
Animation<double> animation;
AnimationController controller;
```

In *initState* method of our class we reate *AnimationController*. It expects a *TickerProvider* object as one of its inputs. As our class is using the *SingleTickerProviderStateMixi* mixin, we can pass *this* to it. Other parameter is *duration* property to specify the duration of the animation.

```
controller = new AnimationController(vsync: this,
    duration: new Duration(seconds: 5));
```

Create a *Tween* object specifying the begin and end values of our animation.

```
Tween tween = new Tween<double>(begin: 0.0, end: 400.0);
```

Create Animation object using *tween* object.

```
animation = tween.animate(controller);
```

The animation object generates an animation event for every tick of the ticker. In order to handle events we use *addListener()* method. In event handler invoke *setState()* method to update the state of your widget and redraw it.

```
animation.addListener(() {
  setState(() {
  });
});
```

To start the animation, we invoke *forward()* method of the animation controller. If we want the animation to repeat, we can call *repeat()* method.

```
controller.repeat();
```

The animation is now ready. We can apply it to any widget.

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-03-03-animating-widgets-in-flutter-4.png" alt="Applying animation to widget"/>
  <figcaption>Applying animation to widget</figcaption>
</figure>

### Applying animation to widget

Now we create a widget and apply animation value to one of its property.

```
child: new Stack(
    children: <Widget>[
      new Positioned(
          child: FlutterLogo(),
          height: 100.0,
          width: 100.0,
          left: animation.value,
          top: 100.0  
      )
    ])
```

Here we have assigned animation value to *left* property of the widget.

### Animation effect

Add this widget in any of the screen in the App. Here is how it looks:

<figure>
  <img src="{{site.baseurl}}/assets/images/2019-03-03-animating-widgets-in-flutter-1.gif" alt="Flutter Animation"/>
  <figcaption>Flutter Animation</figcaption>
</figure>

### Complete Code

```
import 'package:flutter/animation.dart';
import 'package:flutter/material.dart';
class AnimationApp extends StatefulWidget {
  @override
  State<StatefulWidget> createState() {
    return new AnimationState();
  }
}

class AnimationState extends State<AnimationApp> with SingleTickerProviderStateMixin {
Animation<double> animation;
  AnimationController controller;
@override
  Widget build(BuildContext context) {
    return new Container(
        color: Colors.white,
        child: new Stack(
            children: <Widget>[
              new Positioned(
                  child: FlutterLogo(),
                  height: 100.0,
                  width: 100.0,
                  left: animation.value,
                  top: 100.0
              )
            ])
    );
  }

@override
  void initState() {
    super.initState();
    controller = new AnimationController(vsync: this,
        duration: new Duration(seconds: 4));
    Tween tween = new Tween<double>(begin: 0.0, end: 400.0);
    animation = tween.animate(controller);
    animation.addListener(() {
      setState(() {
      });
    });

    controller.repeat();
  }
}
```

> This article is a part of the series of articles related to mobile technology. If you are looking for a mobile app development team, please contact us at info@47billion.com.

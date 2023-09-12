# Flutter_doc_CokBK_NAV_Navigate_Navigate_with_named_route
 https://docs.flutter.dev/cookbook/navigation/named-routes
Navigate with named routes
==========================

1.  [Cookbook](https://docs.flutter.dev/cookbook)
2.  [Navigation](https://docs.flutter.dev/cookbook/navigation)
3.  [Navigate with named routes](https://docs.flutter.dev/cookbook/navigation/named-routes)

info Note: Named routes are no longer recommended for most applications. For more information, see [Limitations](https://docs.flutter.dev/ui/navigation#limitations) in the [navigation overview](https://docs.flutter.dev/ui/navigation) page.

In the [Navigate to a new screen and back](https://docs.flutter.dev/cookbook/navigation/navigation-basics) recipe, you learned how to navigate to a new screen by creating a new route and pushing it to the [`Navigator`](https://api.flutter.dev/flutter/widgets/Navigator-class.html).

However, if you need to navigate to the same screen in many parts of your app, this approach can result in code duplication. The solution is to define a *named route*, and use the named route for navigation.

To work with named routes, use the [`Navigator.pushNamed()`](https://api.flutter.dev/flutter/widgets/Navigator/pushNamed.html) function. This example replicates the functionality from the original recipe, demonstrating how to use named routes using the following steps:

1.  Create two screens.
2.  Define the routes.
3.  Navigate to the second screen using `Navigator.pushNamed()`.
4.  Return to the first screen using `Navigator.pop()`.

[](https://docs.flutter.dev/cookbook/navigation/named-routes#1-create-two-screens)1\. Create two screens
--------------------------------------------------------------------------------------------------------

First, create two screens to work with. The first screen contains a button that navigates to the second screen. The second screen contains a button that navigates back to the first.

content_copy

```
import 'package:flutter/material.dart';

class FirstScreen extends StatelessWidget {
  const FirstScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('First Screen'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Navigate to the second screen when tapped.
          },
          child: const Text('Launch screen'),
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  const SecondScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Second Screen'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            // Navigate back to first screen when tapped.
          },
          child: const Text('Go back!'),
        ),
      ),
    );
  }
}
```

[](https://docs.flutter.dev/cookbook/navigation/named-routes#2-define-the-routes)2\. Define the routes
------------------------------------------------------------------------------------------------------

Next, define the routes by providing additional properties to the [`MaterialApp`](https://api.flutter.dev/flutter/material/MaterialApp-class.html) constructor: the `initialRoute` and the `routes` themselves.

The `initialRoute` property defines which route the app should start with. The `routes` property defines the available named routes and the widgets to build when navigating to those routes.

content_copy

```
MaterialApp(
  title: 'Named Routes Demo',
  // Start the app with the "/" named route. In this case, the app starts
  // on the FirstScreen widget.
  initialRoute: '/',
  routes: {
    // When navigating to the "/" route, build the FirstScreen widget.
    '/': (context) => const FirstScreen(),
    // When navigating to the "/second" route, build the SecondScreen widget.
    '/second': (context) => const SecondScreen(),
  },
)
```

report_problem Warning: When using `initialRoute`, don't define a `home` property.

[](https://docs.flutter.dev/cookbook/navigation/named-routes#3-navigate-to-the-second-screen)3\. Navigate to the second screen
------------------------------------------------------------------------------------------------------------------------------

With the widgets and routes in place, trigger navigation by using the [`Navigator.pushNamed()`](https://api.flutter.dev/flutter/widgets/Navigator/pushNamed.html) method. This tells Flutter to build the widget defined in the `routes` table and launch the screen.

In the `build()` method of the `FirstScreen` widget, update the `onPressed()` callback:

content_copy

```
// Within the `FirstScreen` widget
onPressed: () {
  // Navigate to the second screen using a named route.
  Navigator.pushNamed(context, '/second');
}
```

[](https://docs.flutter.dev/cookbook/navigation/named-routes#4-return-to-the-first-screen)4\. Return to the first screen
------------------------------------------------------------------------------------------------------------------------

To navigate back to the first screen, use the [`Navigator.pop()`](https://api.flutter.dev/flutter/widgets/Navigator/pop.html) function.

content_copy

```
// Within the SecondScreen widget
onPressed: () {
  // Navigate back to the first screen by popping the current route
  // off the stack.
  Navigator.pop(context);

```

`\
`

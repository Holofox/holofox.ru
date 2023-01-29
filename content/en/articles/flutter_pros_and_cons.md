---
title: "Flutter Pros & Cons"
description: ""
date: 2023-01-29
tags: ["flutter", "kotlin", "dart", "java", "swift", "google", "apple"]
summary: "What does a developer need to know to switch to **Flutter**? Let's see what features you can encounter
and is it worth switching to?"
---

What does a developer need to know to switch to **Flutter**? The article will mention native languages and tools,
which are close to the usual representation of the mobile development process, which will help you get to know
tools and technologies used in [Flutter](https://flutter.dev/).

## What is Flutter?

[Flutter](https://flutter.dev/) is a free and open source toolkit for developing cross-platform
software that uses the [Dart](https://dart.dev/) language. If you are familiar with **Kotlin, Swift, Java**
or even **Typescript**, then **Dart** can become a kindred spirit too.

Distinctive features:

* open source project with a strong support community;
* own rendering engine, cross-platform and a single development language;
* safe interaction with native code through the platform channel;
* high performance in relation to other cross-platform tools.

## Pros

### Dart is the main reason developers love Flutter

To begin with, **Dart** was created by the **Google** team as a replacement or alternative to **JavaScript**. Start
writing in this language
can be as fast as learning to ride a bicycle without hands. You can start with
small [tours](https://dart.dev/guides/language/language-tour). By the way, the language is single-threaded out of the
box, but provides an [Event Loop](https://dart.cn/articles/archive/event-loop) mechanism that helps to work with
asynchronous/parallel operations.

And it all looks almost the same as [coroutines](https://kotlinlang.org/docs/coroutines-overview.html)
in [Kotlin](https://kotlinlang.org/) or even
like [Concurrency](https://docs.swift.org/swift-book/LanguageGuide/Concurrency.html) in [Swift](https://www.swift.org/),
let's see and compare the syntax:

#### Dart

```dart
class Language {
  const Language(this.name);

  final String name;

  Future<void> learn(Duration duration) {
    return Future<void>.delayed(
      duration, () => print('Well done! $name is learned!'),
    );
  }
}

Future<void> main() async {
  final dart = Language('Dart');
  await dart.learn(Duration(seconds: 2));
}
```

#### Kotlin

```kotlin
import kotlinx.coroutines.delay

class Language(private val name: String) {
    suspend fun learn(duration: Long) {
        delay(duration)
        print("Well done! $name is learned!")
    }
}

suspend fun main() {
    val kotlin = Language("Kotlin")
    kotlin.learn(2000L)
}
```

#### Swift

```swift
import Foundation

class Language {
  let name: String

  init(name: String) {
    self.name = name
  }

  func learn(interval: TimeInterval) async throws -> Void {
    try await Task.sleep(nanoseconds: UInt64(interval * 1_000_000_000))
    print("Well done! \(name) is learned!")
  }
}

Task.init {
  let swift = Language(name: "Swift")
  try await swift.learn(interval: 2.0)
}
```

As you can see, **Dart** has good code visual aesthetics, but beyond that, you can still find support:

* [null-safety](https://dart.dev/null-safety)
  and [static typing](https://dart.dev/guides/language/type-system);
* **just-in-time** in development mode and **ahead-of-time** in release mode;
* [implicit interfaces](https://dart.dev/guides/language/language-tour#implicit-interfaces)
  and [extension](https://dart.dev/guides/language/extension-methods).

### Simple and flexible layout

The user interface is declarative and consists
from [widgets](https://docs.flutter.dev/development/ui/widgets) - sort of components that can be placed
on the screen. When compared with familiar tools, you can try to bring
example [Jetpack Compose](https://developer.android.com/jetpack/compose) for **Android**
and [SwiftUI](https://developer.apple.com/xcode/swiftui/) for **iOS**.

To draw widgets, the [Skia](https://skia.org/) graphics engine is used, which is largely undemanding to
version and the platform itself, which allows you to embody truly incredible things. Physics and the widgets themselves
try to be close to system ones, repeating the guidelines of a particular system, which opens up an additional
opportunity to maximize their customize according to your goals and objectives.

You can get familiar with the layout of the user interface
from [introduction](https://docs.flutter.dev/development/ui/widgets-intro) to widgets.

### Fast adaptation to OS changes

Many cross-platform tools are reluctant to accept new OS changes, which often holds developers back
to keep up with the times. Consider an example with support
[ProMotion](https://developer.apple.com/documentation/quartzcore/optimizing_promotion_refresh_rates_for_iphone_13_pro_and_ipad_pro)
displays with dynamic frame rate. For any cross-platform tool, this is now a major challenge for making changes to the
engine core:

* make a number of changes that would allow you to work with the most efficient frame rate for specific
  devices;
* consider issues related to the impact of energy consumption;

With the release of the new **iPhone 13** line, developers immediately became interested in how applications written in
**Flutter**. The miracle did not happen, and on the very first day of sales in the repository
was [started](https://github.com/flutter/flutter/issues/90675) issue, also
there have been [first drafts](https://github.com/flutter/engine/pull/30900) that would add such support. On
the current moment there is support through the flag, which by
default is [written](https://github.com/flutter/flutter/pull/94509) in the project, but it is hardcoded to the minimum
frequency, which on the one hand makes it possible to use the screen to the fullest, and on the other hand -
leads to battery consumption.

**Flutter** is supported not only by the internal **Google** team, but also by the open developer community, which
allows
rejoice in such small things together, as joint efforts bring the cross-platform closer and closer to the native.

### Third party packages

Today, developers are making every effort to leave their contribution to the community.
[Flutter Favorite](https://docs.flutter.dev/development/packages-and-plugins/favorites) sets the bar high
quality that novice developers should focus on when choosing an external dependency in a project.

It is worth noting that the community is now in a good supply of stable packages that can be used in
working projects.

## Cons

Any tool has [weaknesses](https://github.com/flutter/flutter/wiki/Popular-issues) that you encounter only when you start
to approach the solution serious tasks.

### Code generation

Code generation may seem like an ideal solution in reducing developer time to write and maintain routine
parts of the project, but this is not always the case. In **Dart**, code generation is designed in such a way that it
has to be restarted every time to see new changes. In large projects, such moments begin to play a cruel joke with
developers, taking most of the time to wait for the generated part of the code (for example, in **CI/CD**).
You can hang a listener, but this is not always suitable for the reason that it begins to react to any changes in
code, which leads to frequent access to the SSD and freezes.

**Kotlin** has a very quick background [KSP](https://kotlinlang.org/docs/ksp-quickstart.html) (or
even [kapt](https://kotlinlang.org/docs/kapt.html)), which are nice to work with, unlike
from [build_runner](https://dart.dev/tools/build_runner) to **Dart**. Code generation in **Dart** so far
requires [major rethinking](https://github.com/flutter/flutter/issues/63323) to cover needs
most developers.

### Simulate user interaction

**Flutter** can be praised for its excellent support and optimization for only one platform, for which it was sharpened
in first of all - **Android**. If a native **iOS** developer is allowed to feel an application written in **Flutter**,
then he is not will get that same first-class user experience from using it. Physics and animations are just trying to
be similar to those to which the user is accustomed.

The developers still managed to seamlessly repeat the components and physics in
style [Material Design](https://m3.material.io/), for
except for the [Human Interface Guidelines](https://developer.apple.com/design/), where the physics and the components
themselves are interactions sometimes feel artificial, as if there is another layer between the finger and the button
that ruins the experience of using it. And the problem is not even in the components themselves, but in how **Flutter**
works in general on this platform.

### Different levels of performance

When it comes to web applications, development on [Flutter Web](https://flutter.dev/multi-platform/web) will require
special and rigorous approach
in [optimizing](https://medium.com/flutter/optimizing-performance-in-flutter-web-apps-with-tree-shaking-and-deferred-loading-535fbe3cd674)
, which in general will force to rethink its expediency. I would like to caution the use of this platform for
Progressive Web Apps (**PWA**) or Single Page Applications (**SPA**) development because they performance can
significantly inferior to other tools, which will ultimately negatively affect the overall user experience and
developer.

And also Flutter in the present
time [does not support](https://docs.flutter.dev/deployment/android#what-are-the-supported-target-architectures) build
project under **x86** architecture for **Android**. It is believed that the number of such devices on the market is not
so large, and with there are fewer of them every day, and the changes that need to be made to implement the compiled
files for this architecture will require a [significant](https://github.com/flutter/flutter/issues/9253) amount of work
in **Dart** compiler. You can also read more
with [supported](https://docs.flutter.dev/development/tools/sdk/release-notes/supported-platforms) platforms to
decide if Flutter is right for your purposes.

It is worth mentioning that writing an application under **watchOS** will also fail, however
there
is [possibility](https://medium.com/kbtg-life/adding-apple-watch-to-flutter-app-via-flutter-method-channel-f1443532d94e)
to embed your own native extension to the current application **Flutter**.

### Analyzer wants to be better

When several developers participate in projects, it most often happens that after the next refactoring, there are
unused fields, methods, classes, files, etc., which ultimately gives rise to an interconnected chain of dead code,
whose existence may not be immediately known.

[Analyzer](https://pub.dev/packages/analyzer) is available out of the box, it can be configured
different [rules](https://dart-lang.github.io/linter/lints/), but they are constrained by certain types
warnings/errors that prevent costly operations to find unused methods, classes, and etc.

As a partial solution to the problem, use [Dart Code Metrics](https://dcm.dev/docs/individuals/getting-started), but in
large projects it will be there is a low speed of statistical analysis, which in its own way also causes inconvenience.

## Neither here nor there

I tried to collect common working points inherent in cross-platform development in order to warn about possible
features that you may encounter as you develop a product on **Flutter**.

### Platform differences scare

In a cross-platform approach, not all designers are ready to implement **UI/UX** familiar to users for various
platforms. Usually something in between is chosen and most often the basis in design
advocates [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/guidelines/overview/)
. This often abused, leading to galactic problems.

A layout may contain a functional component that is familiar to one platform but not to another.
Therefore, some components still need to be adapted to the behavior of a particular platform in order to reduce the
negative and misunderstanding on the part of users.

### One codebase

Maintaining a cross-platform application on the same codebase is an interesting adventure, since the code is in
appearance and one, but the conditions for interaction with each platform can be completely different. The wrong
architecture can greatly increase the time for testing and support.

Here it is also worth thinking about what functionality should be checked on different platforms, and what can be done
on one - this feature must be actively used if a cross-platform tool has been chosen.

## Findings

Flutter is a modern and fast solution for developing cross-platform applications. Despite their
features, after a while everything can [change](https://github.com/flutter/flutter/wiki/Roadmap) so much that the
current disadvantages will no longer be significant, and new ones will come to replace them, because every day small
victories are achieved, which ultimately change people's perception of cross-platform tools.

Briefly summarizing the main theses of the article:

1. **Dart** is a simple language that is easier to learn than **Kotlin/Swift/Java**.
2. Widgets allow you to implement complex custom views very quickly and flexibly.
3. **Flutter** adapts with the times to hardware or software changes.
4. **Flutter** has an active developer community, various packages and programs to improve their quality.
5. Code generation and statistical code analysis require more team involvement in improving these tools.
6. Performance may vary from platform to platform, so you need to decide on the target
   purpose.
7. User experience on some platforms may differ from native.
8. Cross-platform projects, as a rule, require a special approach to building projects.

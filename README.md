# <img height="30" width="30" alt="kotlin-logging" src="https://raw.githubusercontent.com/MicroUtils/kotlin-logging/master/misc/images/kotlin-logging.png"> [kotlin-logging](https://github.com/MicroUtils/kotlin-logging) [![Build Status](https://travis-ci.org/MicroUtils/kotlin-logging.png?branch=master)](https://travis-ci.org/MicroUtils/kotlin-logging) [![Slack channel](https://img.shields.io/badge/Chat-Slack-blue.svg)](https://kotlinlang.slack.com/messages/kotlin-logging/) [![Maven Central](https://img.shields.io/maven-central/v/io.github.microutils/kotlin-logging.svg)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22io.github.microutils%22) [![Apache License V.2](https://img.shields.io/badge/license-Apache%20V.2-blue.svg)](https://github.com/MicroUtils/kotlin-logging/blob/master/LICENSE)

Lightweight logging framework for Kotlin, written in [![Pure Kotlin](https://img.shields.io/badge/100%25-kotlin-blue.svg)](https://kotlinlang.org/).  
A convenient and performant logging library wrapping [slf4j](http://www.slf4j.org/) with Kotlin extensions.

#### Call log methods, without checking whether the respective log level is enabled
```Kotlin
logger.debug { "Some $expensive message!" }
```

Behind the scenes the expensive message do not get evaluated if debug is not enabled:
```Kotlin
// This is what happens when you write the above ^^^
if (logger.isDebugEnabled) logger.debug("Some $expensive message!")
```

#### Define the logger, without explicitly specifiying the class name
```Kotlin
// Place definition above class declaration to make field static
private val logger = KotlinLogging.logger {}
```

Behind the scenes `val logger` will be created in the class, with the class/file name:
```Kotlin
// This is what happens when you write the above ^^^
val logger = LoggerFactory.getLogger("package.ClassName")
```

#### Log exceptions in a Kotlin-style
```Kotlin
// exception as first parameter with message as lambda
logger.error(exception) { "a $fancy message about the $exception" }
```

## Getting started
 
```Kotlin
private val logger = KotlinLogging.logger {} 
class FooWithLogging {
    val message = "world"
    fun bar() {
        logger.debug { "hello $message" }
    }
}
```

An `Android` example project with kotlin logging can be found in [kotlin-logging-example-android](https://github.com/MicroUtils/kotlin-logging-example-android).

## Download

**Important note:** kotlin-logging depends on slf4j-api (In the JVM artifact). In runtime, it is also required to depend on a logging implementation. More details in [how-to-configure-slf4j](http://saltnlight5.blogspot.co.il/2013/08/how-to-configure-slf4j-with-different.html). And an excelent detailed explanation in [a-guide-to-logging-in-java](https://www.marcobehler.com/guides/a-guide-to-logging-in-java). 

**Multiplatform:** See the [section below](https://github.com/MicroUtils/kotlin-logging/blob/master/README.md#multiplatform).

### Maven
```xml
<dependency>
  <groupId>io.github.microutils</groupId>
  <artifactId>kotlin-logging</artifactId>
  <version>1.6.26</version>
</dependency>
```
See full example in [kotlin-logging-example-maven](https://github.com/MicroUtils/kotlin-logging-example-maven).  

### Gradle
```Groovy
compile 'io.github.microutils:kotlin-logging:1.6.26'
```

Or alternatively, download jar from [github](https://github.com/MicroUtils/kotlin-logging/releases/latest) or [bintray](https://dl.bintray.com/microutils/kotlin-logging/io/github/microutils/kotlin-logging/) or [maven-central](http://repo1.maven.org/maven2/io/github/microutils/kotlin-logging/).

## Multiplatform

An experimental common & js support is available.  
More info on [wiki](https://github.com/MicroUtils/kotlin-logging/wiki/Multiplatform-support) and issue [#21](https://github.com/MicroUtils/kotlin-logging/issues/21).

## Overview

After seeing many questions like [Idiomatic way of logging in Kotlin](http://stackoverflow.com/questions/34416869/idiomatic-way-of-logging-in-kotlin) and [Best practices for loggers](https://discuss.kotlinlang.org/t/best-practices-for-loggers/226/15), It seems like there should be a standard for logging and obtaining a logger in kotlin. kotlin-logging provide a wrapper for slf4j api to be used by kotlin classes with the following advantages:
  - No need to write the logger and class name or logger name boileplates.
  - A straight forward way to log messages with lazy-evaluated string using lambda expression `{}`.
  - All previous slf4j implementation still can be used.

## Who is using it

- https://www.jetbrains.com/youtrack/ (https://www.jetbrains.com/help/youtrack/standalone/Third-Party-Software-Used-by-YouTrack.html)
- https://github.com/DiUS/pact-jvm
- https://github.com/AsynkronIT/protoactor-kotlin
- https://github.com/square/misk
- https://github.com/openrndr/openrndr
- https://github.com/JetBrains/xodus

And many more... (add your name above)

## FAQ

- Why not use plain slf4j? kotlin-logging has better native kotlin support. It adds more functionality and enable less boilerplates.
- Is all slf4j implementation supported (Markers, params, etc')? Yes, KLogger inherits Logger and all methods are supported.
- Is location logging possible? Yes, location awerness was added in kotlin-logging 1.4.
- When I do `logger.debug`, my IntelliJ IDEA run console doesn't show any output. Do you know how I could set the console logger to debug or trace levels? Is this an IDE setting, or can it be set in the call to KLogging()? Setting log level is done per implementation. Kotlin-logging and slf4j are just facades for the underlying logging lib (log4j, logback etc') more details [here](http://stackoverflow.com/questions/43146977/how-to-configure-kotlin-logging-logger).
- Can I access the actual logger? Yes, via `KLogger.underlyingLogger` property.

## Usage

- See [wiki](https://github.com/MicroUtils/kotlin-logging/wiki) for more examples.

It is possible to configure Intellij live template. For file level logger configure the following:
- Text template: `private val logger = mu.KotlinLogging.logger {}`.
- Applicable in `Kotlin: top-level`.

## Support

- Open an issue here: https://github.com/MicroUtils/kotlin-logging/issues
- Ask a question in StackOverflow with [kotlin-logging tag](http://stackoverflow.com/tags/kotlin-logging/info).
- Chat on Slack channel: https://kotlinlang.slack.com/messages/kotlin-logging
- Chat on Telegram channel: https://t.me/klogging

## More links

- kotlin-logging is hosted on [bintray](https://bintray.com/microutils/kotlin-logging/kotlin-logging/view) and [maven central](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22io.github.microutils%22).
- https://medium.com/@OhadShai/logging-in-kotlin-95a4e76388f2
- [kotlin-logging vs AnkoLogger for Android](https://medium.com/@OhadShai/logging-in-android-ankologger-vs-kotlin-logging-bb693671442a)
- [How kotlin-logging was published](https://medium.com/@OhadShai/no-forks-one-star-now-what-how-i-published-my-open-source-projects-8a5b5ae35d2c#.e3ygj6uf3)
- [Kotlin Logging Without the Fuss](https://realjenius.com/2017/08/31/logging-in-kotlin/)
- [DropWizard + Kotlin = Project Kronslott](https://medium.com/@davideriksson_91895/dropwizard-kotlin-project-kronslott-e2aa51b277b8)
- [Logging in Kotlin – the right approach](https://amarszalek.net/blog/2018/05/13/logging-in-kotlin-right-approach/)
- https://bednarek.wroclaw.pl/log4j-in-kotlin/

## Contributors

- Ohad Shai
- Pavel Nikitin [JetBrains]
- Christoph Gritschenberger
- Igor Manushin
- krokofant
- ravikumar-n
- Dario Seidl
- b14ckyfox
- robertfmurdock
- Corneil du Plessis

See also here: https://github.com/MicroUtils/kotlin-logging/graphs/contributors

## Contributing

Pull requests are welcome!  
[Show your ❤ with a ★](https://github.com/MicroUtils/kotlin-logging/stargazers)



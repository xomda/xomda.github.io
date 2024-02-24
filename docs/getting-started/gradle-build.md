---
outline: deep
---

# Using XOMDA with Gradle

It's easy to add XOMDA to Gradle, this automates a lot and provides a seamless experience.

## Build configuration

First of all, make sure that Gradle knows where to find the plugin. Therefore, you need to configure the plugin
management in your settings.gradle.

***settings.gradle***

```groovy
pluginManagement {
    repositories {
        mavenCentral()
        gradlePluginPortal()
    }
}
```

Next, add the Gradle plugin to your individual build files.

***gradle.build***

```groovy
plugins {
    id "org.xomda.plugin-gradle" version "latest.release"
}

repositories {
    mavenLocal()
    mavenCentral()
}

dependencies {
    // The "xomda" configuration lets you add dependencies 
    // to your build-templates
    xomda libs.log4j
}

xomda {
    // The "xomda" extensions lets you configure XOMDA
    // (see Plugin configuration below for the available options)
}
```

## Plugin configuration

### Classpath

The packages in which the plugin will look for interfaces, to create proxies from.

```groovy
xomda {
    // org.xomda.model is the default classpath
    // it's the package where the XOMDA object model is found.
    classpath ["org.xomda.model"]
}
```

### Models

By default, the models will automatically be picked up. If you want strict control over which CSV's are used as input,
this can be set by specifying the models.

```groovy
xomda {
    models ["./xomda/Model.csv"]
}
```

### Plugins & Templates

The gradle plugin can be extend in various ways, even Templates are treated like plugins.

```groovy
xomda {
    plugins ["org.xomda.model.Plugin"]
}
```

## Templates

After XOMDA is added to your Gradle build, it needs be provided with some templates
that will generate your code and assets.

All of this code needs to be added to the `src/xomda/java` directory in your project.

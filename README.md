# The ECJ Plugin for Gradle
This a plugin for using the [Eclipse JDT core](http://eclipse.org/jdt/core/) batch compler (ECJ) in [Gradle](http://gradle.org) builds.

This updated version of gradle-ecj:

- has been tested with Gradle 3.5.1
- integrates [ECJ 4.6.1](http://mvnrepository.com/artifact/org.eclipse.jdt.core.compiler/ecj)

## Usage
### Apply the plugin
To use the ECJ plugin, you must include and apply it in your build scripts:

```groovy
apply plugin: 'de.johni0702.ecj'

buildscript {
    repositories {
        mavenCentral() // for ecj
        maven { url 'https://jitpack.io' } // for this plugin
    }

    dependencies {
        // Replace master-SNAPSHOT with a specific commit hash to not always get the latest version
        classpath 'com.github.johni0702:gradle-ecj-plugin:master-SNAPSHOT'
    }
}
```

### Configuration
By default, ecj plugin use the following compilation options or flags:

  - UTF-8 encoding
  - source and target compatibility as configured for the JavaCompile task
  - compilation warning and error flags, please refer to [Eclipse JDT Help](http://help.eclipse.org/), section: `Java development user guide / Tasks / Compiling Java code / Using batch compiler`, gradle-ecj uses default values descripted in that document

You can override these default settings, by providing an `ecj` configuration closure, like this:

```groovy

ecj {
    encoding = 'utf-8'                  // default is utf-8

    warn << 'emptyBlock'                // enable a single warning, in addition to the defaults
    warn << 'enumSwitch' << 'unused'    // enable multiple warnings, in addition to the defaults
    warn -= 'typeHiding'                // suppress the given warning

    // warn = [ 'none' ]                // suppress all warnings

    //err << 'unused'                   // convert some warnings to errors
}
```

In addition, you can specify source and target compatiblity as normal gradle builds:

```groovy
sourceCompatibility = 1.6
targetCompatibility = 1.6
```

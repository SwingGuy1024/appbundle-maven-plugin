#### _Fork Note:_

_This is a fork of the useful GitHub project at https://github.com/federkasten/appbundle-maven-plugin, which is useful but out-of-date. That project was built using Java 1.6, and will not bundle applications running JDKs later than 1.9. This updates the source to Java 1.8, and fixes the minor bug that causes failure when using with Java 1.10+. Curiously, it still fails when building under Java 15, but works fine with later and earlier versions. I have tested it with all versions of Java from 8 through 17, and it only fails with Java 15. I haven't bothered to look into the Java 15 bug._

# appbundle-maven-plugin

Maven plugin that creates an Application Bundle for OS X containing all your project dependencies and the necessary metadata.

```xml
<plugin>
  <groupId>sh.tak.appbundler</groupId>
  <artifactId>appbundle-maven-plugin</artifactId>
  <version>1.2.0</version>
  <configuration>
    <mainClass>your.app.MainClass</mainClass>
  </configuration>
  <executions>
    <execution>
      <phase>package</phase>
      <goals>
        <goal>bundle</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

Package with following command,

```shell
mvn package appbundle:bundle
```

## Use Custom Info.plist and Icon

Put your custom Info.plist and Icon.icns under your maven resource paths (`src/main/resources` on default configuration).

Configure `pom.xml` like below,

```xml
<configuration>
   <mainClass>your.app.MainClass</mainClass>
   <dictionaryFile>YourCustomInfo.plist</dictionaryFile>
   <iconFile>CustomIncon.icns</iconFile>
</configuration>
```

## Embedd Java Runtime Environment

Locate the JRE or JDK on your Mac (`/Library/Java/JavaVirtualMachines/` on default configuration).

Configure `pom.xml` like below,

```xml
<configuration>
   <mainClass>your.app.MainClass</mainClass>
   <jrePath>/Library/Java/JavaVirtualMachines/jdk1.8.0_92.jdk</jrePath>
</configuration>
```

## How to create DMG

Configure `pom.xml` like below,

```xml
<configuration>
   <mainClass>your.app.MainClass</mainClass>
   <generateDiskImageFile>true</generateDiskImageFile>
</configuration>
```

## About this plugin

As you may know, Apple has dropped Java development from OS X excluding security patches.

mojo's [osxappbundle-maven-plugin](http://mojo.codehaus.org/osxappbundle-maven-plugin/) depends on Apple's Java launcher, so it does not support Java version 7 and future.

Oracle's [Java Application Bundler](https://java.net/projects/appbundler) supports other Java runtime (including Java 7, 8 and more), but it does not support maven.

I merged both and fix to work as a maven plugin that supports latest Mac OS X.

## License

Copyright 2014 - 2016, [Takashi AOKI][tak.sh] and other contributors.

Copyright 2012, Oracle and/or its affiliates.

`native/main.m` is licensed under the [GNU General Public License version 2][gnu-general-public-license-2.0].

Other files are licensed under the [Apache License, Version 2.0][apache-license-2.0].

[tak.sh]: https://tak.sh
[gnu-general-public-license-2.0]: http://www.gnu.org/licenses/gpl-2.0.html
[apache-license-2.0]: http://www.apache.org/licenses/LICENSE-2.0.html

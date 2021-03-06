# Bach.java - Java Shell Builder
 
[![jdk11](https://img.shields.io/badge/jdk-11-blue.svg)](http://jdk.java.net/11/)
[![travis](https://travis-ci.org/sormuras/bach.svg?branch=master)](https://travis-ci.org/sormuras/bach)
[![experimental](https://img.shields.io/badge/api-experimental-yellow.svg)](https://jitpack.io/com/github/sormuras/bach/master-SNAPSHOT/javadoc/)

Use Java source (in [jshell]) to build your modular Java project.

```text
    ___      ___      ___      ___
   /\  \    /\  \    /\  \    /\__\
  /::\  \  /::\  \  /::\  \  /:/__/_
 /::\:\__\/::\:\__\/:/\:\__\/::\/\__\
 \:\::/  /\/\::/  /\:\ \/__/\/\::/  /
  \::/  /   /:/  /  \:\__\    /:/  /
   \/__/    \/__/    \/__/    \/__/.java
```

> No need to be a maven to be able to use a build tool - [forax/pro](https://github.com/forax/pro)

Fast-forward to [install-jdk.sh](#install-jdksh) section.

## Execute Bach.java on-the-fly

This section will help you get started with `Bach.jsh` used as a remote `load-file` of [jshell].

##### 0. Install JDK 11 or later
Make sure you have JDK 11 or later installed and configured.
`jshell` should be executable from any directory and print its version via: 
```text
<path/> jshell --version
jshell 11.0.2
```

##### 1. Source `Bach.jsh` into JShell

Open a command shell and change into the directory containing your modular Java project. 

```text
<path/> jshell https://bit.ly/bach-jsh
```

That's all you need to build a modular Java project.

> Note: the shortened `https://bit.ly/bach-jsh` expands to https://raw.githubusercontent.com/sormuras/bach/master/src/bach/Bach.jsh

For immediate results, such as fail-fast on errors, use:

```text
jshell --execution=local https://bit.ly/bach-jsh
```

For more information what Bach.java is doing at runtime, use:

```text
jshell --execution=local -J-Debug=true https://bit.ly/bach-jsh
```

For more details consult the output of `jshell --help`.

## Bootstrap Bach.java

This section will help you get started with `Bach.java` used as single file source code Java program.

##### 0. Install JDK 11 or later
Make sure you have JDK 11 or later installed and configured.
`jshell` should be executable from any directory and print its version via: 
```text
<path/> jshell --version
jshell 11.0.2
```

##### 1. Create demo directory
Create an empty directory and change into it.
On Windows, you may open a command prompt and enter `mkdir demo & cd demo`.
On Linux and Mac OS, it could read `mkdir demo && cd demo`.

```text
<path/demo/> | // blinking cursor
```

##### 2. Download `Bach.java`
Either download a copy of [Bach.java] from GitHub manually or let [jshell] do it for you:

```text
<path/demo/> jshell https://bit.ly/boot-bach
```

> Note: the shortened `https://bit.ly/boot-bach` expands to https://raw.githubusercontent.com/sormuras/bach/master/boot.jsh

```text
<path/demo/>
.
├── bach                 // Linux/Mac OS launch script | 
├── bach.bat             // Windows batch file         |    Just convenient short-cuts for:
└── .bach                //                             \__   java .bach/master/Bach.java  
    └── master           //
        └── Bach.java    // Java Shell Builder
```

##### 3. Scaffold, build and launch demo project
Remember to prepend `./` before each `bach` command when running on Linux or Mac OS. 

```text
<path/demo/> bach scaffold
<path/demo/> bach build
<path/demo/> bach launch
```

## Available Actions

`java Bach.java help` prints

```text
Usage of Bach.java (master):  java Bach.java [<action>...]

Available default actions are:
 build        Build modular Java project in base directory.
 clean        Delete all generated assets - but keep caches intact.
 erase        Delete all generated assets - and also delete caches.
 help         Print this help screen on standard out... F1, F1, F1!
 launch       Start project's main program.
 tool         Run named tool consuming all remaining arguments:
                tool <name> <args...>
                tool java --show-version Program.java
 scaffold     Create modular Java sample project in base directory.
```

## Directory Layout

Project with one more more modules.

```text
demo
  + src
    + com.greetings
    + org.astro
    + ...
```

Project with one more more modules and test modules.

```text
demo
  + src
    + com.greetings
    + org.astro
    + ...
  + test
    + com.greetings
    + org.astro
    + ...
    + integration
    + ...
```

# install-jdk.sh

`install-jdk.sh` main purpose is to install the _latest-and-greatest_ available OpenJDK release from [jdk.java.net](http://jdk.java.net).
It supports GA releases and builds provided by [Oracle](http://www.oracle.com/technetwork/java/javase/terms/license/index.html) as well. 

#### Options of `install-jdk.sh`
```
-h|--help                 Displays this help
-d|--dry-run              Activates dry-run mode
-s|--silent               Displays no output
-e|--emit-java-home       Print value of "JAVA_HOME" to stdout (ignores silent mode)
-v|--verbose              Displays verbose output

-f|--feature 9|10|...|ea  JDK feature release number, defaults to "ea"
-l|--license GPL|BCL      License defaults to "GPL"
-o|--os linux-x64|osx-x64 Operating system identifier (works best with GPL license)
-u|--url "https://..."    Use custom JDK archive (provided as .tar.gz file)
-w|--workspace PATH       Working directory defaults to user's ${HOME}
-t|--target PATH          Target directory, defaults to first component of the tarball
-c|--cacerts              Link system CA certificates (currently only Debian/Ubuntu is supported)
```

#### How to set `JAVA_HOME` with `install-jdk.sh`

- Source `install-jdk.sh` into current shell to install latest OpenJDK and let it update `JAVA_HOME` and `PATH` environment variables:

  - `source ./install-jdk.sh` _Caveat: if an error happens during script execution the calling shell will terminate_
  
- Provide target directory path to use as `JAVA_HOME`:

  - `JAVA_HOME=~/jdk && ./install-jdk.sh --target $JAVA_HOME && PATH=$JAVA_HOME/bin:$PATH`

- Run `install-jdk.sh` in a sub-shell to install latest OpenJDK and emit the installation path to `stdout`:

  - `JAVA_HOME=$(./install-jdk.sh --silent --emit-java-home)`
  - `JAVA_HOME=$(./install-jdk.sh --emit-java-home | tail --lines 1)`

## be free - have fun
[![jsb](https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/Bachsiegel.svg/220px-Bachsiegel.svg.png)](https://wikipedia.org/wiki/Johann_Sebastian_Bach)

[jshell]: https://docs.oracle.com/en/java/javase/11/tools/jshell.html
[bach.jsh]: https://github.com/sormuras/bach/blob/master/bach.jsh
[boot.jsh]: https://github.com/sormuras/bach/blob/master/boot.jsh
[Bach.java]: https://github.com/sormuras/bach/blob/master/src/main/Bach.java
[install-jdk.sh]: https://github.com/sormuras/bach/blob/master/install-jdk.sh

# kotlin

## Environment setup

### Downloading the compiler
Every release ships with a standalone version of the compiler. We can download the latest version (kotlin-compiler-1.3.71.zip) from GitHub Releases.

### Manual Install
Unzip the standalone compiler into a directory and optionally add the bin directory to the system path. The bin directory contains the scripts needed to compile and run Kotlin on Windows, OS X and Linux.

### SDKMAN!
An easier way to install Kotlin on UNIX based systems such as OS X, Linux, Cygwin, FreeBSD and Solaris is by using SDKMAN!. Simply run the following in a terminal and follow any instructions:
```
$ curl -s https://get.sdkman.io | bash
```
Next open a new terminal and install Kotlin with:
```
$ sdk install kotlin
```
### Homebrew
Alternatively, on OS X you can install the compiler via Homebrew.
```
$ brew update
$ brew install kotlin
$ brew update
$ brew install kotlin
```

## Creating and running a first application
Create a simple application in Kotlin that displays Hello, World!. Using our favorite editor, we create a new file called hello.kt with the following:
``` kt
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

Target platform: JVMRunning on kotlin v. 1.3.70
Compile the application using the Kotlin compiler
```
$ kotlinc hello.kt -include-runtime -d hello.jar
```

The -d option indicates the output path for generated class files which may be either a directory or a .jar file. The -include-runtime option makes the resulting .jar file self-contained and runnable by including the Kotlin runtime library in it. If you want to see all available options run
```
$ kotlinc -help
```

Run the application.
```
$ java -jar hello.jar
```

Compiling a library
If you're developing a library to be used by other Kotlin applications, you can build the .jar file without including the Kotlin runtime into it.
```
$ kotlinc hello.kt -d hello.jar
```

Since binaries compiled this way depend on the Kotlin runtime you should make sure the latter is present in the classpath whenever your compiled library is used.

You can also use the kotlin script to run binaries produced by the Kotlin compiler:
```
$ kotlin -classpath hello.jar HelloKt
```

HelloKt is the main class name that the Kotlin compiler generates for the file named hello.kt.

### Using the command line to run scripts
Kotlin can also be used as a scripting language. A script is a Kotlin source file (.kts) with top level executable code.

``` kts
import java.io.File

// Get the passed in path, i.e. "-d some/path" or use the current path.
val path = if (args.contains("-d")) args[1 + args.indexOf("-d")]
           else "."

val folders = File(path).listFiles { file -> file.isDirectory() }
folders?.forEach { folder -> println(folder) }
```

To run a script, we just pass the -script option to the compiler with the corresponding script file.
```
$ kotlinc -script list_folders.kts -- -d <path_to_folder_to_inspect>
```

Since 1.3.0 Kotlin has an experimental support for scripts customization, such as adding external properties, providing static or dynamic dependencies, and so on. Customizations are defined by so-called Script definitions - annotated kotlin classes with appropriate support code. The script filename extension is used to select appropriate definition.

Properly prepared script definitions are detected and applied automatically when the appropriate jars are included in the compilation classpath. Alternatively, you can specify definitions manually using -script-templates option to the compiler:
```
$ kotlinc -script-templates org.example.CustomScriptDefinition -script custom.script1.kts
```

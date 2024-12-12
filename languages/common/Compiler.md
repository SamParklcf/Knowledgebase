# Compilers in C#, Java, and Kotlin

![Compilers in C#, Java, and Kotlin](/resources/languages/common/CompilerWithDotNETJavaAndKotlin.png)

A compiler is a special program that translates code written in a high-level programming language (like C#, Java, or Kotlin) into a lower-level language that the computer can understand and execute.

### Key Functions of a Compiler:
1. **Lexical Analysis:** The source code is broken down into tokens (keywords, variables, operators, etc.).
2. **Syntax Analysis:** The compiler checks the code against the language's grammar rules to ensure it is syntactically correct.
3. **Semantic Analysis:** It checks the meaning of the statements, ensuring that the operations are logically valid.
4. **Optimization:** The compiler improves the performance of the code, such as reducing execution time or memory usage.
5. **Code Generation:** Finally, the compiler generates the machine code or intermediate code.

The file produced by a compiler is often called a **binary file** or an **executable file**. Whereas you can read a source code and understand it, binary or executable files are not meant to be read by a human person. Only your computer can make sense of it.

In Java, the compiled code is known as **bytecode**, which runs on the **Java Virtual Machine (JVM)**. In .NET, the compiled code is called **Intermediate Language (IL)** code, which runs on the **Common Language Runtime (CLR)**.

### Example Compilers:
- **C# Compiler (Roslyn):** Compiles C# code into Intermediate Language (IL) code for the .NET framework.

- **Java Compiler (javac):** Compiles Java code into bytecode, which is executed by the Java Virtual Machine (JVM).

- **Kotlin Compiler:** Compiles Kotlin code into bytecode for the JVM, JavaScript, or native binaries using Kotlin/Native.

## [.NET Compiler](https://learn.microsoft.com/en-us/dotnet/csharp/roslyn-sdk/)
The .NET compiler is a crucial component of the [.NET ecosystem](https://dotnet.microsoft.com/en-us/learn/dotnet/what-is-dotnet), responsible for translating high-level code written in languages like C#, F#, and Visual Basic into Intermediate Language (IL) code.

### What is Intermediate Language (IL)?
Intermediate Language (IL), also known as Common Intermediate Language (CIL) or Microsoft Intermediate Language (MSIL), is a low-level programming language used by the .NET framework. It serves as the intermediate step between high-level source code and machine code.

#### Key Features of Intermediate Language (IL):
- **Platform Independence:** IL code is platform-independent, meaning it can be executed on any platform that has a compatible .NET runtime environment (e.g., Windows, Linux, macOS).

- **Language Interoperability:** IL code can be generated from different high-level languages supported by .NET (e.g., C#, F#, Visual Basic). This allows for seamless interoperability between different .NET languages.

- **[Just-In-Time (JIT) Compilation](https://www.telerik.com/blogs/understanding-net-just-in-time-compilation):** At runtime, the [Common Language Runtime (CLR)](https://learn.microsoft.com/en-us/dotnet/standard/clr) compiles IL code into native machine code specific to the platform's architecture using JIT compilation. This ensures that the application can run efficiently on the target machine.

- **Metadata:** IL code is accompanied by rich metadata that describes the types, members, and other elements defined in the code. This metadata is used by the CLR for various runtime services, including type checking, security, and garbage collection.

- **[Assembly](https://learn.microsoft.com/en-us/dotnet/standard/assembly/):** IL code, along with metadata and other resources, is packaged into an assembly. Assemblies are the building blocks of .NET applications and can be either executables (.exe) or libraries (.dll).

Some Useful links:
- [Managed execution process](https://learn.microsoft.com/en-us/dotnet/standard/managed-execution-process): Refers to how the Common Language Runtime (CLR) handles the execution of .NET applications.
- [Common type system (CTS)](https://learn.microsoft.com/en-us/dotnet/standard/base-types/common-type-system): The common type system defines how types are declared, used, and managed in the common language runtime, and is also an important part of the runtime's support for cross-language integration. 
- [What is "managed code"?](https://learn.microsoft.com/en-us/dotnet/standard/managed-code): When working with .NET, you'll often encounter the term "managed code". This article explains what managed code means and provides additional information around it.
- [Native interoperability](https://learn.microsoft.com/en-us/dotnet/standard/native-interop/): The following articles show the various ways of doing "native interoperability" in .NET.

---
So, why we should choose and use .NET? see [Why Choose .NET?](https://dotnet.microsoft.com/en-us/platform/why-choose-dotnet)


## Java Compiler

The Java compiler, known as `javac`, is a key component of the `Java Development Kit (JDK)`. Its primary role is to convert Java source code into bytecode, which can then be executed by the `Java Virtual Machine (JVM)`

### Java Runtime Environment (JRE)
The Java Runtime Environment, or JRE, is a software layer that runs on top of a computer’s operating system software and provides the class libraries and other resources that a specific Java program requires to run.

The JRE is one of three interrelated components for developing and running Java programs. The other two components are as follows:

- **The Java Development Kit, or JDK**, is a set of tools for developing Java applications. Developers choose JDKs by Java version and by package or edition—Java Enterprise Edition (Java EE), Java Special Edition (Java SE) or Java Mobile Edition (Java ME). Every JDK always includes a compatible JRE because running a Java program is part of the process of developing a Java program.

- **The Java Virtual Machine, or JVM**, runs live Java applications. Every JRE includes a default JRE, but developers can choose another that meets the specific resource needs of their applications.
The JRE combines Java code created by using the JDK with the necessary libraries required to run it on a JVM and then creates an instance of the JVM that runs the resulting program. JVMs are available for multiple operating systems, and programs created with the JRE run on all of them. In this way, the Java Runtime Environment is what enables a Java program to run in any operating system without modification.

### Java Virtual Machine (JVM)
JVM is responsible for converting bytecode to machine-specific code and is necessary in both JDK and JRE. It is also platform-dependent and performs many functions, including memory management and security. In addition, JVM can run programs that are written in other programming languages that have been converted to Java bytecode.

`Java Native Interface (JNI)` is often referred to in connection with JVM. JNI is a programming framework that enables Java code running in JVM to communicate with (that is, to call and be called by) applications that are associated with a piece of hardware and specific operating system platform. These applications are called native applications and can often be written in other languages. Native methods are used to move native code written in other languages into a Java application.

### Java Development Kit (JDK)
Java Development Kit, or JDK, is a software development kit that is a superset of JRE. It is the foundational component that enables Java application and Java applet development. It is platform-specific, so separate installers are needed for each operating system (for example, Mac, Unix, and Windows).

### How JVM, JRE and JDK work together
- **Java Development Kit (JDK)**:
    - **Purpose:** The JDK is used for developing Java applications. It includes tools for writing, compiling, and debugging Java code.
    - **Components:** It contains the `Java compiler (javac)`, `documentation generator (javadoc)`, `archiver (jar)`, and the `JRE`.
- **Java Runtime Environment (JRE)**:
    - **Purpose:** The JRE provides the environment required to run Java applications.
    - **Components:** It includes the `JVM` and `core libraries` required for running Java applications.
- **Java Virtual Machine (JVM)**:
    - **Purpose:** The JVM executes `Java bytecode`, converting it into machine code that can be executed by the host system.
    - **Components:** It includes the `class loader`, `bytecode verifier`, and `execution engine`.

As a result:
| Component | Description                           |
|-----------|---------------------------------------|
| JDK       | For developing Java applications.     |
| JRE       | For running Java applications.        |
| JVM       | For executing Java bytecode on any platform. |

```
+--------------------------------------------------------------------------------+
|                          JDK (Java Development Kit)                            |
|--------------------------------------------------------------------------------|
| - javac (Java Compiler)                                                        |
| - javadoc (Documentation Generator)                                            |
| - jar (Archiver)                                                               |
| - jdb (Debugger)                                                               |
| - Development Tools:                                                           |
|   ├── javap (Disassembler)                                                     |
|   ├── jps (Java Process Status Tool)                                           |
|   ├── jstat (Java Virtual Machine Statistics Monitoring Tool)                  |
|   ├── jstack (Java Stack Trace)                                                |
|   ├── jmap (Memory Map)                                                        |
|   ├── jshell (Java Shell/REPL)                                                 |
|   └── Other development tools                                                  |
|                                                                                |
|    +-----------------------------------------------------------------------+   |
|    |                       JRE (Java Runtime Environment)                  |   |
|    |-----------------------------------------------------------------------|   |
|    | - Core Libraries (JCL)                                                |   |
|    |   ├── java.lang, java.util, java.io, java.net, ...                    |   |
|    |   └── other core libraries                                            |   |
|    | - Native Libraries                                                    |   |
|    |   └── Native methods implemented in C or C++.                         |   |
|    | - Runtime components                                                  |   |
|    |   ├── Java Class Libraries                                            |   |
|    |   ├── Java Management Extensions (JMX)                                |   |
|    |   ├── Java Naming and Directory Interface (JNDI)                      |   |
|    |   ├── Java Sound API                                                  |   |
|    |   ├── Java 2D API                                                     |   |
|    |   ├── Java Web Start                                                  |   |
|    |                                                                       |   |
|    |   +---------------------------------------------------------------+   |   |
|    |   |                  JVM (Java Virtual Machine)                   |   |   |
|    |   |---------------------------------------------------------------|   |   |
|    |   | - Class Loader                                                |   |   |
|    |   | - Bytecode Verifier                                           |   |   |
|    |   | - Execution Engine                                            |   |   |
|    |   |   ├── JInterpreter                                            |   |   |
|    |   |   └── Just-In-Time (JIT) Compiler                             |   |   |
|    |   | - Garbage Collector                                           |   |   |
|    |   | - Java Native Interface (JNI)                                 |   |   |
|    |   | - Runtime Data Areas                                          |   |   |
|    |   |   ├── Method Area                                             |   |   |
|    |   |   ├── Heap                                                    |   |   |
|    |   |   ├── Stack                                                   |   |   |
|    |   |   ├── Program Counter (PC) Register:                          |   |   |
|    |   |   └── Native Method Stack                                     |   |   |
|    |   +---------------------------------------------------------------+   |   |
|    +-----------------------------------------------------------------------+   |
+--------------------------------------------------------------------------------+

```

Some Useful links:
- [Java Runtime Environment (JRE)](https://www.ibm.com/topics/jre): What is the Java Runtime Environment (JRE)?
- [JVM vs. JRE vs. JDK: What’s the difference?](https://www.ibm.com/think/topics/jvm-vs-jre-vs-jdk): How do JVM, JRE and JDK relate and work together in the Java development process?
- [What is JDK, JRE, and JVM](https://javacodehouse.com/blog/jdk-jre-jvm/#:~:text=These%20components%20work%20together%20to%20load%20classes%2C%20manage,Java%20applications%20to%20run%20in%20a%20platform-independent%20manner.): Let’s take a closer look at JDK, JRE, and JVM to understand the function of each.

## Kotlin Compiler

The Kotlin compiler, known as `kotlinc`, is a tool that translates Kotlin source code into bytecode that can be executed on the Java Virtual Machine (JVM). It can also compile Kotlin code to JavaScript or native binaries, allowing Kotlin to be used in a wide range of platforms and applications.


## Ahead-Of-Time (AOT) Compilation
Ahead-Of-Time (AOT) compilation is a technique where the source code is compiled into native machine code before it is executed. Unlike Just-In-Time (JIT) compilation, where code is compiled at runtime, AOT compilation translates the entire codebase into a standalone executable during the build process. This approach has several advantages, particularly in terms of performance and startup time.

#### Key Points about AOT:
- **Faster Startup:** Since the code is already compiled to native machine code, the application can start faster compared to JIT (Just-In-Time) compilation.
- **Reduced Runtime Overhead:** AOT eliminates the need for runtime compilation, reducing the overhead during execution.
- **Smaller Footprint:** The resulting native executable is typically smaller and more efficient.
- **GraalVM:** Kotlin can leverage GraalVM for AOT compilation, which provides advanced optimizations and performance improvements.

| **Language**     | **AOT Compilation Tool/Technology**         | **Description**                                                                                                  | **Official Link**                                          |
|------------------|--------------------------------------------|------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------|
| **Java**         | **GraalVM**                                 | High-performance runtime that provides AOT compilation, enabling Java applications to be compiled to native code | [GraalVM](https://www.graalvm.org/)                        |
| **.NET/C#**      | **.NET Native**                             | AOT compilation technology for UWP apps, improving performance and reducing memory usage                        | [.NET Native](https://docs.microsoft.com/en-us/dotnet/framework/net-native/) |
|                  | **ReadyToRun (R2R)**                        | Compiles .NET assemblies ahead of time to improve startup performance                                            | [ReadyToRun](https://docs.microsoft.com/en-us/dotnet/core/deploying/ready-to-run) |
| **Kotlin**       | **Kotlin/Native**                           | Compiles Kotlin code to native binaries, enabling Kotlin applications to run on platforms without the JVM        | [Kotlin/Native](https://kotlinlang.org/docs/native-overview.html) |
|                  | **GraalVM**                                 | Provides AOT compilation for Kotlin, enabling the creation of native executables from Kotlin code                | [GraalVM](https://www.graalvm.org/)                        |



## Language Equivalent Table
| **Subject**                           | **Java**                                         | **.NET/C#**                                            | **Kotlin**                                             | **Official/Unofficial Link**                                                                                                                                                    |
|---------------------------------------|-------------------------------------------------|-------------------------------------------------------|--------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Compiler**                          | Java Compiler (`javac`)                         | C# Compiler (`csc`)                                    | Kotlin Compiler (`kotlinc`)                             | [Java Compiler (`javac`)](https://docs.oracle.com/en/java/javase/17/docs/specs/man/javac.html), [C# Compiler (`csc`)](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/compiler-options/), [Kotlin Compiler (`kotlinc`)](https://kotlinlang.org/docs/command-line.html) |
| **Standard Class Library**            | Java Standard Class Library (JCL)               | .NET Standard Class Library (BCL)                      | Kotlin Standard Library                                 | [Java Class Library (JCL)](https://docs.oracle.com/javase/8/docs/api/), [.NET Standard Class Library (BCL)](https://learn.microsoft.com/en-us/dotnet/api/), [Kotlin Standard Library](https://kotlinlang.org/api/latest/jvm/stdlib/) |
| **Development Kit**                   | Java Development Kit (JDK)                      | .NET SDK                                               | Kotlin Standard Library                                 | [Java Development Kit (JDK)](https://www.oracle.com/java/technologies/javase-jdk17-downloads.html), [.NET SDK](https://docs.microsoft.com/en-us/dotnet/core/sdk/), [Kotlin Standard Library](https://kotlinlang.org/api/latest/jvm/stdlib/) |
| **Runtime Environment**               | Java Runtime Environment (JRE)                  | .NET Runtime                                           | Kotlin Runtime                                          | [Java Runtime Environment (JRE)](https://www.oracle.com/java/technologies/javase-jre8-downloads.html), [.NET Runtime](https://docs.microsoft.com/en-us/dotnet/core/runtime), [Kotlin Runtime](https://kotlinlang.org/docs/reference/native-overview.html) |
| **Virtual Machine**                   | Java Virtual Machine (JVM)                      | Common Language Runtime (CLR)                          | Kotlin/JVM                                              | [Java Virtual Machine (JVM)](https://www.oracle.com/java/technologies/javase-jvm.html), [Common Language Runtime (CLR)](https://docs.microsoft.com/en-us/dotnet/standard/clr), [Kotlin/JVM](https://kotlinlang.org/docs/reference/jvm-overview.html) |
| **Documentation Generator**           | Java Documentation Generator (`javadoc`)        | XML Documentation Comments                             | Kotlin Documentation Comments (KDoc)                    | [Java Documentation Generator (`javadoc`)](https://docs.oracle.com/en/java/javase/17/docs/specs/man/javadoc.html), [XML Documentation Comments](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/xmldoc/), [Kotlin Documentation Comments (KDoc)](https://kotlinlang.org/docs/kotlin-doc.html) |
| **Archive Tool**                      | Java Archive Tool (`jar`)                       | Assembly Packaging Tool (`al`)                         | Kotlin Archive Tool (`jar`)                             | [Java Archive Tool (`jar`)](https://docs.oracle.com/en/java/javase/17/docs/specs/man/jar.html), [Assembly Packaging Tool (`al`)](https://docs.microsoft.com/en-us/dotnet/framework/tools/al-exe-assembly-linker), [Kotlin Archive Tool (`jar`)](https://kotlinlang.org/docs/tutorials/command-line.html) |
| **Debugger**                          | Java Debugger (`jdb`)                           | Visual Studio Debugger                                 | Kotlin Debugger (`kotlin-debugger`)                     | [Java Debugger (`jdb`)](https://docs.oracle.com/en/java/javase/17/docs/specs/man/jdb.html), [Visual Studio Debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/), [Kotlin Debugger (`kotlin-debugger`)](https://kotlinlang.org/docs/native-debugging.html) |
| **Disassembler**                      | Java Disassembler (`javap`)                     | IL Disassembler (`ildasm`)                             | Kotlin Bytecode Disassembler                            | [Java Disassembler (`javap`)](https://docs.oracle.com/en/java/javase/17/docs/specs/man/javap.html), [IL Disassembler (`ildasm`)](https://docs.microsoft.com/en-us/dotnet/framework/tools/ildasm-exe-il-disassembler), [Kotlin Explorer](https://github.com/romainguy/kotlin-explorer) |
| **Process Status Tool**               | Java Process Status Tool (`jps`)                | Process Explorer                                       | Kotlin Process Status Tool                              | [Java Process Status Tool (`jps`)](https://docs.oracle.com/en/java/javase/17/docs/specs/man/jps.html), [Process Explorer](https://docs.microsoft.com/en-us/sysinternals/downloads/process-explorer), [Kotlin Process Builders Tool](https://www.slingacademy.com/article/working-with-process-builders-in-kotlin/) |
| **Virtual Machine Statistics Tool**   | Java Virtual Machine Statistics Monitoring Tool (`jstat`) | Performance Monitor                                    | Kotlin JVM Statistics Monitoring Tool                   | [Java Virtual Machine Statistics Monitoring Tool (`jstat`)](https://docs.oracle.com/en/java/javase/17/docs/specs/man/jstat.html), [Performance Diagnostic Tools](https://learn.microsoft.com/en-us/aspnet/core/performance/diagnostic-tools?view=aspnetcore-9.0), [Kotlin JVM Statistics Monitoring Tool](https://kotlinlang.org/docs/native-memory-manager.html) |
| **Stack Trace**                       | Java Stack Trace (`jstack`)                     | Exception Stack Trace                                  | Kotlin Stack Trace                                      | [Java Stack Trace (`jstack`)](https://docs.oracle.com/en/java/javase/17/docs/specs/man/jstack.html), [Exception Stack Trace](https://docs.microsoft.com/en-us/dotnet/standard/exceptions/), [Kotlin Stack Trace](https://kotlinlang.org/docs/reference/exceptions.html) |
| **Memory Map**                        | Java Memory Map (`jmap`)                        | Memory Profiler                                        | IntelliJ Profiler                                       | [Java Memory Map (`jmap`)](https://docs.oracle.com/en/java/javase/17/docs/specs/man/jmap.html), [Memory Profiler](https://docs.microsoft.com/en-us/visualstudio/profiling/memory-usage), [IntelliJ Profiler](https://blog.jetbrains.com/idea/2023/07/profile-on-the-fly-with-the-intellij-profiler/) |
| **Interactive Shell**                 | Java Shell (`jshell`)                           | Interactive C# REPL (`csi`)                            | Kotlin REPL (`kotlin-repl`)                              | [Java Shell (`jshell`)](https://docs.oracle.com/en/java/javase/17/docs/specs/man/jshell.html), [Interactive C# REPL (`csi`)](https://learn.microsoft.com/en-us/archive/msdn-magazine/2016/january/essential-net-csharp-scripting), [Kotlin REPL (`kotlin-repl`)](https://www.jetbrains.com/help/idea/kotlin-repl.html) |
| **Management Extensions**             | Java Management Extensions (JMX)               | System.Diagnostics and Performance Counters            | Kotlin Management Extensions                            | [Java Management Extensions (JMX)](https://docs.oracle.com/javase/8/docs/technotes/guides/jmx/), [System.Diagnostics and Performance Counters](https://docs.microsoft.com/en-us/dotnet/framework/debug-trace-profile/), [Kotlin Management Extensions](https://kotlinlang.org/docs/extensions.html) |
| **Native Interface**                  | Java Native Interface (JNI)                    | Platform Invocation Services (P/Invoke)                | Kotlin Native Interface (KNI)                           | [Java Native Interface (JNI)](https://docs.oracle.com/en/java/javase/8/docs/technotes/guides/jni/), [Platform Invocation Services (P/Invoke)](https://docs.microsoft.com/en-us/dotnet/standard/native-interop/pinvoke), [Kotlin Native Interface (KNI)](https://jonnyzzz.com/blog/2019/12/15/jni-kotlin/) |
| **Other Development Tools**           | Visual Studio, MSBuild, NuGet                  | IntelliJ IDEA, Gradle, Maven                            | IntelliJ IDEA, Gradle, Maven                             | [Visual Studio](https://visualstudio.microsoft.com/), [MSBuild](https://docs.microsoft.com/en-us/visualstudio/msbuild/msbuild), [NuGet](https://www.nuget.org/), [IntelliJ IDEA](https://www.jetbrains.com/idea/), [Gradle](https://gradle.org/), [Maven](https://maven.apache.org/) |

REPL: Stands for Read-Eval-Print Loop

### Compile & Run a simple 'Hello World' application
In this example we explain how a simple program can be ran in C#, Java, and Kotlin:

let's consider this simple piece of code:

#### In .NET
```cs
public class ConsoleApp
{
    static void Main(string[] args)
    {
        System.Console.WriteLine("Hello, C# World!");
    }
}
```

- Save this code in a file called: `ConsoleApp.cs`.
- Run `csc ConsoleApp.cs` command in `Developer Command Prompt` installed with Visual Studio:
    - This command will compile the source file and make an executable `ConsoleApp.exe` file for you.
- Now, you can simple type `ConsoleApp.exe` in the command prompt to run the program. 

The result would be:
```
C:\Users\SamPa\Desktop\Test>csc ConsoleApp.cs
Microsoft (R) Visual C# Compiler version 4.12.0-3.24572.7 (dfa7fc6b)
Copyright (C) Microsoft Corporation. All rights reserved.


C:\Users\SamPa\Desktop\Test>ConsoleApp.exe
Hello, C# World!
```

#### In Java
```java
public class ConsoleApp {

    public static void main(String... args) {
        System.out.println("Hello, Java World!");
    }
}
```

- Save this code in a file called: `ConsoleApp.java`.
- Compile and Run source file with (JDK v11 and later):
    - `Java ConsoleApp.java` will compile and run the program instantly (JDK v11 and later).
    - To make the `.class` file: simply run `Javac ConsoleApp.java` will make you the `ConsoleApp.class` file.

The result would be:
```
PS C:\Users\SamPa\Desktop\Test> java ConsoleApp.java
Hello, Java World!
```

#### In Kotlin
```kotlin
fun main() {
    println("Hello, Kotlin World!")
}
```

- Save this code in a file called: `ConsoleApp.kt`.
- Run `kotlinc ConsoleApp.kt` command to compile the source code.
- Run `kotlin ConsoleAppKt.class` command to run the program.

The result would be:
```
PS C:\Users\SamPa\Desktop\Test> kotlinc ConsoleApp.kt
PS C:\Users\SamPa\Desktop\Test> kotlin ConsoleAppKT.class
Hello, Kotlin World!
```

#### As a result:
| Language | Compiler          | Virtual Machine     |
|----------|-------------------|---------------------|
| C#       | `csc`             | CLR                 |
| Java     | `javac`           | JVM (Java Virtual Machine) |
| Kotlin   | `kotlinc`         | JVM (Java Virtual Machine) |


```
| Command | Purpose                    |
|---------|----------------------------|
| dotnet  | Command for CLR            |
| Java    | Command for JVM            |
```
```
PS C:\Users\SamPa\Desktop\Test> dotnet --version
9.0.101
```
```
PS C:\Users\SamPa\Desktop\Test> java -version
openjdk version "23.0.1" 2024-10-15
OpenJDK Runtime Environment (build 23.0.1+11-39)
OpenJDK 64-Bit Server VM (build 23.0.1+11-39, mixed mode, sharing)
```

## .NET Platform Evolution

- [The history of C#](https://learn.microsoft.com/en-us/dotnet/csharp/whats-new/csharp-version-history)
- [.NET Framework versions and dependencies](https://learn.microsoft.com/en-us/dotnet/framework/migration-guide/versions-and-dependencies)
- [C# language versioning](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/language-versioning)
- [.NET Standard version](https://learn.microsoft.com/en-us/dotnet/standard/net-standard?tabs=net-standard-1-0#net-standard-versions)
- [Versions of .NET](https://versionsof.net/)

## Java Platform Evolution

- [JDK Releases](https://www.java.com/releases/)
- [Java Archive](https://www.oracle.com/java/technologies/downloads/archive/)
- [The Java Version Almanac](https://javaalmanac.io/)

## Kotlin Platform Evolution

- [Release details](https://kotlinlang.org/docs/releases.html#release-details)
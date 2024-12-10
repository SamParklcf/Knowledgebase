# Project structure in C#, Java, and Kotlin

![Project structure in C#, Java, and Kotlin](/resources/languages/common/ProjectStructureInCSharpJavaAndKotlin.png)

## Why Should You Have a Project Structure?
The purpose of having a well-defined project structure in software development is to ensure that your code is organized, maintainable, and scalable. It helps developers to work more efficiently, understand the project quickly, and collaborate effectively.
- **Efficiency:** It speeds up the development process by providing a clear path for adding and locating different parts of the code.

- **Collaboration:** Makes it easier for multiple developers to work on the same project without stepping on each other's toes.

- **Maintenance:** Facilitates easier maintenance and debugging by organizing code logically.

- **Best Practices:** Encourages following best practices and standard conventions, reducing errors and inconsistencies.

### C# Project Structure
In C#, the project structure is essential for managing dependencies, configuration files, and different parts of the application. Here are some reasons why it's important:

- **Organization:** Clear separation of code, resources, and configuration files makes it easy to navigate and manage.

- **Dependency Management:** The project file (`.csproj`) helps manage dependencies and package references.

- **Build and Deployment:** The structure ensures that the build and deployment processes are smooth and automated.

The basic project structure for a C# application typically looks like this:
```
MySolution
│
├── MyProject
│   ├── bin
│   ├── obj
│   └── MyProject.csproj
│
├── MyLibrary (optional)
│   ├── bin
│   ├── obj
│   └── MyLibrary.csproj
│ 
├── MyProject.Tests
│   ├── bin 
│   ├── obj
│   └── MyProject.Tests.csproj
│
└── MySolution.sln
```

- The **solution folder (`MySolution`)** is the root directory that contains one or more projects. The solution file (`.sln`) ties all the projects together.
- [**Solution File (`MySolution.sln`):**](https://learn.microsoft.com/en-us/visualstudio/extensibility/internals/solution-dot-sln-file?view=vs-2022) This file is used by Visual Studio to load the solution and manage all the projects it contains.
- **`bin` Folder:** Contains the compiled output of your project. It is subdivided into `Debug` and `Release` folders, depending on the build configuration.
- **`obj` Folder:** Contains temporary files used during the build process. This folder is also subdivided by configuration.
- [**`MyProject.csproj`:**](https://learn.microsoft.com/en-us/aspnet/web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file) The project file that contains project-specific settings and references.

Also see: [What are solutions and projects in Visual Studio?](https://learn.microsoft.com/en-us/visualstudio/ide/solutions-and-projects-in-visual-studio?view=vs-2022)

A complete example exists my [GitHub CSharpCodeLab repo](https://github.com/SamParklcf/CSharpCodeLab)
```
CSharpCodeLab
│
├── .git
├── .github
|
├── Console
│   ├── bin
│   ├── obj
│   ├── Program.cs
│   └── Console.csproj
|
├── GitVersion.yml
|
└── CSharpCodeLab.sln
```

CSharpCodeLab.sln file content:
```
Microsoft Visual Studio Solution File, Format Version 12.00
Project("{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}") = "Console", "Console\Console.csproj", "{5A6C3A96-1B6B-42A1-A5CF-1F5B05071FC1}"
EndProject
Global
	GlobalSection(SolutionConfigurationPlatforms) = preSolution
		Debug|Any CPU = Debug|Any CPU
		Release|Any CPU = Release|Any CPU
	EndGlobalSection
	GlobalSection(ProjectConfigurationPlatforms) = postSolution
		{5A6C3A96-1B6B-42A1-A5CF-1F5B05071FC1}.Debug|Any CPU.ActiveCfg = Debug|Any CPU
		{5A6C3A96-1B6B-42A1-A5CF-1F5B05071FC1}.Debug|Any CPU.Build.0 = Debug|Any CPU
		{5A6C3A96-1B6B-42A1-A5CF-1F5B05071FC1}.Release|Any CPU.ActiveCfg = Release|Any CPU
		{5A6C3A96-1B6B-42A1-A5CF-1F5B05071FC1}.Release|Any CPU.Build.0 = Release|Any CPU
	EndGlobalSection
EndGlobal
```
Console.csproj file content:
```xml
<Project Sdk="Microsoft.NET.Sdk">

    <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>net9.0</TargetFramework>
        <ImplicitUsings>enable</ImplicitUsings>
        <Nullable>enable</Nullable>
        <AssemblyName>CodeLab.CSharp.Console</AssemblyName>
        <RootNamespace>CodeLab.CSharp.Console</RootNamespace>
        <LangVersion>default</LangVersion>
        <GeneratePackageOnBuild>true</GeneratePackageOnBuild>
    </PropertyGroup>

    <ItemGroup>
      <PackageReference Include="GitVersion.MsBuild" Version="6.0.5">
        <PrivateAssets>all</PrivateAssets>
        <IncludeAssets>runtime; build; native; contentfiles; analyzers; buildtransitive</IncludeAssets>
      </PackageReference>
    </ItemGroup>

</Project>
```

Program.cs file content:
```cs
namespace CodeLab.CSharp.Console;

class Program
{
    static void Main(string[] args)
    {
        System.Console.WriteLine("Hello, World!");
    }
}
```
### Java Project Structure
Java projects typically follow a standard structure that is crucial for several reasons:

- **Convention Over Configuration:** Adhering to standard conventions (like `src/main/java` and `src/main/resources`) reduces configuration overhead.
**
- **Modularity:** Clear separation of source code, resources, and test code enhances modularity and maintainability.

- **Build Tools:** Tools like Maven and Gradle rely on specific project structures to automate builds, testing, and deployments.

The basic project structure for a Java application typically looks like this:

**For Gradle Projects:**
```
MyJavaProject
│
├── build.gradle(.kts)
├── settings.gradle(.kts)
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── mycompany
│   │   │           └── App.java
│   │   ├── resources
│   └── test
│       ├── java
│       │   └── com
│       │       └── mycompany
│       │           └── AppTest.java
│       └── resources
└── build
```

- **Project Root Directory (MyJavaProject):** The root directory contains all the project files and subdirectories.
- **`build.gradle(.kts)` / `settings.gradle(.kts)`:** (Gradle) Configuration files that define the build logic and dependencies for the project.
- **src:** The source directory where all the source code and resources are stored.
    - **`main/java`:** Contains the main application code. The package structure follows the standard Java convention (e.g., com.mycompany).
    - **`main/resources`:** Contains application resources such as configuration files, property files, and other non-code assets.
    - **`test/java`:** Contains test code. The package structure mirrors the main/java directory to keep the test code organized.
    - **`test/resources`:** Contains test resources such as test-specific configuration files and data.
- **`build`:** These directories are used by Maven or Gradle to store the compiled bytecode, JAR files, and other build outputs.

A complete example exists my [GitHub JavaCodeLab repo](https://github.com/SamParklcf/JavaCodeLab)
```
JavaCodeLab
│
├── .git
├── .github
|
├── .gradle
|
├── codelab.java.console
|   ├── build
|   ├── src
│   │    ├── main
│   │    │   ├── java
│   │    │   │   └── codelab.java.console
│   │    │   │       └── Main.java
│   │    │   └── resources
│   │    └── test
│   │        ├── java
│   │        |   └── codelab.java.console
│   │        │       └── MainTest.java
│   │        └── resources
│   └── build.gradle.kts  
|
├── gradle
|   ├── wrapper 
|   └── libs.versions.toml
|
├── GitVersion.yml
|
├── gradlew
├── gradlew.bat
|
└── settings.gradle.kts
```

libs.versions.toml file content:
```toml
[versions]
junit = "5.11.3"

[libraries]
junit-bom = { group = "org.junit", name = "junit-bom", version.ref = "junit" }
junit-jupiter = { group = "org.junit.jupiter", name = "junit-jupiter", version.ref = "junit" }
```

settings.gradle.kts file content:
```kotlin
include("codelab.java.console")
```

build.gradle.kts file content:
```kotlin
import groovy.json.JsonSlurper

plugins {
    application
}

application {
    mainClass = "codelab.java.console.Main"
    applicationName = "codelab.java.console.app"
}

repositories {
    mavenCentral()
}

group = "codelab.java"

//Setting this version ensures that if any issues occur during versioning, it will use the default version.
version = "0.1.0-SNAPSHOT"


//----------------------------------- Semantic Versioning / Continues Integration -------------------------------------
val gitVersionJsonFilePath = "../gitversion.json" // make a const for the 'gitversion.json' file path.

// Register an executable task to generate the 'gitversion.json' file using the 'gitversion' CLI.
tasks.register<Exec>("gitVersionOutputJSon") {
    commandLine("sh", "-c", "gitversion /output json > $gitVersionJsonFilePath")
}

/*
Register a task that depends on 'gitVersionOutputJson' to run after it.
This task will read the 'gitversion.json' file, extract the 'SemVer' key value, and assign it to the 'project.version'.
*/
tasks.register("parseGitVersion") {
    dependsOn("gitVersionOutputJSon")
    doLast {
        val jsonSlurper = JsonSlurper()
        val gitVersionFile = file(gitVersionJsonFilePath)
        val gitVersion = jsonSlurper.parse(gitVersionFile) as Map<*, *>
        project.version = gitVersion["SemVer"].toString()
        println("---> Project version set to: ${project.version}")
    }
}

/*
Configure the 'Jar' task to depend on the 'parseGitVersion' task. This ensures that every time the 'Jar' task runs,
it first executes the 'parseGitVersion' task to determine the project version.
Also assigns the title and version of the .jar file to the 'project.name' and 'project.version'.
*/
tasks.withType<Jar>().configureEach {
    dependsOn("parseGitVersion")
    from(sourceSets["main"].output)
    manifest {
        attributes(
            "Implementation-Title" to project.name,
            "Implementation-Version" to project.version
        )
    }
}
//---------------------------------------------------------------------------------------------------------------------

dependencies {
    testImplementation(platform(libs.junit.bom))
    testImplementation(libs.junit.jupiter)
}

tasks.test {
    useJUnitPlatform()
}

tasks.jar {
    manifest {
        attributes["Main-Class"] = application.mainClass
    }
}
```

Main.java file content:
```java
package codelab.java.console;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

### Kotlin Project Structure
Kotlin projects, often integrated with Android development, benefit from a well-defined structure:

- **Consistency:** Following the standard Kotlin/Android project structure ensures consistency across different projects.

- **Build Optimization:** Tools like Gradle use the structure to optimize builds and manage dependencies effectively.

- **Scalability:** A clear structure allows for easy scaling of the project by adding new modules, features, and components.

The basic project structure for a Kotlin application typically looks like this:

**For Gradle Projects:**
```
MyKotlinProject
│
├── build.gradle.kts
├── settings.gradle.kts
├── src
│   ├── main
│   │   ├── kotlin
│   │   │   └── com
│   │   │       └── mycompany
│   │   │           └── Main.kt
│   │   ├── resources
│   └── test
│       ├── kotlin
│       │   └── com
│       │       └── mycompany
│       │           └── MainTest.kt
│       └── resources
└── build
```

- **`build.gradle.kts`:** The build script file for Gradle using Kotlin DSL. It contains configuration details used by Gradle to build the project.
- **`settings.gradle.kts`:** The settings script file for Gradle, also using Kotlin DSL. It defines the configuration for the entire Gradle build, including project dependencies.
- **`src`:** The source directory where all the source code and resources are stored.
    - **`main/kotlin`:** Contains the main application code. The package structure follows the standard Kotlin convention (e.g., com.mycompany).
    - **`main/resources`:** Contains application resources such as configuration files, property files, and other non-code assets.
    - **`test/kotlin`:** Contains test code. The package structure mirrors the main/kotlin directory to keep the test code organized.
    - **`test/resources`:** Contains test resources such as test-specific configuration files and data.
- **`build`:** This directory is used by Gradle to store the compiled bytecode, JAR files, and other build outputs.

A complete example exists my [GitHub KotlinCodeLab repo](https://github.com/SamParklcf/KotlinCodeLab)
```
KotlinCodeLab
│
├── .git
├── .github
|
├── .gradle
|
├── codelab.kotlin.console
|   ├── build
|   ├── src
│   │    ├── main
│   │    │   ├── kotlin
│   │    │   │   └── codelab.kotlin.console
│   │    │   │       └── Main.java
│   │    │   └── resources
│   │    └── test
│   │        ├── kotlin
│   │        |   └── codelab.kotlin.console
│   │        │       └── MainTest.java
│   │        └── resources
│   └── build.gradle.kts 
|
├── gradle
|   ├── wrapper 
|   └── libs.versions.toml  
|
├── GitVersion.yml
|
├── gradlew
├── gradlew.bat
|
└── settings.gradle.kts
```

libs.versions.toml file content:
```toml
[versions]
kotlin = "2.1.0"

[libraries]
kotlin-test = { group = "org.jetbrains.kotlin", name = "kotlin-test", version.ref = "kotlin" }
```

settings.gradle.kts file content:
```kotlin
include("codelab.kotlin.console")
```

build.gradle.kts file content:
```kotlin
import groovy.json.JsonSlurper

plugins {
    kotlin("jvm") version libs.versions.kotlin
    application
}

application {
    mainClass = "codelab.kotlin.console.MainKt"
    applicationName = "codelab.kotlin.console.app"
}

repositories {
    mavenCentral()
}

//Setting this version ensures that if any issues occur during versioning, it will use the default version.
version = "0.1.0-SNAPSHOT"

//----------------------------------- Semantic Versioning / Continues Integration -------------------------------------
val gitVersionJsonFilePath = "../gitversion.json" // make a const for the 'gitversion.json' file path.

// Register an executable task to generate the 'gitversion.json' file using the 'gitversion' CLI.
tasks.register<Exec>("gitVersionOutputJSon") {
    commandLine("sh", "-c", "gitversion /output json > $gitVersionJsonFilePath")
}

/*
Register a task that depends on 'gitVersionOutputJson' to run after it.
This task will read the 'gitversion.json' file, extract the 'SemVer' key value, and assign it to the 'project.version'.
*/
tasks.register("parseGitVersion") {
    dependsOn("gitVersionOutputJSon")
    doLast {
        val jsonSlurper = JsonSlurper()
        val gitVersionFile = file(gitVersionJsonFilePath)
        val gitVersion = jsonSlurper.parse(gitVersionFile) as Map<*, *>
        project.version = gitVersion["SemVer"].toString()
        println("---> Project version set to: ${project.version}")
    }
}

/*
Configure the 'Jar' task to depend on the 'parseGitVersion' task. This ensures that every time the 'Jar' task runs,
it first executes the 'parseGitVersion' task to determine the project version.
Also assigns the title and version of the .jar file to the 'project.name' and 'project.version'.
*/
tasks.withType<Jar>().configureEach {
    dependsOn("parseGitVersion")
    from(sourceSets["main"].output)
    manifest {
        attributes(
            "Implementation-Title" to project.name,
            "Implementation-Version" to project.version
        )
    }
}
//---------------------------------------------------------------------------------------------------------------------

dependencies {
    testImplementation(libs.kotlin.test)
}

tasks.test {
    useJUnitPlatform()
}

tasks.jar {
    manifest {
        attributes["Main-Class"] = application.mainClass
    }
    /*
    This iterates over all the files in the compileClasspath configuration and unpacks them into the JAR.
    This includes all the dependencies needed to run your application.
    */
    configurations["compileClasspath"].forEach {
        from(zipTree(it.absoluteFile))
    }
    /*
    This strategy ensures that if there are duplicate files (like META-INF files) across the dependencies,
    they are all included rather than causing a conflict.
    */
    duplicatesStrategy = DuplicatesStrategy.INCLUDE
}
```

Main.kt file content:
```kotlin
package codelab.kotlin.console

fun main(args: Array<String>) {
    println("Hello World!")
}
```

### Language Equivalent Table

| Component                     | C#                                      | Java                                    | Kotlin                                  |
|-------------------------------|-----------------------------------------|-----------------------------------------|-----------------------------------------|
| **Main Project Directory**    | Solution                                | Project                                 | Project                                 |
| **Project Directory**         | Project                                 | src/main/java                           | src/main/kotlin                         |
| **Namespace/Package**         | Namespace                               | Package                                 | Package                                 |
| **Entry Point**               | Program.cs                              | Main.java                               | Main.kt                                 |
| **Build/Configuration File**  | MyProject.csproj                        | pom.xml (Maven) / build.gradle(.kts) (Gradle) | build.gradle.kts (Gradle)               |
| **Source Code Directory**     | src                                     | src/main/java                           | src/main/kotlin                         |
| **Resources Directory**       | Properties                              | src/main/resources                      | src/main/resources                      |                       | src/main/webapp                         |
| **Test Directory**            | Project.Tests                           | src/test/java                           | src/test/kotlin                         |
| **Compiled Output**           | bin/Debug, bin/Release                  | target (Maven) / build (Gradle)         | build                                   |
| **Temporary Build Files**     | obj/Debug, obj/Release                  | target/classes (Maven) / build/classes  | build/classes                           |
| **Configuration File**        | App.config (optional)                   | application.properties                  | application.properties                  |
| **Build Tool**        | MSBuild                   | gradle/maven                  | gradle/maven                  |
---

C# and Java have many similarities. As you learn C#, you can apply much of the knowledge you already have from programming in Java: see [Roadmap for Java developers learning C#](https://learn.microsoft.com/en-us/dotnet/csharp/tour-of-csharp/tips-for-java-developers)

---
**Note:** In this section, we aimed to outline the fundamental structure that every project should adhere to. However, it's important to note that the project structure will significantly evolve based on the required architecture.

### Widely Applicable Architectures
Here are some best practices about the architectures:
- Onion Architecture
- Clean Architecture
- Domain-Driven Design
- Microservices Architecture
- Model-View-Controller (MVC)
- Event-Driven Architecture
- Model-View-ViewModel (MVVM)
- Model-View_Presenter (MVP)
- Component-Based Architecture
- Service-Oriented Architecture
- Model-View-Intent (MVI)
- And so on... 

#### Language-Specific Considerations
While the concepts of these architectures are widely applicable, the implementation details may vary:

- **C#:** Often used with frameworks like `ASP.NET`, `WPF`, and `MAUI`, which provide specific patterns and tools aligned with these architectures.

- **Java:** Commonly paired with frameworks like `Spring`, `Java EE`, and `Android`, which have their own conventions and best practices for implementing these architectures.

- **Kotlin:** Frequently used with Android development, leveraging libraries and tools tailored for Kotlin, such as `Kotlin Coroutines` for concurrency and `Jetpack Compose` for UI.


Here are some useful links to follow:
- [Awesome Software Architecture](https://awesome-architecture.com/): Curated list of awesome articles and resources to learn and practice software architecture, patterns and principles. this repository will be updated continuously, keep yourself up to date.
- [awesome-software-architecture-resources](https://github.com/RAKMAK/awesome-software-architecture-resources): A curated list of awesome articles, videos, and other resources to learn and practice software architecture, patterns, and principles.
- [Software Architecture Books & Resources](https://www.reddit.com/r/softwarearchitecture/comments/16usw23/megathread_software_architecture_books_resources/?rdt=34052): This thread is dedicated to the often-asked question, 'what books or resources are out there that I can learn architecture from?' The list started from responses from others on the subreddit, so thank you all for your help.
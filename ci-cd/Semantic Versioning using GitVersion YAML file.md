# Semantic Versioning using GitVersion YAML file for your .NET, Java, and Kotlin projects' CI/CD

![Semantic Versioning using GitVersion YAML file for your .NET, Java, and Kotlin projects' CI/CD](/resources/ci-cd/SemanticVersioningUsingGitVersionYAMLFile-Cover.png)

## What is Semantic Versioning?

***[Semantic Versioning (SemVer)](https://semver.org/)*** is a versioning scheme that uses a three-part version number: MAJOR.MINOR.PATCH. It helps to convey meaning about the underlying changes in a new release:

- ***MAJOR*** version changes indicate incompatible API changes.
- ***MINOR*** version changes add functionality in a backward-compatible manner.
- ***PATCH*** version changes are for backward-compatible bug fixes.

## What is GitVersion?

***[GitVersion](https://gitversion.net/)*** is a tool that automatically generates a semantic version number based on your Git history. It analyzes your repository's commit history and branch structure to determine the appropriate version number.

All you need to do is:

1. Prepare your desired `GitVersion.yml` file.
2. Add it to the root path of your project/Module directory, where your `.git` directory exists.
3. Prepare the build:
    - If you are using .NET:
        - Add [`GitVersion.MsBuild`](https://www.nuget.org/packages/GitVersion.MsBuild) NuGet package to your every single project in the solution.
    - If you are using Java/Kotlin:
        - Add the necessary tasks to create the `gitversion.json` file by [`GitVersion CLI`](https://gitversion.net/docs/usage/cli/arguments) to parse the right version for your projects.
4. Boom! Build your solution (in .NET) / main module (in Java/Kotlin)

### Preparing `GitVersion.yml`
You can find a detailed explanation for configuring your `GitVersion.yml` file on [gitversion.net](https://gitversion.net/docs/reference/configuration). Alternatively, you can use the sample I prepared based on `GitFlow (GitFlow/v1)` available in my [GitHub](https://gist.github.com/SamParklcf/b84008129adf0b842c94454af15d08e6):

```yml
# This configuration uses GitFlow branching model which always has a main and a develop branch. see: https://nvie.com/posts/a-successful-git-branching-model/
# This configuration follows Semantic Versioning. see: https://semver.org/
# A good explanation on semantic versioning: https://semantic-versioning.org/
workflow: GitFlow/v1
assembly-versioning-scheme: MajorMinorPatchTag
assembly-file-versioning-scheme: MajorMinorPatchTag
assembly-informational-format: "{FullSemVer}"
tag-prefix: "[vV]?"
version-in-branch-pattern: (?<version>[vV]?\d+(\.\d+)?(\.\d+)?).*
major-version-bump-message: '\+semver:\s?(breaking|major)'
minor-version-bump-message: '\+semver:\s?(feature|minor)'
patch-version-bump-message: '\+semver:\s?(fix|patch)'
no-bump-message: '\+semver:\s?(none|skip)'
tag-pre-release-weight: 60000
commit-date-format: "yyyy-MM-dd"
merge-message-formats: {}
update-build-number: true
semantic-version-format: Strict #ensure that versions are consistently formatted and that the versioning process remains predictable and reliable. This can be particularly important for projects with strict dependency management and release policies.
strategies:
  - Fallback #This strategy is used when no other versioning strategy applies. It ensures that a version is always generated, even if no tags or commits indicate a version change.
  #ConfiguredNextVersion: #This strategy allows you to manually specify the next version number. It's useful for scenarios where you want to control the versioning process directly.
  - MergeMessage #This strategy increments the version based on the merge commit message. If the message contains specific keywords (e.g., "version bump"), the version number is incremented accordingly.
  #- TaggedCommit #This strategy uses the commit tagged with a version number to determine the next version. It's useful for projects that follow a strict versioning policy based on tags.
  - TrackReleaseBranches #This strategy tracks branches that are used for releases. It ensures that the version number is incremented based on the commits made to these branches.
  - VersionInBranchName #This strategy extracts the version number from the branch name itself. It's useful for projects that use branch names to indicate version information.
branches:
......
```

### Add `GitVersion.yml` to the root path of your project
By placing the `GitVersion.yml` file in the root of your solution (in .NET) or main module (in Java/Kotlin), the `gitversion` CLI will use it for all sub-projects or sub-modules.

#### In Java/Kotlin:
You can find the sample projects in my repo at GitHub:
- [Check JavaCodeLab project](https://github.com/SamParklcf/JavaCodeLab/tree/feature/setup)
- [Check KotlinCodeLab project](https://github.com/SamParklcf/KotlinCodeLab/tree/feature/setup)
- [Check CSharpCodeLab project](https://github.com/SamParklcf/CSharpCodeLab/tree/feature/setup)

Java project:

![Java GitVersion.yml file placement](/resources/ci-cd/GitVersionYAMLFileForJava.png)

Kotlin project:

![Kotlin GitVersion.yml file placement](/resources/ci-cd/GitVersionYAMLFileForKotlin.png)

CSharp project:

![CSharp GitVersion.yml file placement](/resources/ci-cd/GitVersionYAMLFileForCSharp.png)

### Prepare Java/Kotlin project to generate `gitversion.json` file
**Note:** This guide is intended to use with `build.gradle.kts`. You can modify it to suit your needs.
1. Open `build.gradle.kts` file for every single project and inject this code block into it:
```kotlin
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
```

**Note:** To ensure the `gitVersionOutputJSon` task is runnable, you need to install `GitVersion CLI` on your operating system and set it as an `environment variable`.

This block of code should be placed between your { `plugins`, `repositories`, ... } and { `dependencies`, ...}.

finally you would have something like this:
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
The Semantic Versioning block generates the `gitversion.json` file in the root path of your project:

![GitVersion Json File](/resources/ci-cd/GitVersionJsonFileForJava.png)
![GitVersion Json File](/resources/ci-cd/GitVersionJsonFileForKotlin.png)

If you look at the file, you should have something like this:
```json
{
  "AssemblySemFileVer": "0.1.0.1",
  "AssemblySemVer": "0.1.0.1",
  "BranchName": "feature/setup",
  "BuildMetaData": 5,
  "CommitDate": "2024-12-05",
  "CommitsSinceVersionSource": 5,
  "EscapedBranchName": "feature-setup",
  "FullBuildMetaData": "5.Branch.feature-setup.Sha.f2526f6ec73f6753bc39a17edd186c3114f34872",
  "FullSemVer": "0.1.0-setup.1+5",
  "InformationalVersion": "0.1.0-setup.1+5",
  "Major": 0,
  "MajorMinorPatch": "0.1.0",
  "Minor": 1,
  "Patch": 0,
  "PreReleaseLabel": "setup",
  "PreReleaseLabelWithDash": "-setup",
  "PreReleaseNumber": 1,
  "PreReleaseTag": "setup.1",
  "PreReleaseTagWithDash": "-setup.1",
  "SemVer": "0.1.0-setup.1",
  "Sha": "f2526f6ec73f6753bc39a17edd186c3114f34872",
  "ShortSha": "f2526f6",
  "UncommittedChanges": 3,
  "VersionSourceSha": "",
  "WeightedPreReleaseNumber": 30001
}

```

Let's take a look at what happens when you run the `build` task:
- `gitVersionOutputJSon` task tries to make the `gitversion.json` file based on your project changes..
- `parseGitVersion` task tries to parse the generated JSON file and take the 'SemVer' and assign it to the `project.version`
- Now gradle uses this property to generate the `jar` file.


### Preparing the build in .NET
1. Add [`GitVersion.MsBuild`](https://www.nuget.org/packages/GitVersion.MsBuild) NuGet package to every single project in the solution:

![GitVersion.MSBuild Nuget Package](/resources/ci-cd/GitVersionMSBuildNuGetPackage.png)


**Congrats!** you finish the local project side.

### Let's explore the build server setup on GitHub to ensure the CI process runs smoothly

- **[For Java/Kotlin:](https://gist.github.com/SamParklcf/c42e433ad36e89987617f7d4568cee6e)**
```yml
name: Java Kotlin Build and Test With Gradle

on: [push, pull_request, workflow_dispatch]

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: read

    steps:
      - name: Checkout
        uses: actions/checkout@v4.2.2
        with:
          fetch-depth: 0

      - name: Set up JDK 23
        uses: actions/setup-java@v4.5.0 #https://github.com/actions/setup-java
        with:
          java-version: '23'
          distribution: 'oracle'

      - name: Install GitVersion 6.0.5 for Gradle
        run: |
          wget -q -O gitversion.tar.gz https://github.com/GitTools/GitVersion/releases/download/6.0.5/gitversion-linux-x64-6.0.5.tar.gz
          mkdir gitversion_extracted
          tar -xzf gitversion.tar.gz -C gitversion_extracted
          ls -R gitversion_extracted
          sudo mv gitversion_extracted/gitversion /usr/local/bin/gitversion
          sudo chmod +x /usr/local/bin/gitversion
      - name: Setup Gradle 8.11.1
        uses: gradle/actions/setup-gradle@v4 #https://github.com/gradle/actions/blob/main/docs/setup-gradle.md#build-with-a-specific-gradle-version
        with:
          gradle-version: '8.11.1'

      - name: Build with Gradle 8.11.1
        run: gradle build --scan --warning-mode all

  dependency-submission: # See: https://github.com/gradle/actions/blob/main/dependency-submission/README.md

    runs-on: ubuntu-latest

    permissions:
      contents: write

    steps:
      - name: Checkout
        uses: actions/checkout@v4.2.2

      - name: Set up JDK 23
        uses: actions/setup-java@v4.5.0
        with:
          java-version: '23'
          distribution: 'oracle'

      - name: Setup Gradle 8.11.1
        uses: gradle/actions/setup-gradle@v4
        with:
          gradle-version: '8.11.1'

      - name: Setup Gradle Wrapper
        run: gradle wrapper

      - name: Generate and submit dependency graph
        uses: gradle/actions/dependency-submission@v4
```

- **[For .NET:](https://gist.github.com/SamParklcf/6b846cba562401be4f27858357989a01)** 
```yml
name: .NET Build and Test

on: [push, pull_request, workflow_dispatch]

jobs:
  build_and_Test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout #https://github.com/GitTools/actions/blob/main/docs/examples/github/gitversion/setup.md
        uses: actions/checkout@v4.2.2
        with:
          fetch-depth: 0

      - name: Install GitVersion 6.x #https://github.com/GitTools/actions/blob/main/docs/examples/github/gitversion/setup.md
        uses: gittools/actions/gitversion/setup@v3.0.3
        with:
          versionSpec: '6.x'
          preferLatestVersion: true

      - name: Determine Version #https://github.com/GitTools/actions/blob/main/docs/examples/github/gitversion/execute.md
        uses: gittools/actions/gitversion/execute@v3.0.3
        with:
          useConfigFile: true
          updateAssemblyInfo: true

      - name: Setup .NET 9 #https://github.com/actions/setup-dotnet
        uses: actions/setup-dotnet@v4.1.0
        with: 
          dotnet-version: '9.0.x'

      - name: Available projects
        run: dotnet sln list

      - name: Restore dependencies
        run: dotnet restore

      - name: Build
        run: dotnet build --no-restore

      - name: Test
        run: dotnet test --no-build --verbosity normal
```
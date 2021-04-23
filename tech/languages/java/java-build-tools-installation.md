---
title: Java build tools
subsection: java
order: 2
---

# Java build tools

The most popular build tools used by millions of Java developers are packaged in official Fedora repositories. This page contains information on how easy it is to install them.

## Maven installation

[Maven](https://maven.apache.org/) is probably the most popular build tool in Java world these days. To install it, simply type:

```
$ sudo dnf install maven
```

## Ant+Ivy installation

Last but not least, still quite popular duo [Ant+Ivy](http://ant.apache.org/ivy/) can be installed simply by typing:

```
$ sudo dnf install ant apache-ivy
```

## Creating a Maven project

### Using `mvn` command-line tool

Use the command from the [Maven quick start guide](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html):

```
$ mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4 -DinteractiveMode=false
```

The project that is created follows the [Maven Project Structure](http://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html). Initially you should see the `src` directory when you explore the project directory. You will also notice that your project directory has a file, the [pom.xml](https://maven.apache.org/pom.html) in it, this is your Maven project file that defines your build, and how you will transition through the Maven build [lifecycles](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html). 

The sample application created by the Maven archetype contains a single "Hello World" application (jar).

The `target` directory will be created after the first compilation: run 

```
$ mvn compile
```

This directory is where your compiled artifacts, or generated outputs (from builds) are stored. Its best to think of this directory as a temp space, used to store the outputs from a build. 

### Creating a git repo

This project folder is not a Git repository yet. Create a git repo:
```
$ cd my-app
$ git init
```

If you run `git status` in the created `my-app` directory, you will see that the `target` directory is still part of your git repository. It is a best practice not to include this in your version control system, so it is recommended that you create a [gitignore](https://git-scm.com/docs/gitignore) file, add this directory and anything under it as ignored files.

A good starter `.gitignore` file for Maven projects can be found on [Github](https://github.com/github/gitignore/blob/master/Maven.gitignore). Download it into your repo with:

```
$ curl https://raw.githubusercontent.com/github/gitignore/master/Maven.gitignore -o .gitignore
```

The `src` directory is the start of your source directory structure, and under this directory you will see typically see any number of [package directories](http://docs.oracle.com/javase/tutorial/java/package/managingfiles.html) (example: `main`). If you have tests, you will find them in the `test` directory.



<!-- TODO: once content for Scala programming language is created, mention here that it's also possible to use SBT to build Java projects + link to corresponding Scala section. -->

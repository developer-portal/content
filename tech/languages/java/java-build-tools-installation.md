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

## DevAssistant is obsolete, use it for reference only

You can get started with Maven by using [DevAssistant](/tools/devassistant/about.html) to create a simple project, simply type (after you have DevAssistant setup and installed):   

```
da --debug crt java maven -n Dev_Sample
```

The project that is created (Example: Dev_Sample), roughly follows the [Maven Project Structure](http://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html) but does not contain all of the directories or files. Initially you should see 2 directories (`src` and `target`) when you explore the project directory. You will also notice that your project directory has a file, the [pom.xml](https://maven.apache.org/pom.html) in it, this is your Maven project file that defines your build, and how you will transition through the Maven build [lifecycles](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html). 

The `target` directory is created as part of your initial project build, triggered by DevAssistant command above. This directory is where your compiled artifacts, or generated outputs (from builds) are stored. Its best to think of this directory as a temp space, used to store the outputs from a build. 

- Note: if you run `git status` in the created `Dev_Sample` directory, you will see that the `target` directory is not part of your git repository. Its a best practice to not include this in your version control system, so its recommended that you create a [gitignore](https://git-scm.com/docs/gitignore) file, add this directory and anything under it as ignored files.

The `src` directory, is the start of your source directory structure, and under this directory you will see typically see any number of [package directories](http://docs.oracle.com/javase/tutorial/java/package/managingfiles.html)(Example: main), and the template testing framework (using junit). 

The sample application created, as part of the DevAssisttant project creation, creates a single application (jar) from the `main.java.org.devassistant.maven.Main` class. It also creates a single test (test if a boolean is true), that is run when a build happens. 

<!-- TODO: once content for Scala programming language is created, mention here that it's also possible to use SBT to build Java projects + link to corresponding Scala section. -->

---
title: Static Analysis
subsection: c
order: 6
---

# Static Analysis
Static analysis is a technique of analyzing programs without executing them.
It is often used in compilers for code optimizations and producing warnings.
We have several static analyzers in Fedora that can be used to automatically
detect programming mistakes by analyzing source code only.  Especially for
statically typed languages (like C/C++), static analyzers can significantly
help us to catch various classes of bugs in our code before it ever runs.

There are various optional diagnostics in GCC that could be enabled by
```-W...``` compilation flags.  Besides the built-in GCC diagnostic, we can use
standalone static analyzers for C/C++, such as
[Cppcheck](http://cppcheck.sourceforge.net/),
[Clang](http://clang-analyzer.llvm.org/), or
[Sparse](https://sparse.wiki.kernel.org).  There are also static
analyzers for dynamically typed languages -- for
example [ShellCheck](http://www.shellcheck.net/about.html), which analyzes
shell scripts, or [Pylint](http://www.pylint.org/), which analyzes programs
written in Python.

## Using csbuild to analyze C/C++ programs
In order to make it easier to use static analyzers by C/C++ developers, there
is a utility named ```csbuild``` that runs static analyzers in background fully
transparently.  You can install csbuild by dnf, which will also pull the needed
static analyzers as dependencies:

```
sudo dnf install csbuild
```

Its usage is as easy as:

```
csbuild -c 'make ...'
```
... where you replace ```make ...``` by the actual command you use to compile
your project.  By running the above command, you will get extended diagnostic
produced by GCC and the output of Cppcheck and Clang analyzers for the modules
that were (re)compiled during the build.

## Differential scans
If your project is tracked in a git repository, you can use csbuild for
differential scans to check for added (or fixed) bugs between a pair of git
revisions.  For example, before you push your commits in the master branch of
your project to a public git repository, you can first check that you are not
introducing any new bugs in those commits:

```
csbuild -g origin/master..master -c "make ..."
```

In this mode, only bugs introduced between the specified pair of revisions are
reported.  You can use the ```--print-fixed``` option to print also bugs that
were fixed between the pair of revisions.  You can also use the
```---git-bisect``` option to find the exact commit that introduced a new bug:

```
csbuild -g origin/master..master -c "make clean && make ..." --git-bisect
```

The complexity of the search algorithm is logarithmic, which means that for a
search in 1024 commits, only 10 builds are needed.  For these options to work,
you need to use a build command that fully rebuilds all sources.

## Travis CI and static analysis
[Travis CI](https://travis-ci.org/) is a freely avilable CI (Continuous
Integration) service, which is integrated with [GitHub](https://github.com/).
If you have a repository on GitHub, you can configure Travis CI to run a series
of tests each time you push new commits into your repository.  This is normally
used to monitor that the latest version of your project can be built from
sources and that its test-suite still passes (if you have one).

csbuild allows you to run static analyzers automatically whenever you push new
commits to your repository so that, if new bugs are detected by static
analysis, you are notified by an e-mail from Travis CI.  You can achieve this
by using the ```--gen-travis-yml``` option of csbuild to generate a
configuration file for Travis CI.  In this mode, you also need to use the
```--install``` option to specify dependencies required for build of your
project.  It expects a space-separated list of packages that can be installed on
Ubuntu LTS.  The command in the following example generates a Travis CI
configuration file to enable static analysis for [curl](http://curl.haxx.se/):

```
csbuild -c "./buildconf && ./configure && make -j5" \
        --install libtool --git-bisect \
        --gen-travis-yml > .travis.yml
```

Then you commit the generated file ```.travis.yml``` to your repository and
push:

```
git add .travis.yml
git commit -m "notify me about newly introduced bugs"
git push
```

Finally, you enable Travis CI for your GitHub repository at
[https://travis-ci.org/profile](https://travis-ci.org/profile) and you are done!

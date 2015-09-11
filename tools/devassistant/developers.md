---
title: For Developers
page: devassistant
order: 2
---

This section is intended for developers that want to make their own assistants
for their project. If you want to learn how to use DevAssistant, go to
[Tutorials](#tutorials.md). Furthermore, the tutorial is significantly
condensed to be as clear and short as possible. For a much more detailed
tutorial, visit [DevAssistant
documentation](http://doc.devassistant.org/en/latest/developer_documentation/create_assistant.html).

# Write Your Own Assistant

If you contribute to a software project, especially one that many contributors
work on, you can benefit greatly from having an assistant set suited precisely
to your project. Likewise, if you like working with a language that is not yet
covered by [existing assistants](https://dapi.devassistant.org/all/), you can
create a new assistant package that does just that.

While you can make your assitants without packaging and distributing them (more
on that
[here](http://doc.devassistant.org/en/latest/developer_documentation/create_assistant/yaml/tutorial.html)),
we strongly suggest you start creating the whole package (DAP—DevAssistant
Package), and this tutorial takes that into consideration.

If you have DevAssistant installed (to check that, see the [installation
guide](#about.md/#Installing DevAssistant on Fedora)), see if you also have the
DAP package for creating other DAPs. This command should return a line with
information about an installed package named `dap`:

    $ da pkg list --installed | grep dap

If the command returned nothing, either install the package through Fedora's
DNF:

    $ sudo dnf install devassistant-dap-dap

or install the DAP locally for your account only:

    $ da pkg install dap

## Create the package

With all the necessary bits and pieces in place, you can start with creating
the package. Go to your working directory and create a new DAP with the desired
[assistants roles](#about.md/##Assistants) prepared (any of`create`, `tweak`,
`prepare`, `extras`):

    $ da create dap --name foo --crt --prep

The above command creates a directory named `dap-foo` (`dap-` is added due to
naming conventions), and in it a structure with assistants, in this case for
the creation and preparation of projects. There are also directories for
documentation, auxiliary files, and icons (useful for making your assistant
accessible to GUI users).

    dap-foo/
    ├── assistants/
    │   ├── crt/
    │   │   └── foo.yaml
    │   └── prep/
    │       └── foo.yaml
    ├── doc/
    │   └── foo/
    │       └── LICENSE
    ├── files/
    │   └── foo/
    ├── icons/
    │   └── foo/
    └── meta.yaml

The file `meta.yaml` contains metadata about the whole package, the author, and
dependencies. It is important you fill it in
[properly](http://doc.devassistant.org/en/latest/developer_documentation/create_assistant/packaging_and_distributing.html#meta-yaml-explained)
because otherwise you will not be able to package it or publish it on the
[DevAssistant Package Index (DAPI)](https://dapi.devassistant.org). Do not
forget to include a licence of your choice too.

## Write a Sample Assistant

An assistant is a [YAML
file](http://doc.devassistant.org/en/latest/developer_documentation/create_assistant/yaml.html)
with several sections that describe what it does.  In this chapter, we will go
through the typical ones. The full description can be found in the
[documentation](http://doc.devassistant.org/en/latest/developer_documentation/create_assistant/yaml.html).
If you do not like the idea of writing a YAML assistant, you can [use a
language of your
choice](http://doc.devassistant.org/en/latest/developer_documentation/create_assistant/pingpong.html)
for most parts of the assistant (so far only Python support is implemented).

### Header

The header information contains data displayed to users when looking for the
right assistant for their use case.

    fullname: Assistant for Foo Bar Baz
    description: More verbose description of what it does

### Dependencies

The dependencies section describes what packages should be installed by which
package manager. There are many package managers supported, to name a few: Yum,
DNF, gem, pip, pacman, and more. To indicate that e. g. RPM packages `baz` and
`qux`, and a Python (pip) package `foobar` should be installed, form the
dependencies section the following way:

    dependencies:
      - rpm: ['baz', 'qux']
      - pip: ['foobar']

### Arguments

To allow the user to provide input, arguments are needed. Either you specify
the argument properties yourself (in this case, a mandatory argument named
`name` specified by flags `-n` and `--name`):

    args:
      name:
        flags: [-n, --name]
        required: True
        help: A short description of the argument

or you can use a definition from a so-called
[snippet](http://doc.devassistant.org/en/latest/developer_documentation/create_assistant/yaml/snippets.html)
(think of it a header file or a library), in this case a snippet named
`common_args`:

    args:
      name:
        use: common_args

If you use a defintion from a snippet, you must declare a dependency on it in
the `meta.yaml` file in your package (by adding a `dependencies:
['common_args']` to the file.

Arguments' values are automatically stored in a variable of the same name, in
this case, `$name`.

### Files

You assistant may include other files than just the assistants, for example
those that will be placed in the project's directory on creation. To include a
file named `foo.txt`, copy it into the `files` subdirectory in the DAP's
structure, and add a reference to it to the `files` section in the assistant
under an appropriate handle, in this case e. g. `foo`:

    files:
      foo: &foo
        source: foo.txt

Elsewhere in the assistant, the file will be only referred to by its handle
`foo`. Repeating the handle name with `&` is necessary due to technical
limitations of the current implementation.

### Run Section

The run section is a procedural section where you put the commands that should
be executed during the assistant's run. Typically, you create a directory to
put the project into, copy the files from the `files` section, start services,
emit messages to be logged, or push the code to GitHub. For the full list of
possible commands, have a look at [run section
reference](http://doc.devassistant.org/en/latest/developer_documentation/create_assistant/yaml/run_sections_reference.html).

The run section consists of a list of commands (each item of the list starting
with `-`), their arguments, and other logic. To illustrate this better, let us
have a look at this sample run section:

    run:
    - setup_project_dir:
        from: name
        on_existing: fail
    - cl: cd $contdir/$topdir
    - $date~: $(date)
    - log_i: Run started at $date
    - cl: cp *foo .
    - if $(test -f foo.txt):
        - log_i: Foo.txt copied successfully
    - else:
        - log_e: Error copying Foo.txt

As fairly obvious, the command `setup_project_dir` creates the project dir from
the variable `name`, as specified, and will fail if the directory already
exists. What is not obvious is that in addition to that, it sets the variables
`$contdir` (the directory one level above the project directory) and `$topdir`
(the project directory), which will be used shortly.

The next command, `cl: cd $contdir/$topdir`, executes a shell command that
changes the current working directory to the project's directory. If you want
to simply execute calls in the shell, call the `cl` (*command line*) command.
If you want to assign the result of the call to a variable or check the result
in an `if` clause, use the `$(...)` syntax like in shell instead, as shown on
the next line. The line in question, `$date~: $(date)`, is a variable
assignment. In this case, it assigns the result of calling the shell command
`date` into a variable named `$date`. The tilde (`~`) is there so that
`$(date)` is interpreted. If it was not there, the assigned value would be the
string `$(date)` itself. Generally speaking, all commands can be appended with
the tilde to force interpreting the value on the right side of the colon.

The commands `log_i`, `log_w`, and `log_e` are all used for logging on
different levels (`INFO`, `WARNING`, `ERROR`). Unlike the first two, `log_e`
also stops the execution of the assistant as it means fatal error that
DevAssistant can not recover from.

The last thing not yet covered in this little example is the `if..else`
construct. It works just how you expect it to, except not only can you query
shell command results (`test -f foo.txt`) in the example, but also the values
of variables (`if defined $variable`, for example) and
[more](http://doc.devassistant.org/en/latest/developer_documentation/command_reference.html).

### The whole assistant

The sections that were described above add up to a simple little assistant that
looks like this:

    fullname: Assistant for Foo Bar Baz
    description: More verbose description of what it does

    dependencies:
      - rpm: ['baz', 'qux']
      - pip: ['foobar']

    args:
      name:
        use: common_args

    files:
      foo: &foo
        source: foo.txt

    run:
    - setup_project_dir:
        from: name
        on_existing: fail
    - cl: cd $contdir/$topdir
    - $date~: $(date)
    - log_i: Run started at $date
    - cl: cp *foo .
    - if $(test -f foo.txt):
        - log_i: Foo.txt copied successfully
    - else:
        - log_e: Error copying Foo.txt

Please, bear in mind that this is a small and non-exhaustive example of what
can be done with DevAssistant. To see the whole set of options and a more
complicated example, visit the [Create Your Own
Assistant](http://doc.devassistant.org/en/latest/developer_documentation/create_assistant.html)
section of the DevAssistant Documentation.

## Packaging

When the assistants are created, you can prepare the whole package for
distribution, which is done by executing:

    $ da tweak dap pack

in the source directory. This command creates a properly formatted DAP from the
files present, and saves it under the name `dap-NAME-VERSION.dap`. To ensure
the DAP meets all the requirements for distribution, run:

    $ da pkg lint ./dap-NAME-VERSION.dap

The command outputs a list of problems that prevent the DAP from being used in
distribution. After the problems are sorted out, you can install the DAP by
running:

    $ da pkg install ./dap-NAME-VERSION.dap

or upload it to the [DAPI](https://dapi.devassistant.org) for others to
consume. Use the command:

    $ da extra dap upload -d ./dap-NAME-VERSION.dap

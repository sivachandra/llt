# Understanding the compilation step

## The simplest compile command?

One can invoke the compiler in many ways. The most popular way is probably
by clicking the **Build** or **Run** button on an IDE like VS Code. However,
in this document we will focus on invoking the compiler from the command line
as it is simpler to explore the various options one can pass to the compiler.
We will use C++, a compiled language, to learn about the different ways to
compile source files.

Let us start with a simple *Hello World* program listed in a source file named
`hello_word.cpp` as follows:

```
#include <iostream>

int main() {
  std::cout << "Hello, World!" << std::endl;
  return 0;
}
```

If you are not familiar with C++, I suggest going through any beginner C++
tutorial available on the internet. In this document, our focus is on what
happens when one tries to compile a C++ source file and not on the C++ language.
Let's compile the above file using the following command in a terminal window:

```
$> clang++ hello_world.cpp
```

This is the simplest command line that one can use to compile a source file
into an executable program. On Linux, the above command will produce an
executable program with name `a.out`. If you run this executable, it will
print `Hello, World!` on your terminal screen. The command has two parts. The
first part is the name of the compiler, which in our case is `clang++`. The
second part is the name of the source file, which in our case is
`hello_word.cpp`. So, by invoking the command, we instructed `clang++` to
compile `hellow_world.cpp` and produce an executable.

## Compiling to produce object files

Let us now modify the compilation command a little bit:

```
$> clang++ -c hello_world.cpp
```

The difference is the additional `-c` option compared to the above simple
command. Because of this option, instead of producing an executable, the 
compiler will produce an *object file* named `hello_world.o`. The `-c` option
to `clang++` instructed it to only compile the source file and to not follow it
up with a *link* step to produce an executable. This also means that in the
previous section, we used the term *compile* loosely to mean both compile and
link. Conventionally, when there is not much ambiguity about what we actually
mean by *compile*, we tend to use to mean *compile and link*.

There are two new terms that were used here: *object file* and *link*. Let us
try to understand these two terms in more detail.

### Object files

When you instruct a compiler to only compile a source file, it will take that
source file and produce an object file. On Linux, object files typically have
the extention `.o`. These object files contain the machine instructions
corresponding to the C++ source in the input source file (the file
`hello_world.cpp` in our example.) The object files cannot themselves be
executed (or run) like how we could run the `a.out` file from the previous
section.

### Linking

The object files produced by the compile action have to be *linked* via a link
to produce an executable. One can link the `hello_world.o` object file by
running the following command:

```
$> clang++ hello_world.o
```

When we run this command, `clang++` recognizes the `.o` extension of the input
source file and performs only the link step. As before, the link step produces
a file named `a.out` which can be executed to print the `Hello, World!` message.

Why a link step is necessary at all is beyond the scope of this document. We will
discuss it in detail in a different document.

## The compiler is actually a driver

Even though we referred to `clang++` as a compiler in the previous sections, 
we used `clang++` to peform the compile step as well as to peform the link step.
To be technically correct, we should actually call `clang++` as **a compiler
driver**. The reason is that `clang++` isn't the one actually performing the
compile or the link steps. It is a driver program which calls the real compiler
and the real linker to perform the compile and link steps. It calls the real
compiler and/or the real linker based on the options and types of inputs we pass
to it.

## Multiple source files

One can compile and link multiple source files with a single invocation of the
compiler driver.


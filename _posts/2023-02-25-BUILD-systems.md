---
title: BUILD Systems
published: true
---

Recently, I have been working on making internal code buildable in open source, and the process has made me fall in love with build systems! 

But what exactly is a build system? you might ask.

At its core, a build system is a tool for managing software development projects. Some online articles describe it as a tool for "translating" source code files, such as Java and Python, into executable programs that can run. There are many types of build systems available, including popular ones like Make, CMake, and Gradle. These build systems have their own syntax and rules for managing dependencies and compiling code.

I have been working with [Bazel](https://bazel.build/) to build Android code in open source, and I find it beautiful! Bazel is an open source build system developed by Google. It uses `build graphs` to manage dependencies between source code files, allowing Bazel to build only the necessary parts of the code. This feature was handy for my project, as we only planned to build a portion of the system in open source.

While Bazel by itself is absolutely fascinating, I was more intrigued by how (mostly) seamless it was to migrate code from an internal build system to Bazel and have things build the same. It felt like an exciting engineering problem to ensure that code in general, is build system-agnostic (As long as you have the right dependencies). So I did some further research into the underlying principles for build systems and found the following concepts to be crucial:

- File Context: For small programs in a single file or a handful of files in a single directory, it is easy to execute code by directly invoking the compiler (e.g. `javac *.java` to build Java source files in the current directory). However, once you have to pull dependencies from unrelated directories, things get a lot more complex. Build systems use file context to manage dependencies, determine the code needed to build a specific target, and compile files in the correct order. This context can also help users save time and reduce build errors by detecting invalid dependencies or circular dependencies in a larger system.

- Reliable Artifacts: In Java, we have JAR files, an encoding mechanism for bundling multiple Java files and resources. With JARs, you can effectively distribute tagged and hashable versions of a piece of software for reliable and deterministic behavior. This ability simplifies relying on third-party code and guarantees consistency in build output. In my context, I was able to pull in equivalent external dependencies for my project from open source repositories to ensure the program does not behave differently from the internal version.

- Build Tools: Finally, build systems must have multi-language support. These build tools help determine how different parts of the system built with varying languages can come together and interact. In [task-based](https://bazel.build/basics/task-based-builds) build systems, users are free to define these build tools, such as specifying executor scripts and how the program gets built. However, for [artifact-based](https://bazel.build/basics/artifact-based-builds) build systems like Bazel, this is abstracted away to achieve better build performance.

Build systems continue to fascinate me and there are even more interesting concepts to them such as Incremental and Distributed build support. I might explore these in a later post. 
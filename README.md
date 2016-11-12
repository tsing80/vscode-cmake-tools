# CMake Tools

CMake Tools provides the native developer a full-featured, convenient, and
powerful configure+build workflow for CMake-based projects within the
Visual Studio Code editor.

This extension itself *does not* provide language support for the CMake
scripting language. For that I recommend [this extension](https://marketplace.visualstudio.com/items?itemName=twxs.cmake).

## What's New?

For users who were using the `cmake.generator.<platform>`-style configuration options,
those options has been renamed to the form `cmake.<platform>.generator` to fit
a new naming convention for config options. Read about the 0.7.3 update for more
information.

### **0.7.4**:
  - **Target debugging is now enabled by default, and has been assigned a
    `ctrl+f5` keybinding**
  - Fix issue with being able to switch back to the `all` target
  - Fix issue with CTest output being garbled without line breaks
  - Fix hang when build tools generate large amounts of output.*
  - **New** make-shift progress bar for build progress (supports Make and Ninja).*
  - Options to control what output parsers are enabled*

  \* Special thanks goes to [bbosnjak](https://github.com/bbosnjak) for these ones!


## Issues? Questions? Feature requests?

**PLEASE**, if you experience any issues, create an issue on
[the GitHub page](https://github.com/vector-of-bool/vscode-cmake-tools)!
I'm only one person with no QA team, so I can't test all the different possible
configurations you may have, but I'll gladly help anyone fix issues relating to
this extension.

## `initialBuildType` Deprecation Notice:

- **The ``initialBuildType`` configuration option is no longer supported**. This
  option was buggy and surprisingly hard to implement correctly. Now, if CMake
  Tools doesn't know how you would like to configure your project, it will ask
  you on the first configure what [build variant](https://github.com/vector-of-bool/vscode-cmake-tools/blob/develop/docs/build_variants.md) you would
  like to configure with. The default variants are the same old CMake build
  types most users are familiar with.

# Getting Started

CMake Tools provides several pieces of functionality to make it easier to work
with CMake-based projects within Visual Studio Code. For example, it adds a
"CMake: Build" command to the command palette, which is bound to the ``F7``
key by default.

By default, CMake Tools assumes that you place your CMake build tree in a
subdirectory of the source tree called ``build``. This can be configured with
the ``cmake.buildDirectory`` configuration option, which can be set globally or
on a per-project basis. If you try to build but do not yet have a build
directory, CMake Tools will prompt you to configure the project.

CMake Tools uses a configuration setting ``cmake.configureSettings`` to define
options to pass to CMake when configuring the project. In this way, build
settings can be stored as part of the project in ``settings.json`` in the
``.vscode`` directory.

## The Status bar

![CMake Status Bar Items](images/statusbar_marked.png)

CMake Tools provides a few buttons on the statusbar:

1.  The name of the current project, the current build type (Debug, Release, etc.),
    and the current status of CMake Tools. Click this button to change the active
    configuration.
2.  A build button. Click this button to build the default target. Quickly invoking
    a build is also bound to the ``F7`` key by default. While building, this button
    changes into a _stop_ button. Clicking the stop button will cancel the
    currently running build/configure process.
3.  The default/active target. This is the target that will be invoked if run
    the build command. Clicking on this button will let you select a different
    target to be built by default.
4.  The Target Debugging launcher (must be explicitly enabled, se below).
5.  The active debug target (must be explicitly enabled).
6.  The CTest results button. Click this button to rebuild and run CTest tests.

CMake Tools will also show the most recent line of CMake output as a status message
to the right of the buttons. Invoking a command will open the CMake/Build output
channel, where the progress and output of the build/configure commands can be
seen.

## Target Debugging

*Target Debugging*, allows developers to easily use the Visual
Studio Code Debugger with their CMake targets without having to write a
``launch.json``. [Read about enabling and using the feature here](https://github.com/vector-of-bool/vscode-cmake-tools/blob/develop/docs/target_debugging.md).

## Compiler Diagnostics

CMake Tools also parses the compiler output of GCC, Clang, and MSVC looking for
diagnostics. It will populate the diagnostics for files which produce any warnings
or errors.

## CTest Tests

CMake Tools also features integration with CTest, both executing and displaying
results, even inline in the editor:

![Failing Check](images/failed_check.png)

(Currently, only Catch test output is supported)

## Other Features

- Command to quickly generate a very basic CMakeLists.txt and C++ source file.
- Set CMake configuration values in ``settings.json``.
- Provides diagnostics for CMake scripts.
- Quickly jump into CMakeCache.txt

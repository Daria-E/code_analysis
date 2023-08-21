# Code analysis and cross-compiling on amd64 for arm64: TinyCalculator

[TinyCalculator](https://github.com/BaseMax/TinyCalculator) is a simple CLI calculator, written purely in C++.

I started with a fresh, fully-updated (as of time of writing) amd64 VM of Ubuntu 22.04 LTS. Installed `cppcheck`, retrieved the app's source code, and ran the following command from the source root directory:

``cppcheck . 2> err.txt``

This recursively checks the current folder, prints the progress onscreen and writes any errors to `err.txt`. `err.txt` is empty, so there are no errors, warnings, or notes.

I then compiled the app for x64, to check if it works: `g++ main.cpp -o calc`. Running the `calc` binary works.

Installed the arm64 cross-compiler for c++: `sudo apt install g++-aarch64-linux-gnu`

Finally - compiled for arm64 with `aarch64-linux-gnu-g++ main.cpp -o calc_arm`. Trying to run `calc_arm` results in `cannot execute binary file: Exec format error` - which means `calc_arm` is indeed of a different architecture than our working environment.


# More complex program: CherryTree

[CherryTree](https://github.com/giuspen/cherrytree) is a note-taking app that supports nested notes, attachments, TeX, images, charts and more. It's considerably more complex than TinyCalculator...

Similarly to the previous time, I retrieved the source code and ran cppcheck. The error log (`cherrytree_errors.html`) is attached.

Sadly, I failed to compile the app for ARM64. While the cross-compiler is available, it seems some dependencies of the program don't play nicely with cross-compiling (namely the FMT library, and other TeX-related dependencies). This was expected, as CherryTree's documentation highly recommends building on the target arch. This can be accomplished by running an ARM64 VM on the x86_64 host, and building there.

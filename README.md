# Code analysis and cross-compiling on amd64 for arm64: TinyCalculator

[TinyCalculator](https://github.com/BaseMax/TinyCalculator) is a simple CLI calculator, written purely in C++.

We started with a fresh, fully-updated (as of time of writing) amd64 VM of Ubuntu 22.04 LTS. We then installed `cppcheck`, retrieved the app's source code, and ran the following command from the source root directory:

``cppcheck . 2> err.txt``

This recursively checks the current folder, prints the progress onscreen and writes any errors to `err.txt`. `err.txt` is empty, so there are no errors, warnings, or notes.

We then compiled the app for x64, to check if it works: `g++ main.cpp -o calc`. Running the `calc` binary works.

We installed the arm64 cross-compiler for c++: `sudo apt install g++-aarch64-linux-gnu`

Finally - compiled for arm64 with `aarch64-linux-gnu-g++ main.cpp -o calc_arm`. Trying to run `calc_arm` results in `cannot execute binary file: Exec format error` - which means `calc_arm` is indeed of a different architecture than our working environment.

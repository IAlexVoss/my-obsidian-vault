# Steps:

First, you need **raylib** (C++ lib for creating some simulations, --v 5.0+, any digital)

## Instruments:

Windows: [https://www.raylib.com/](https://www.raylib.com/) 
or -> use vcpkg:
```Console
vcpkg install raylib
```

Compilator: g++/clang++ (standard C++17).

In CMakeLists.txt for raylib need:
```cmake
cmake_minimum_required(VERSION 3.11)
project(SimCanvas)

find_package(raylib REQUIRED)
add_executable(sim main.cpp)
target_link_libraries(sim raylib)
```


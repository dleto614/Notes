Commands to get a project ready to go:

```
vcpkg new --application
vcpkg add port fmt 
vcpkg install # Install all packages ported above
vcpkg integrate install # Run this following command to link cmake to vcpkg
```

To generate build files with CMake:

```
# either

mkdir build && cd build && cmake ../

# or

mkdir build && cmake -B build && cd build
```

To build and run:

```
make && ./HelloWorld
```


------

Example cmake file for cpr:

```
cmake_minimum_required(VERSION 3.31)

project(cprtest)

include(FetchContent)
FetchContent_Declare(cpr GIT_REPOSITORY https://github.com/libcpr/cpr.git)
FetchContent_MakeAvailable(cpr)

add_executable(main main.cpp)

target_link_libraries(main PRIVATE cpr::cpr)
```

------

Example cmake file for nlohmann-json/nlohmann_json:

```
cmake_minimum_required(VERSION 3.31)

project(json-test)

add_executable(main main.cpp)

find_package(nlohmann_json CONFIG REQUIRED)
target_link_libraries(main PRIVATE nlohmann_json::nlohmann_json)
```

To compile:

```
cmake -B build -DCMAKE_TOOLCHAIN_FILE=/home/alex/Documents/Tools/vcpkg/scripts/buildsystems/vcpkg.cmake
```
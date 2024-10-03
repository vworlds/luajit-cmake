# luajit-cmake

CMake build-system for LuaJIT. This is meant for using LuaJIT as a library
in an existing CMake project.

This repository does not contain LuaJIT, but it manages downloading it from the configured repo and tag.

This is a fork from [Janbuller/luajit-cmake](https://github.com/Janbuller/luajit-cmake) and tuned to make sure `LUAJIT_UNWIND_EXTERNAL` is set for Linux.

I've tried to backport as much as possible from [zhaozg](https://github.com/zhaozg/luajit-cmake)'s original version and recent improvements.

Additionally, I have made it easy to select from the parent project what fork of LuaJIT and version is compiled.

## How to use:

Include the following in your `CMakeLists.txt` file:

```cmake
# Set the LuaJIT repository and tag to compiled by luajit-cmake
set(LUAJIT_GIT_REPOSITORY "https://github.com/openresty/luajit2")
set(LUAJIT_GIT_TAG "v2.1-20240815")

# Include the luajit-cmake project with the custom repository and tag
# luajit-cmake will download and compile the above fork of LuaJIT
FetchContent_Declare(
    luajitcmake
    GIT_REPOSITORY https://github.com/vworlds/luajit-cmake.git
    GIT_TAG master  # Replace with the desired commit/tag
)

FetchContent_MakeAvailable(luajitcmake)

# Link the LuaJIT library
target_link_libraries(${YOUR_PROJECT} PUBLIC libluajit)
```

(Replace `master` with the desired tag in this repo. Alternatively, just fork the repo and manage your own tags)

With the above, you are actually including in your `CMakeLists.txt` this project, which in turn downloads, configures and compiles the LuaJIT repo and git tag specified by `LUAJIT_GIT_REPOSITORY` and `LUAJIT_GIT_TAG`.

The above example points to OpenResty's fork. To use the original LuaJIT repo, simply modify the above to:

```cmake
set(LUAJIT_GIT_REPOSITORY "https://github.com/LuaJIT/LuaJIT")
set(LUAJIT_GIT_TAG "v2.1.ROLLING")
```

Forked from [https://git.sr.ht/~lasse/luajit-cmake](https://git.sr.ht/~lasse/luajit-cmake), which in turn was forked from
[https://github.com/zhaozg/luajit-cmake](https://github.com/zhaozg/luajit-cmake),
with significant portions removed as they were not needed for lasse's purposes.

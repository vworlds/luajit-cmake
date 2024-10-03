# luajit-cmake

CMake build-system for LuaJIT. This is meant for using LuaJIT as a library
in an existing CMake project.

This repository does not contain LuaJIT, but it manages downloading it from the configured repo and tag.

This is a fork from [https://git.sr.ht/~lasse/luajit-cmake](https://git.sr.ht/~lasse/luajit-cmake) and modified slightly to make it work for our project, which means it is not guaranteed to work for anything other than x64 architecture.

## Changes made:

### In LuaJIT.cmake:

- Removed Unwind library detection code, because we want to force `LUAJIT_UNWIND_EXTERNAL` so stack is not messed up in C++
- Added Lua 5.2 compatibility flag

## How to use:

Include the following in your `CMakeLists.txt` file:

```cmake
# Set the LuaJIT repository and tag to be used by the luajit-cmake project
set(LUAJIT_GIT_REPOSITORY "https://github.com/openresty/luajit2")
set(LUAJIT_GIT_TAG "v2.1-20240815")

# Include the luajit-cmake project with the custom repository and tag
FetchContent_Declare(
    luajitcmake
    GIT_REPOSITORY https://github.com/vworlds/luajit-cmake.git
    GIT_TAG master  # Replace with the desired commit/tag
)

FetchContent_MakeAvailable(luajitcmake)
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
with significant portions removed as they are not needed for lasse's purposes.

cmake_minimum_required(VERSION 3.27)

include(FetchContent)

# Provide default values, but allow overriding via the parent project
option(LUAJIT_GIT_REPOSITORY "https://github.com/openresty/luajit2")
option(LUAJIT_GIT_TAG "v2.1-20240815")

FetchContent_Declare(
  luajitsrc
  GIT_REPOSITORY ${LUAJIT_GIT_REPOSITORY}
  GIT_TAG ${LUAJIT_GIT_TAG}
)

FetchContent_MakeAvailable(luajitsrc)

set(LUAJIT_DIR ${luajitsrc_SOURCE_DIR})

if(LUAJIT_DIR)
  project(luajit)
  include(LuaJIT.cmake)
  if (PARENT_DIRECTORY)
    set(LUA_TARGET luajit PARENT_SCOPE)
    set(LUA_LIBRARIES libluajit PARENT_SCOPE)
  endif()
else()
  message(FATAL_ERROR "LUAJIT_DIR not set")
endif()

cmake_minimum_required(VERSION 3.16)

project(microui-sdl3
    VERSION 0.1.0
    DESCRIPTION "SDL3 renderer backend for microui"
    LANGUAGES C
)

set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

if(CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
    set(MICROUI_SDL3_IS_TOP_LEVEL TRUE)
else()
    set(MICROUI_SDL3_IS_TOP_LEVEL FALSE)
endif()

option(MICROUI_SDL3_BUILD_EXAMPLES "Build example programs" ${MICROUI_SDL3_IS_TOP_LEVEL})
option(MICROUI_SDL3_BUILD_TESTS "Build tests" ${MICROUI_SDL3_IS_TOP_LEVEL})

# SDL3 
find_package(SDL3 CONFIG QUIET)

if(NOT SDL3_FOUND)
    message(STATUS "microui-sdl3: system SDL3 not found, fetching via FetchContent")

    include(FetchContent)

    set(MICROUI_SDL3_SDL_TAG "release-3.4.16" CACHE STRING
        "SDL3 git tag to fetch when no system SDL3 is found")

    # Keep SDL's own build from dragging its tests/examples into ours, and
    # pin its link type explicitly so it doesn't vary by SDL's own default.
    set(SDL_SHARED OFF CACHE BOOL "" FORCE)
    set(SDL_STATIC ON CACHE BOOL "" FORCE)
    set(SDL_TEST_LIBRARY OFF CACHE BOOL "" FORCE)
    set(SDL_EXAMPLES OFF CACHE BOOL "" FORCE)

    FetchContent_Declare(
        SDL3
        GIT_REPOSITORY https://github.com/libsdl-org/SDL.git
        GIT_TAG        ${MICROUI_SDL3_SDL_TAG}
        GIT_SHALLOW    TRUE
    )
    FetchContent_MakeAvailable(SDL3)
endif()

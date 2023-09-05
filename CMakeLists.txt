# CMake configuration for linuxdeployqt
# Not meant to replace the qmake build system, but for use with CMake based IDEs.

cmake_minimum_required(VERSION 3.2)

project(linuxdeployqt)

# set version and build number
set(VERSION 1-alpha)
if("$ENV{TRAVIS_BUILD_NUMBER}" STREQUAL "")
    set(BUILD_NUMBER "<local dev build>")
else()
    set(BUILD_NUMBER "$ENV{TRAVIS_BUILD_NUMBER}")
endif()

# get current date
execute_process(
    COMMAND env LC_ALL=C date -u "+%Y-%m-%d %H:%M:%S %Z"
    OUTPUT_VARIABLE DATE
    OUTPUT_STRIP_TRAILING_WHITESPACE
    RESULT_VARIABLE DATE_RESULT
)
if(NOT DATE_RESULT EQUAL 0)
    message(FATAL_ERROR "Failed to determine date string")
endif()
mark_as_advanced(DATE DATE_RESULT)

add_subdirectory(tools/linuxdeployqt)

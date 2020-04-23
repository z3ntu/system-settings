project(ubuntu-system-settings C CXX)
cmake_minimum_required(VERSION 2.8.10)

find_package(Qt5Gui REQUIRED)
find_package(Qt5Qml REQUIRED)
find_package(Qt5Quick REQUIRED)
find_package(Qt5Test REQUIRED)

set(CMAKE_AUTOMOC ON)

add_subdirectory(tests)

project(ubuntu-system-settings C CXX)
cmake_minimum_required(VERSION 2.8.10)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x -fno-permissive -pedantic -Wall -Wextra")
find_package(Qt5Gui REQUIRED)
find_package(Qt5Qml REQUIRED)
find_package(Qt5Quick REQUIRED)
find_package(Qt5Test REQUIRED)

# Workaround for https://bugreports.qt-project.org/browse/QTBUG-29987
set(QT_IMPORTS_DIR "${CMAKE_INSTALL_LIBDIR}/qt5/qml")
set(CMAKE_AUTOMOC ON)

include_directories(src)
add_subdirectory(tests)

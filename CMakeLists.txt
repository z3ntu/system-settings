project(ubuntu-system-settings C CXX)
cmake_minimum_required(VERSION 2.8.10)

set(PROJECT_VERSION 0.1)
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
include(FindPkgConfig)
include(GNUInstallDirs)
set(LIBDIR ${CMAKE_INSTALL_LIBDIR})
enable_testing()


set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x -fno-permissive -pedantic -Wall -Wextra")
find_package(Qt5Concurrent REQUIRED)
find_package(Qt5DBus REQUIRED)
find_package(Qt5Gui REQUIRED)
find_package(Qt5Qml REQUIRED)
find_package(Qt5Quick REQUIRED)
find_package(Qt5Sql REQUIRED)
find_package(Qt5Test REQUIRED)
find_package(Qt5Widgets REQUIRED)

# Workaround for https://bugreports.qt-project.org/browse/QTBUG-29987
set(QT_IMPORTS_DIR "${CMAKE_INSTALL_LIBDIR}/qt5/qml")
set(CMAKE_AUTOMOC ON)

pkg_search_module(GOBJECT REQUIRED gobject-2.0)
pkg_search_module(GLIB REQUIRED glib-2.0)
pkg_check_modules(GIO REQUIRED gio-2.0 gio-unix-2.0)
pkg_search_module(UPOWER_GLIB REQUIRED upower-glib)
pkg_search_module(ACCOUNTSSERVICE REQUIRED accountsservice)
pkg_search_module(GEONAMES REQUIRED geonames)
pkg_search_module(ICU REQUIRED icu-i18n)
pkg_search_module(ANDR_PROP libandroid-properties)
pkg_check_modules(QTDBUSMOCK REQUIRED libqtdbusmock-1 REQUIRED)
pkg_check_modules(QTDBUSTEST REQUIRED libqtdbustest-1 REQUIRED)
pkg_search_module(POLKIT_AGENT polkit-agent-1)
pkg_search_module(CLICK REQUIRED click-0.4)
pkg_check_modules(QTGSETTINGS REQUIRED gsettings-qt)

find_program(XGETTEXT_BIN xgettext)
find_program(MSGFMT_BIN msgfmt)
find_program(INTLTOOL_MERGE intltool-merge)
find_program(INTLTOOL_EXTRACT intltool-extract)

set(DATA_DIR share)
set(MODULE_DIR ubuntu-system-settings)
set(MANIFEST_DIR "ubuntu/settings/system")
set(QML_DIR qml-plugins)
set(PRIVATE_DIR private)

# share/ubuntu/settings/system
set(PLUGIN_MANIFEST_DIR_BASE ${DATA_DIR}/${MANIFEST_DIR})
# ubuntu-system-settings
set(PLUGIN_MODULE_DIR_BASE ${MODULE_DIR})
# ubuntu-system-settings/private
set(PLUGIN_PRIVATE_MODULE_DIR_BASE "${PLUGIN_MODULE_DIR_BASE}/${PRIVATE_DIR}")
# share/ubuntu/settings/system/qml-plugins
set(PLUGIN_QML_DIR_BASE ${DATA_DIR}/${MANIFEST_DIR}/${QML_DIR})
# E.g. /usr/share/ubuntu/settings/system
set(PLUGIN_MANIFEST_DIR "${CMAKE_INSTALL_PREFIX}/${PLUGIN_MANIFEST_DIR_BASE}")
# E.g. /usr/lib/ubuntu-system-settings
set(PLUGIN_MODULE_DIR "${CMAKE_INSTALL_PREFIX}/${LIBDIR}/${PLUGIN_MODULE_DIR_BASE}")
# E.g. /usr/share/ubuntu/settings/system/qml-plugins
set(PLUGIN_QML_DIR "${CMAKE_INSTALL_PREFIX}/${PLUGIN_QML_DIR_BASE}")
# E.g. /usr/lib/ubuntu-system-settings/private
set(PLUGIN_PRIVATE_MODULE_DIR "${CMAKE_INSTALL_PREFIX}/${LIBDIR}/${PLUGIN_PRIVATE_MODULE_DIR_BASE}")
set(SETTINGS_SHARE_DIR "${CMAKE_INSTALL_PREFIX}/${PLUGIN_MANIFEST_DIR_BASE}")
set(PUSH_HELPER_DIR "lib/ubuntu-push-client/legacy-helpers")

SET(CMAKE_INSTALL_RPATH "${PLUGIN_MODULE_DIR}")

add_subdirectory(lib)
include_directories(lib)
include_directories(src)
add_subdirectory(plugins)
add_subdirectory(src)
add_subdirectory(tests)

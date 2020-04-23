include_directories(
    ../src
    ${CMAKE_CURRENT_BINARY_DIR}
    ${GLIB_INCLUDE_DIRS}
    ${QTDBUSMOCK_INCLUDE_DIRS}
    ${QTDBUSTEST_INCLUDE_DIRS}
)

set(XVFB_CMD xvfb-run -a -s "-screen 0 640x480x24")

add_definitions(-DI18N_DOMAIN="ubuntu-system-settings")
add_definitions(-DPLUGIN_PRIVATE_MODULE_DIR="${PLUGIN_PRIVATE_MODULE_DIR}")
add_definitions(-DPLUGIN_MODULE_DIR="${CMAKE_CURRENT_BINARY_DIR}")
add_definitions(-DMANIFEST_DIR="data")
add_definitions(-DPLUGIN_MANIFEST_DIR="${CMAKE_CURRENT_SOURCE_DIR}/data")
add_definitions(-DQML_TEST_DIR="${CMAKE_CURRENT_SOURCE_DIR}")
add_definitions(-DQML_DIR="${CMAKE_CURRENT_BINARY_DIR}")
add_definitions(-DPLUGIN_QML_DIR="${CMAKE_CURRENT_BINARY_DIR}")
add_definitions(-DSYSTEM_IMAGE_DBUS_TEMPLATE="${CMAKE_SOURCE_DIR}/tests/autopilot/ubuntu_system_settings/tests/systemimage.py")
add_definitions(-DI18N_DOMAIN="ubuntu-system-settings")


add_subdirectory(utils)

# QML tests that require graphical capabilities.
add_custom_target(qmluitests)
add_dependencies(qmluitests UbuntuTest)

add_custom_target(qmltests)
add_dependencies(qmltests qmluitests)

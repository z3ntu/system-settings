include_directories(${CMAKE_CURRENT_BINARY_DIR})

set(QML_SOURCES PageComponent.qml)
add_library(example-plugin MODULE example-plugin.cpp example-plugin.h ${QML_SOURCES})
qt5_use_modules(example-plugin Qml Core)
target_link_libraries(example-plugin SystemSettings)

# This plugin is only an example so let's not install it.
#install(FILES example.settings DESTINATION ${PLUGIN_MANIFEST_DIR})
#install(FILES ${QML_SOURCES} DESTINATION ${PLUGIN_QML_DIR}/example)

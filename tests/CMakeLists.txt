include_directories(
    ../src
    ${CMAKE_CURRENT_BINARY_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${Qt5Gui_PRIVATE_INCLUDE_DIRS}
)

set(UbuntuTestQML_SOURCES
    testutil.cpp
    plugin.cpp
)

add_library(UbuntuTestQml MODULE ${UbuntuTestQML_SOURCES})

target_link_libraries(UbuntuTestQml Qt5::Core Qt5::Quick Qt5::Test)

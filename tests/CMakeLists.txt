include_directories(
    ../src
    ${CMAKE_CURRENT_SOURCE_DIR}
)

set(UbuntuTestQML_SOURCES
    plugin.cpp
)

add_library(UbuntuTestQml MODULE ${UbuntuTestQML_SOURCES})

target_link_libraries(UbuntuTestQml Qt5::Core Qt5::Quick Qt5::Test)

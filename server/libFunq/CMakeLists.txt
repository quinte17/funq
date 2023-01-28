cmake_minimum_required(VERSION 3.6)

project(Funq)

# Tells CMake to generate compiler options appropriate for C++11.
set(CMAKE_CXX_STANDARD 11)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOMOC ON)

# This variable is used to avoid repeating names of source file everywhere we need them.
set(SOURCE_FILES
    funq.cpp
    objectpath.cpp
    dragndropresponse.cpp
    ldPreloadInjector.cpp
    pick.cpp
    player.cpp
    shortcutresponse.cpp
    protocole/delayedresponse.cpp
    protocole/json.cpp
    protocole/jsonclient.cpp
    protocole/protocole.cpp
)

find_package(Qt5 REQUIRED COMPONENTS
    Core
    Network
    Widgets
    Qml
    Quick
    Test
)

add_library(${CMAKE_PROJECT_NAME} SHARED ${SOURCE_FILES})

target_link_libraries(${CMAKE_PROJECT_NAME}
    Qt5::Core
    Qt5::Network
    Qt5::Widgets
    Qt5::Qml
    Qt5::Quick
    Qt5::Test
)

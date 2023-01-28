cmake_minimum_required(VERSION 3.6)

project(Funq)

# Tells CMake to generate compiler options appropriate for C++11.
set(CMAKE_CXX_STANDARD 11)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOMOC ON)

set(Qt5_SYSTEMWIDE /opt/Qt5.8.0/5.8/gcc_64)
set(Qt5_LOCAL $ENV{HOME}/Qt5.8.0/5.8/gcc_64)
message("Testing against Qt")
if(EXISTS ${Qt5_SYSTEMWIDE})
    message("System-wide Qt found!")
    set(Qt5_BASE_DIR ${Qt5_SYSTEMWIDE})
elseif(EXISTS ${Qt5_LOCAL})
    message("Local Qt found!")
    set(Qt5_BASE_DIR ${Qt5_LOCAL})
else()
    message("No user installed Qt5 found!")
endif()

if(DEFINED Qt5_BASE_DIR)
    message("Adjust CMAKE_PREFIX_PATH")
    set(CMAKE_PREFIX_PATH ${Qt5_BASE_DIR};${CMAKE_PREFIX_PATH})
endif()

# This variable is used to avoid repeating names of source file everywhere we
# need them.
set(SOURCE_FILES funq.cpp objectpath.cpp dragndropresponse.cpp ldPreloadInjector.cpp pick.cpp player.cpp shortcutresponse.cpp protocole/delayedresponse.cpp protocole/json.cpp protocole/jsonclient.cpp protocole/protocole.cpp)

find_package(Qt5 REQUIRED COMPONENTS Core Network Widgets Qml Quick Test)

add_library(${CMAKE_PROJECT_NAME} SHARED ${SOURCE_FILES})

target_link_libraries(${CMAKE_PROJECT_NAME} Qt5::Core Qt5::Network Qt5::Widgets Qt5::Qml Qt5::Quick Qt5::Test)

cmake_minimum_required(VERSION 3.6)

project(funq-test-app)

# Tells CMake to generate compiler options appropriate for C++11.
set(CMAKE_CXX_STANDARD 11)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOMOC ON)

# This variable is used to avoid repeating names of source file everywhere we need them.
set(SOURCE_FILES
    main.cpp
    widgets.h
)

find_package(Qt5 REQUIRED COMPONENTS
    Core
    Gui
    Widgets
)

add_executable(${CMAKE_PROJECT_NAME} ${SOURCE_FILES})

target_link_libraries(${CMAKE_PROJECT_NAME}
    Qt5::Core
    Qt5::Gui
    Qt5::Widgets
)

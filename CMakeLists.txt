cmake_minimum_required(VERSION 3.16)

include("cmake/HunterGate.cmake")

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(Homework_2)

find_package(Curses REQUIRED)
include_directories(${CURSES_INCLUDE_DIR})

add_library(${PROJECT_NAME} STATIC
        ${CMAKE_CURRENT_SOURCE_DIR}/
        sources/placing_ships.cpp
        sources/player_field.cpp
        sources/AI.cpp
        sources/comp_field.cpp
        sources/menu.cpp
        )

target_include_directories(${PROJECT_NAME} PUBLIC
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
        "$<INSTALL_INTERFACE:include>")

add_executable(demo ${CMAKE_CURRENT_SOURCE_DIR}/demo/main.cpp)

install(TARGETS ${PROJECT_NAME}
        EXPORT ${PROJECT_NAME}-config
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        )

target_link_libraries(demo ${CURSES_LIBRARIES})
target_link_libraries(demo ${PROJECT_NAME})

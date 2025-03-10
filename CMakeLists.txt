cmake_minimum_required(VERSION 3.13)
 
project(whereami)

# Create static library
add_library(${PROJECT_NAME} STATIC ${CMAKE_CURRENT_LIST_DIR}/src/whereami.c)
set_target_properties(${PROJECT_NAME} PROPERTIES PUBLIC_HEADER ${CMAKE_CURRENT_LIST_DIR}/src/whereami.h)
add_executable(${PROJECT_NAME}-example ${CMAKE_CURRENT_LIST_DIR}/example/executable.c)
target_link_libraries(${PROJECT_NAME}-example ${PROJECT_NAME})

# Use PUBLIC iso INTERFACE, so the targets also finds our own header file
target_include_directories(
    ${PROJECT_NAME}
    PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}/src
)
target_include_directories(
    ${PROJECT_NAME}-example
    PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}/src
)

install(TARGETS ${PROJECT_NAME} ${PROJECT_NAME}-example)


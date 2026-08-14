cmake_minimum_required(VERSION 3.20.0)

project(my_project_name VERSION 0.0.1 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)
# set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_C_STANDARD 17)

if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
    if(NOT CMAKE_SYSTEM_NAME STREQUAL "Linux")
        add_compile_options("$<$<CONFIG:Debug>:-fsanitize=address>")
        add_link_options("$<$<CONFIG:Debug>:-fsanitize=address>")
    endif()
    add_compile_options("$<$<CONFIG:Release>:-flto>")
    add_link_options("$<$<CONFIG:Release>:-flto>")
elseif(MSVC)
    add_compile_options("$<$<CONFIG:Debug>:/fsanitize=address>")
    add_link_options("$<$<CONFIG:Debug>:/fsanitize=address>")
    set(CMAKE_INTERPROCEDURAL_OPTIMIZATION "$<$<CONFIG:Release>:ON>")
endif()

include_directories(${PROJECT_SOURCE_DIR}/include)

add_subdirectory(./src)

# add_subdirectory(./test)

# add_subdirectory(./example)

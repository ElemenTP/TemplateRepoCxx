cmake_minimum_required(VERSION 3.20.0)

project(my_project_name VERSION 0.0.1 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)
# set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_C_STANDARD 17)

if (NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Debug)
    message("Setting default build type to Debug")
endif()

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
        if(NOT CMAKE_SYSTEM_NAME STREQUAL "Linux")
            add_compile_options("-fsanitize=address")
            add_link_options("-fsanitize=address")
        endif()
    elseif(MSVC)
        add_compile_options("/fsanitize=address")
        add_link_options("/fsanitize=address")
    endif()
else()
    if(CMAKE_CXX_COMPILER_ID MATCHES "GNU|Clang")
        add_compile_options("-flto")
        add_link_options("-flto")
    elseif(MSVC)
        set(CMAKE_INTERPROCEDURAL_OPTIMIZATION ON)
    endif()
endif()

include_directories(${PROJECT_SOURCE_DIR}/include)

add_subdirectory(./src)

# add_subdirectory(./test)

# add_subdirectory(./example)

# for each "test/x.cpp", generate target "x"
file(GLOB_RECURSE all_tests *.cpp *.cxx *.cc *.c)
foreach(v ${all_tests})
    string(REGEX MATCH "test/.*" relative_path ${v})
    # message(${relative_path})
    string(REGEX REPLACE "test/" "" target_name ${relative_path})
    string(REGEX REPLACE ".cpp" "" target_name ${target_name})

    add_executable(${target_name} ${v})
endforeach()

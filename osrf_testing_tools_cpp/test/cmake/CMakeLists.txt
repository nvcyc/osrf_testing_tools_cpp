# Test logic for version filtering when selecting googletest version.
add_test(
  NAME "test_osrf_testing_tools_cpp_filter_versions_cmake"
  COMMAND
    ${CMAKE_COMMAND} -P
    "${CMAKE_SOURCE_DIR}/test/cmake/test_osrf_testing_tools_cpp_filter_versions.cmake"
)
# Verify static BFD dependencies with and without optional SFrame/Zstd libraries.
if(UNIX AND NOT APPLE)
  foreach(case with_optional_libraries without_optional_libraries shared)
    add_test(
      NAME "test_backward_dependencies_${case}"
      COMMAND ${CMAKE_COMMAND}
        -S "${CMAKE_CURRENT_SOURCE_DIR}/backward_dependencies"
        -B "${CMAKE_CURRENT_BINARY_DIR}/backward_dependencies_${case}"
        "-DCASE=${case}"
        "-DBACKWARD_CONFIG_FILE=${CMAKE_SOURCE_DIR}/src/memory_tools/vendor/bombela/backward-cpp/BackwardConfig.cmake"
    )
  endforeach()
endif()

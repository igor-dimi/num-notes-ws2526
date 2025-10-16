# code_examples/my_solutions/src/ch1/CMakeLists.txt
set(CHAPTER ch1)

# Per-chapter output folder
set(OUT_DIR "${CMAKE_BINARY_DIR}/bin/${CHAPTER}")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${OUT_DIR}")
foreach(cfg IN ITEMS Debug Release RelWithDebInfo MinSizeRel)
  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${cfg} "${OUT_DIR}/${cfg}")
endforeach()

# Helper to add ch1 examples
function(add_ch_example name)
  add_executable(${name} "${name}.cpp")
  target_link_libraries(${name} PRIVATE hdnum_common)
  # Optional: group in IDEs
  set_target_properties(${name} PROPERTIES FOLDER "${CHAPTER}")
endfunction()

# List executables in this chapter
add_ch_example(ch1_demo)
# add_ch_example(ch1_newton_demo)

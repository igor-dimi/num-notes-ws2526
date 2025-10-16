# code_examples/my_solutions/src/ch1/CMakeLists.txt
set(CHAPTER ch2)

# Per-chapter output folder
set(OUT_DIR "${CMAKE_BINARY_DIR}/bin/${CHAPTER}")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${OUT_DIR}")
foreach(cfg IN ITEMS Debug Release RelWithDebInfo MinSizeRel)
  set(CMAKE_RUNTIME_OUTPUT_DIRECTORY_${cfg} "${OUT_DIR}/${cfg}")
endforeach()

# Helper to add ch2 examples
function(add_ch_example name)
  add_executable(${name} "${name}.cpp")
  target_link_libraries(${name} PRIVATE hdnum_common)
  # Optional: group in IDEs
  set_target_properties(${name} PROPERTIES FOLDER "${CHAPTER}")
endfunction()

# List executables in this chapter
add_ch_example(ch2_demo)
# add_ch_example(ch1_newton_demo)

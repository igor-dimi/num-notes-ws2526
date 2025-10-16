cmake_minimum_required(VERSION 3.16)
project(hdnum_examples CXX)
set(CMAKE_CXX_STANDARD 20)

# (Optional) put all executables under a single bin/ root
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")

# hdnum include dir (submodule)
set(HDNUM_DIR "${CMAKE_CURRENT_LIST_DIR}/../hdnum")

# Common config shared by all examples
add_library(hdnum_common INTERFACE)
target_include_directories(hdnum_common INTERFACE "${HDNUM_DIR}")

# Optional: enable GMP support in hdnum
option(HDNUM_USE_GMP "Enable GMP in hdnum" OFF)
if(HDNUM_USE_GMP)
  target_compile_definitions(hdnum_common INTERFACE HDNUM_HAS_GMP=1)
  find_library(GMPXX gmpxx)
  find_library(GMP   gmp)
  if(GMPXX AND GMP)
    target_link_libraries(hdnum_common INTERFACE ${GMPXX} ${GMP})
  else()
    message(FATAL_ERROR "GMP not found; set paths or disable HDNUM_USE_GMP")
  endif()
endif()

# Chapters to include (add/remove as needed)
set(HDNUM_CHAPTERS ch1 ch2 ch3 ch4 ch5 ch6 ch7 ch8 ch9 ch10)
foreach(ch IN LISTS HDNUM_CHAPTERS)
  if(EXISTS "${CMAKE_CURRENT_LIST_DIR}/src/${ch}/CMakeLists.txt")
    add_subdirectory("src/${ch}")
  endif()
endforeach()

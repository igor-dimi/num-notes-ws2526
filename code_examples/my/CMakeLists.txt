cmake_minimum_required(VERSION 3.16)
project(hdnum_examples CXX)
set(CMAKE_CXX_STANDARD 20)
set(HDNUM_DIR "${CMAKE_CURRENT_LIST_DIR}/../hdnum")

add_executable(demo demo.cc)
target_include_directories(demo PRIVATE "${HDNUM_DIR}")

# Optional: GMP
option(HDNUM_USE_GMP "Enable GMP in hdnum" OFF)
if(HDNUM_USE_GMP)
  target_compile_definitions(ode_demo PRIVATE HDNUM_HAS_GMP=1)
  find_library(GMPXX gmpxx)
  find_library(GMP gmp)
  if(GMPXX AND GMP)
    target_link_libraries(demo PRIVATE ${GMPXX} ${GMP})
  else()
    message(FATAL_ERROR "GMP not found; set library paths or disable HDNUM_USE_GMP")
  endif()
endif()



cmake_minimum_required(VERSION 3.3)
project(wmm15 C)
enable_testing()

add_compile_options(-O3)

add_library(geo GeomagnetismLibrary.c)
set_target_properties(geo PROPERTIES POSITION_INDEPENDENT_CODE TRUE)
target_link_libraries(geo m)

add_library(wmm15 SHARED wmm_point_sub.c)
target_link_libraries(wmm15 PRIVATE geo) 

add_executable(wmm wmm_point.c)
target_link_libraries(wmm PRIVATE geo)


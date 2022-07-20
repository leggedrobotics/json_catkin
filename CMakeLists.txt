cmake_minimum_required(VERSION 2.8.3)
project(json_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(ExternalProject)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include)

set(VERSION 3.9.1)
ExternalProject_Add(json_src
  URL https://github.com/nlohmann/json/archive/v${VERSION}.zip
  UPDATE_COMMAND ""
  CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX} -DCMAKE_BUILD_TYPE=Release
  -DBUILD_SHARED_LIBS=ON
)
ExternalProject_Get_Property(json_src source_dir)
include_directories(${install_dir}/include)


install(DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/nlohmann
        DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}
        FILES_MATCHING PATTERN "*.hpp")
cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include/)

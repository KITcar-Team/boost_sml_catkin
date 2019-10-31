cmake_minimum_required(VERSION 2.8.3)
project(boost_sml_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(ExternalProject)

set(VERSION 1.0.0)

# The configure step fails at catkin_package() if this directory
# doesn't exist yet. Create it at configure time!
file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/boost_sml_catkin)

ExternalProject_Add(boost_sml_src
  GIT_REPOSITORY https://github.com/boost-experimental/sml.git
  GIT_TAG 2dab1265f87f70a2941af9de8f3f157df9a6a53f
  CONFIGURE_COMMAND ""
  BUILD_COMMAND ""
  INSTALL_COMMAND rsync -a ../boost_sml_src/include/boost/sml.hpp ${CATKIN_DEVEL_PREFIX}/include/boost_sml_catkin/sml.hpp
)

include_directories(${CATKIN_DEVEL_PREFIX}/include/)

cs_install()

cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include)

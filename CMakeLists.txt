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
  GIT_TAG 8968695b40ce1c9dad7ba78d8220f5b7bf458d08
  CONFIGURE_COMMAND ""
  BUILD_COMMAND ""
  INSTALL_COMMAND rsync -a ../boost_sml_src/include/boost/ ${CATKIN_DEVEL_PREFIX}/include/boost_sml_catkin/
)

include_directories(${CATKIN_DEVEL_PREFIX}/include/)

cs_install()

cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include)

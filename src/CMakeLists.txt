#
# Copyright (c) 2014 CNRS
# Authors: Mathieu Geisert
#
#
# This file is part of gepetto-viewer
# gepetto-viewer is free software: you can redistribute it
# and/or modify it under the terms of the GNU Lesser General Public
# License as published by the Free Software Foundation, either version
# 3 of the License, or (at your option) any later version.
#
# hpp-manipulation is distributed in the hope that it will be
# useful, but WITHOUT ANY WARRANTY; without even the implied warranty
# of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# General Lesser Public License for more details.  You should have
# received a copy of the GNU Lesser General Public License along with
# hpp-manipulation  If not, see
# <http://www.gnu.org/licenses/>.

SET(LIBRARY_NAME ${PROJECT_NAME})
find_package(OpenSceneGraph REQUIRED)
find_package(osgGA REQUIRED)
find_package(osgDB REQUIRED)
find_package(osgViewer REQUIRED)

ADD_LIBRARY(${LIBRARY_NAME} SHARED
 # group-node.cpp
  #node.cpp
  #window-manager.cpp
  #leaf-node-line.cpp
  #leaf-node-box.cpp
  #leaf-node-cylinder.cpp
  #leaf-node-cone.cpp
  #leaf-node-face.cpp
 # leaf-node-sphere.cpp
  #leaf-node-capsule.cpp
  #leaf-node-ground.cpp
  #leaf-node-collada.cpp
  urdf-parser.cpp
robot.cpp
viewer.cpp
)
include_directories(${PINOCCHIO_PATH}/include)
include_directories(${EIGEN3_INCLUDE_DIR})
PKG_CONFIG_USE_DEPENDENCY(${LIBRARY_NAME} openscenegraph)
PKG_CONFIG_USE_DEPENDENCY(${LIBRARY_NAME} openthreads)
#PKG_CONFIG_USE_DEPENDENCY(${LIBRARY_NAME} eigen3)
PKG_CONFIG_USE_DEPENDENCY(${LIBRARY_NAME} urdfdom)

ADD_EXECUTABLE(testing ../tests/test.cpp)
TARGET_LINK_LIBRARIES(testing ${LIBRARY_NAME} ${OPENTHREADS_LIBRARIES}  ${OPENSCENEGRAPH_LIBRARIES} ${OSGVIEWER_LIBRARIES} ${OSGDB_LIBRARIES} ${OSGGA_LIBRARIES})
INSTALL(TARGETS testing DESTINATION bin)

INSTALL(TARGETS ${LIBRARY_NAME} DESTINATION lib)



# NOTE: Make sure a previous installation of OpenSceneGraph is not installed in /usr/lib/x86_64-linux-gnu/
set(OSG_DIR /usr/local/lib64)
find_package(OpenSceneGraph REQUIRED osg osgDB osgUtil osgViewer osgGA)
       
include_directories(
  SYSTEM  
  ${Boost_INCLUDE_DIRS}
  ${OpenRAVE_INCLUDE_DIRS}
  ${OPENSCENEGRAPH_INCLUDE_DIRS}
)

if (APPLE) 
# see http://forum.openscenegraph.org/viewtopic.php?t=11097
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-deprecated-declarations")
else()
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-deprecated-declarations -fvisibility=hidden")
endif()

                    
add_library(osgviewer
  osgviewer.cpp 
  robot_ui.cpp
)

target_link_libraries(osgviewer ${OPENSCENEGRAPH_LIBRARIES} ${OpenRAVE_BOTH_LIBRARIES} ${Boost_SYSTEM_LIBRARY} utils)


#add_subdirectory(test)
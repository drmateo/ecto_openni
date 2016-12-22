PROJECT(openni_wrapper)

set(CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/../cmake/Modules/" ${CMAKE_MODULE_PATH})
INCLUDE_DIRECTORIES(${PROJECT_SOURCE_DIR}/include)
INCLUDE_DIRECTORIES(${OPENNI_INCLUDE_DIR})
message(STATUS "OpenNI headers: ${OPENNI_INCLUDE_DIR}")
#INCLUDE_DIRECTORIES("/usr/include/openni")
INCLUDE_DIRECTORIES(${OpenCV_INCLUDE_DIRS})

#LINK_DIRECTORIES(${CMAKE_LIBRARY_OUTPUT_DIRECTORY})

set (SRCS 
  src/openni_device.cpp
  src/openni_device_xtion.cpp  
  src/openni_image_bayer_grbg.cpp
  src/openni_device_kinect.cpp     
  src/openni_driver.cpp        
  src/openni_image_rgb24.cpp
  src/openni_device_oni.cpp	  
  src/openni_image_yuv_422.cpp
  src/openni_depth_image.cpp	
  src/openni_device_primesense.cpp  
  src/openni_exception.cpp     
  src/openni_ir_image.cpp
  )

set_source_files_properties(${SRCS}
  PROPERTIES
  COMPILE_FLAGS "-Wno-deprecated -Wno-strict-aliasing -Wno-unknown-pragmas -Wno-error"
  )

ADD_LIBRARY(openni_wrapper SHARED ${SRCS})

find_package(libusb-1.0 REQUIRED)
target_link_libraries(openni_wrapper ${Boost_LIBRARIES}
                                     ${OpenCV_LIBRARIES}
                                     ${OPENNI_LIBRARY}
                                     ${LIBUSB_1_LIBRARIES}
)

install(TARGETS openni_wrapper
        DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
)

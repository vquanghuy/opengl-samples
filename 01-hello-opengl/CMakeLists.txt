cmake_minimum_required(VERSION 3.0)

# Reuseable functions
function(detect_platform result)
  if(APPLE)
    if(CMAKE_SYSTEM_PROCESSOR STREQUAL "arm64")
      set(${result} "darwin_arm64" PARENT_SCOPE)
    else()
      set(${result} "darwin_x86_64" PARENT_SCOPE)
    endif()
  elseif(UNIX)
    set(${result} "linux" PARENT_SCOPE)
  elseif(WIN32)
    set(${result} "windows" PARENT_SCOPE)
  endif()
endfunction()

# Init project name
project(HelloOpenGL)
detect_platform(PLATFORM)

# Set the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Suppress the deprecated warning for OpenGL on macOS
add_definitions(-DGL_SILENCE_DEPRECATION)

# Set the directory for external dependencies
set(EXTERNAL_DIR ${CMAKE_CURRENT_SOURCE_DIR}/external)

# Add include directories for GLFW
include_directories(${EXTERNAL_DIR}/glfw/include)

# Search for all source files in the src directory
aux_source_directory(src SRC_FILES)

# Add executable target
add_executable(HelloOpenGL ${SRC_FILES})

# Configure lib path based on platform
if(PLATFORM STREQUAL "darwin_arm64")
  set(CMAKE_OSX_ARCHITECTURES "arm64")
  set(GLFW_LIB ${EXTERNAL_DIR}/glfw/lib-arm64/libglfw3.a)
elseif(PLATFORM STREQUAL "darwin_x86_64")
  set(CMAKE_OSX_ARCHITECTURES "x86_64")
  set(GLFW_LIB ${EXTERNAL_DIR}/glfw/lib-x86_64/libglfw3.a)
elseif(PLATFORM STREQUAL "windows")
  # TBU
elseif(PLATFORM STREQUAL "linux")
  # TBU
endif()

# Link against GLFW
target_link_libraries(HelloOpenGL PRIVATE ${GLFW_LIB})

# Set the output directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin)

set_target_properties(HelloOpenGL PROPERTIES DEFAULT_BUILD_TARGET ON)

# Xcode specific configuration
if(PLATFORM MATCHES "^darwin")
  set(XCODE_PRODUCT_NAME "HelloOpenGL")

  # Set the startup project for Xcode
  set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY XCODE_STARTUP_PROJECT "HelloOpenGL")

  # Set up folder structure in Xcode
  source_group("src" FILES ${SRC_FILES})

  # Set the default Xcode scheme to HelloOpenGL
  set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY XCODE_SCHEME_TARGET "HelloOpenGL")

  # Add the required macOS frameworks
  target_link_libraries(HelloOpenGL PRIVATE "-framework IOKit" "-framework Cocoa" "-framework OpenGL")
endif()
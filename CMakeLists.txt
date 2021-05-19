cmake_minimum_required(VERSION 3.9.6)
project( Project-Name
  LANGUAGES CXX
  VERSION   1.0.0
  DESCRIPTION "Application Template"
)

#############################
# Options
#############################
option( APP_OPTION               "Option Description" OFF)

#############################
# Set Library Name, Linker, and Flags
#############################
# Library Variables
set(APP_NAME app)
set(SH_VER 0)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Base Compiler Flags
set(MY_DEBUG_FLAGS 
  -Wall 
  -Wextra
  -Werror
  -W
  -DDEBUG
  -g
)

set(MY_RELEASE_FLAGS
  -pedantic
  -03
)

#############################
# Set Files and Directories
#############################
# Source Files
set(SRC_FILES
  ${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp
)

# Header Files
set(HEADER_FILES
  #${CMAKE_CURRENT_SOURCE_DIR}/inc/_.h
)

# Include Files
set(APP_INC_DIRS
  ${CMAKE_CURRENT_SOURCE_DIR}/inc
)

# Library Directories
set(APP_LIB_DIRS
)

set(APP_LIBS 
  #  pthread
)

#############################
# Dependencies 
#############################
# Boost
#find_package( Boost 1.73.0 REQUIRED )

#list( APPEND APP_INC_DIRS
#  ${Boost_INCLUDE_DIRS}
#)

#############################
# Recurse into Extern Directory
#############################

# Set all Directories which contain libraries
link_directories(${APP_LIB_DIRS})

#############################
# Make Target and Set Props
#############################
# Make App Binary
add_executable( ${APP_NAME} ${SRC_FILES} )

# Set Executable Properties
set_target_properties(${SAMPLE_NAME} PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
)

# Target Compiler Flags
target_compile_options( ${APP_NAME}
  PRIVATE
  "$<$<CONFIG:Debug>:${APP_DEBUG_FLAGS}>"
  "$<$<CONFIG:Release>:${APP_RELEASE_FLAGS}>"
)

#############################
# Find and Link Libraries
#############################
# Target Include Directories
target_include_directories( ${APP_NAME}
  PUBLIC
  ${APP_INC_DIRS}
)

# Link External Libraries
target_link_libraries( ${APP_NAME}
  PUBLIC
  ${APP_LIBS}
)

cmake_minimum_required(VERSION 3.22)

#
# This file is generated only once,
# and is not re-generated if converter is called multiple times.
#
# User is free to modify the file as much as necessary
#

# Setup compiler settings
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS ON)

# Define the build type
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE "Debug")
endif()

message("Build type: " ${CMAKE_BUILD_TYPE})

# Enable compile command to ease indexing with e.g. clangd
set(CMAKE_EXPORT_COMPILE_COMMANDS TRUE)

# Compiler options
set(STM32_MCU_FLAGS  -mcpu=cortex-m33 -mfpu=fpv4-sp-d16 -mfloat-abi=hard -mcmse )

#Linker options
set(STM32_LINKER_SCRIPT STM32L552xE_FLASH_ns.ld)


# Set the project name
set(CMAKE_PROJECT_NAME l552-TZ_NS)
project(${CMAKE_PROJECT_NAME})

# Create an executable object type
add_executable(${CMAKE_PROJECT_NAME})

target_compile_options(${CMAKE_PROJECT_NAME} PRIVATE ${STM32_MCU_FLAGS} )

target_link_options(${CMAKE_PROJECT_NAME} PRIVATE ${STM32_MCU_FLAGS})
target_link_options(${CMAKE_PROJECT_NAME} PRIVATE -T "${CMAKE_CURRENT_SOURCE_DIR}/${STM32_LINKER_SCRIPT}")
target_link_options(${CMAKE_PROJECT_NAME} PRIVATE -Wl,-Map=${CMAKE_PROJECT_NAME}.map -Wl,--gc-sections)

# Include mx-generated
include("mx-generated.cmake")

if(NOT TARGET Secure_Nsclib)
    add_library(Secure_Nsclib OBJECT IMPORTED)
    set_target_properties(Secure_Nsclib PROPERTIES IMPORTED_OBJECTS "${CMAKE_SOURCE_DIR}/../Secure_nsclib/secure_nsclib.o")
endif ()

# Enable CMake support for ASM and C languages
enable_language(C ASM)

# In order to use CMake for cross-compiling
set(CMAKE_CXX_COMPILER_FORCED "true") 

# Add project symbols (macros)
target_compile_definitions(${CMAKE_PROJECT_NAME} PRIVATE 
    # Add user defined symbols
)

# Add include paths
target_include_directories(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user defined include paths
)

# Add sources to executable
target_sources(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user sources here
)

# Link directories setup
target_link_directories(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user defined library search paths
)

# Add linked libraries
target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE
    # Add user defined libraries
)

# Validate that STM32CubeMX code is compatible with C standard
if(CMAKE_C_STANDARD LESS 11)
    message(ERROR "Generated code requires C11 or higher")
endif()










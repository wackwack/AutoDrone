cmake_minimum_required(VERSION 3.10)
set(PROJECT_NAME AutoDrone)
project(${PROJECT_NAME} VERSION 1.0.0 LANGUAGES CXX)
find_package(OpenGL)

file(GLOB source_files
	"src/*.cpp"
)

set(SOURCES ${source_files})

# Detect and add SFML
set(CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake_modules" ${CMAKE_MODULE_PATH})
find_package(SFML 2 REQUIRED COMPONENTS network audio graphics window system)

# Set build type --I copied this from ClothSim and it worked!!!!
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif(NOT CMAKE_BUILD_TYPE)

add_executable(${PROJECT_NAME} ${SOURCES})
target_include_directories(${PROJECT_NAME} PRIVATE "include" "lib")
set(SFML_LIBS sfml-system sfml-window sfml-graphics)
target_link_libraries(${PROJECT_NAME} ${SFML_LIBS})
#target_link_libraries(${PROJECT_NAME} sfml-system sfml-window sfml-graphics)
#target_link_libraries(${PROJECT_NAME} C:\\Users\\alask\\Documents\\GitHub\\AutoDrone\\lib\\sfml-system C:\\Users\\alask\\Documents\\GitHub\\AutoDrone\\lib\\sfml-window C:\\Users\\alask\\Documents\\GitHub\\AutoDrone\\lib\\sfml-graphics)
if (UNIX)
   target_link_libraries(${PROJECT_NAME} pthread)
endif (UNIX)

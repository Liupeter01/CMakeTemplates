file(GLOB_RECURSE SUBMODULE_SOURCES CONFIGURE_DEPENDS src/*.cpp include/*.h include/*.hpp)
add_executable(submodule_target)
target_sources(submodule_target ${SUBMODULE_SOURCES})

set(LIBRARY_DIR /path/to/library)
find_package(package_name REQUIRED COMPONENTS components_1 components_n)

target_include_directories(submodule_target PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)

#PUBLIC: allow include directory being passed to other (sub)modules who using current module
target_include_directories(submodule_target PUBLIC ${package_INCLUDE_DIRS})
target_link_libraries(submodule_target PUBLIC package_name::components_1 package_name::components_n)

#PRIVATE:not allow include directory being passed to other (sub)modules who using current module
#target_include_directories(submodule_target PRIVATE ${package_INCLUDE_DIRS})
#target_link_libraries(submodule_target PRIVATE ${package_LIBRARIES})
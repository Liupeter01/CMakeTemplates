file(GLOB_RECURSE SUBMODULE_SOURCES CONFIGURE_DEPENDS src/*.cpp include/*.h include/*.hpp)
add_executable(submodule_target ${SUBMODULE_SOURCES})

#General
set(LIBRARY_DIR /path/to/library)
find_package(package_name CONFIG COMPONENTS components_1 components_n)

target_include_directories(submodule_target PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_link_libraries(submodule_target PRIVATE package_name::components_1 package_name::components_n)

#Boost
set(Boost_DIR "/usr/local/lib/cmake/Boost-1.85.0")
find_package(Boost COMPONENTS system thread REQUIRED)
target_include_directories(async_server PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_link_libraries(async_server PRIVATE Boost::system Boost::thread)

#jsoncpp
find_package(jsoncpp)
target_link_libraries(async_server PRIVATE jsoncpp_object)
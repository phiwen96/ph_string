# find_package(Boost REQUIRED)

file(GLOB_RECURSE HEADER_LIST "${PROJECT_SOURCE_DIR}/include/*.hpp")
file(GLOB SOURCE_LIST ${PROJECT_SOURCE_DIR}/src/*.cpp)

add_library (ph_string
	${SOURCE_LIST}  ${HEADER_LIST} 
)


set_target_properties (ph_string PROPERTIES CXX_STANDARD 20)
target_compile_features (ph_string PUBLIC cxx_std_20)


target_link_libraries (ph_string PUBLIC ph_concepts ph_data_structures)
target_include_directories (ph_string PUBLIC ph_concepts ph_data_structures ${PROJECT_SOURCE_DIR}/include)
# target_include_directories (ph_string PUBLIC ${Boost_INCLUDE_DIRS})
#  OpenSSL::SSL
target_compile_features (ph_string PUBLIC cxx_std_20)

# option(JS_ONLY "Compiles to native JS (No WASM)" OFF)


# if(JS_ONLY)
# 	message(STATUS "Setting compilation target to native JavaScript")
# 	set(CMAKE_EXECUTABLE_SUFFIX ".js")
# 	set_target_properties(ph_string PROPERTIES LINK_FLAGS "-s WASM=0 -s EXPORTED_FUNCTIONS='[_main]'")
# else(JS_ONLY)
# 	message(STATUS "Setting compilation target to WASM")
# 	set(CMAKE_EXECUTABLE_SUFFIX ".wasm.js")
# 	set_target_properties(ph_string PROPERTIES LINK_FLAGS "-s WASM=1 -s EXPORTED_FUNCTIONS='[_main]'")
# endif(JS_ONLY)

# target_compile_options(ph_string PUBLIC "-ast-dump  -fsyntax-only")
# echo 'export LDFLAGS="-L/opt/homebrew/opt/openssl@1.1/lib"' >> ~/.zshrc
# echo 'export CPPFLAGS="-I/opt/homebrew/opt/openssl@1.1/include"' >> ~/.zshrc
target_include_directories(ph_string PRIVATE
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include/ph_string>
    $<INSTALL_INTERFACE:include/ph_string>
)

target_include_directories(ph_string PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)

if (CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)

else()
    set_target_properties(${PROJECT_NAME}          PROPERTIES FOLDER "dependencies")
endif()

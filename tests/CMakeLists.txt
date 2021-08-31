
include(FetchContent)

FetchContent_Declare(
  Catch2
  GIT_REPOSITORY https://github.com/catchorg/Catch2.git
  GIT_TAG        v2.13.1)

FetchContent_MakeAvailable(Catch2)

file(GLOB_RECURSE HEADER_LIST "include/*.hpp")
file(GLOB SOURCE_LIST *.cpp)
add_executable (test_ph_string ${SOURCE_LIST} ${HEADER_LIST})
target_link_libraries (test_ph_string PUBLIC ph_string Catch2::Catch2 ${Boost_LIBRARIES})
target_include_directories (test_ph_string PRIVATE include PUBLIC ph_string ${Boost_INCLUDE_DIRS})
ph_precompile (TARGET test_ph_string PRIVATE PCH ${std_pch})
# add_test (NAME testtest_ph_string COMMAND ${self}) 


if (CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
    set_target_properties(test_ph_string          PROPERTIES FOLDER "ph_string")
else()
    set_target_properties(test_ph_string           PROPERTIES FOLDER "dependencies/ph_string")
endif()
# add_custom_target(
#   GenexDemo
#   COMMAND ${CMAKE_COMMAND} -E echo "$<TARGET_FILE:test_ph_string>"
#   VERBATIM
# )


add_custom_command(
  TARGET test_ph_string PRE_BUILD
  COMMAND ${CMAKE_COMMAND} -E echo "$<TARGET_FILE:test_ph_string>"
#   VERBATIM
)

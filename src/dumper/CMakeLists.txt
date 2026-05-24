project(GH-Offset-Dumper)

add_executable(${PROJECT_NAME} main.cpp GH-Offset-Dumper.rc resource.h)

target_link_libraries(${PROJECT_NAME} PRIVATE GH-Offset-Dumper-Lib)

target_include_directories(${PROJECT_NAME} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/../dumper-lib/include
)

if(MSVC)
    target_compile_options(${PROJECT_NAME} PRIVATE /W3)
    # Require Administrator for the dumper
    set_target_properties(${PROJECT_NAME} PROPERTIES LINK_FLAGS "/MANIFESTUAC:\"level='highestAvailable' uiAccess='false'\"")
endif()

# Set output name to include architecture
if(CMAKE_SIZEOF_VOID_P EQUAL 8)
    set_target_properties(${PROJECT_NAME} PROPERTIES OUTPUT_NAME "${PROJECT_NAME}-x64")
else()
    set_target_properties(${PROJECT_NAME} PROPERTIES OUTPUT_NAME "${PROJECT_NAME}-x86")
endif()

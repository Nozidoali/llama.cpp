set(TARGET llama-imatrix)
add_executable(${TARGET} imatrix.cpp)
target_link_libraries(${TARGET} PRIVATE common llama ${CMAKE_THREAD_LIBS_INIT})
target_compile_features(${TARGET} PRIVATE cxx_std_17)

if(LLAMA_TOOLS_INSTALL)
    if(NOT LLAMA_TOOLS_INSTALL_LIST OR "${TARGET}" IN_LIST LLAMA_TOOLS_INSTALL_LIST)
        install(TARGETS ${TARGET} RUNTIME)
    endif()
endif()

if (CMAKE_SYSTEM_NAME MATCHES "AIX")
    # AIX's flock() function comes from libbsd.a
    target_link_libraries(${TARGET} PRIVATE -lbsd)
endif()

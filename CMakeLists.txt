cmake_minimum_required(VERSION 3.13.4)
set(CMAKE_CXX_STANDARD 17)

 # DOWNLOAD SUBMODULES
 find_package(Git QUIET)
 if(GIT_FOUND and EXISTS "${PROJECT_SOURCE_DIR}/.git")
    option(GIT_SUBMODULE "Check submodules during the build" ON)
    if(GIT_SUBMODULE)
        message(STATUS "Submodule update")
        execute_process(COMMAND ${GIT_EXECUTABLE} submodule update --init --recursive
                        WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR/lib}
                        RESULT_VARIABLE GIT_SUBMOD_RESULT)
        if(NOT GIT_SUBMOD_RESULT EQUAL "0")
            message(FATAL_ERROR "git submodule update --init failed with ${GIT_SUBMOD_RESULT}, please check this command and re-run")
        endif()
    endif()
endif()

# CHECK SUBMODULES
#if(NOT EXISTS "${PROJECT_SOURCE_DIR}/lib/LIB/CMakeLists.txt")
#    message(FATAL_ERROR "The LIB was not downloaded ! GIT Submodle was turned off or failed")
#endif()

enable_testing()

add_subdirectory(src)

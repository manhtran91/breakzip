add_subdirectory (test)
configure_file(breakzip_config.h.in breakzip_config.h)
add_library(breakzipcore breakzip.cpp)
add_executable(breakzip main.cpp)
target_link_libraries(breakzip breakzipcore ${LIBS})

install(TARGETS breakzip breakzipcore
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib/breakziplib)

find_package(Doxygen)
if(DOXYGEN_FOUND)
    configure_file(${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in
        ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile @ONLY)
    add_custom_target(doc
        ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/Doxyfile
        WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
        COMMENT "Generating API docs w/Doxygen" VERBATIM)
endif(DOXYGEN_FOUND)

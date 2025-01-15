cmake_minimum_required(VERSION 3.30)

add_library(${PROJECT_NAME} STATIC)
target_include_directories(${PROJECT_NAME} PUBLIC ../include)
target_link_libraries(${PROJECT_NAME} PUBLIC KtmW32.lib)
target_sources(${PROJECT_NAME} PRIVATE
    ../include/perfect_loader.hpp
    ../include/pl/hook.hpp
    ../include/pl/lazy.hpp
    ../include/pl/mmap.hpp
    ../include/pl/pe.hpp
    ../include/pl/types.hpp

    hook.cpp
    loader.cpp
    mmap.cpp
)

add_library(${CLIB} SHARED)
target_link_libraries(${CLIB} PRIVATE ${PROJECT_NAME})
target_sources(${CLIB} PRIVATE
    ../include/perfect_loader.h
    pl.cpp)

if (${MAIN_PROJECT})
    add_executable(run)
    target_link_libraries(run PRIVATE ${CLIB} ${PROJECT_NAME})
    target_sources(run PRIVATE run.cpp)

    add_library(testdll SHARED)
    target_link_libraries(testdll PRIVATE ${PROJECT_NAME})
    target_sources(testdll PRIVATE dllmain.cpp)

    install(TARGETS run testdll DESTINATION bin)
endif (${MAIN_PROJECT})

install(
    TARGETS ${CLIB} ${PROJECT_NAME}
	ARCHIVE DESTINATION lib
       	LIBRARY DESTINATION lib
        RUNTIME DESTINATION bin
	)

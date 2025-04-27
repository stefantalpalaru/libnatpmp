# CMake-4 got even crazier and errors out if the minimum required version is
# lower than 3.5. Yes, you read that right - they redefined boolean logic :-)
cmake_minimum_required(VERSION 3.5)
project(natpmp C)

add_definitions(-DNATPMP_STATICLIB -DENABLE_STRNATPMPERR)

if(WIN32)
    set(${PROJECT_NAME}_ADD_SOURCES
        wingettimeofday.c
    )
endif()

add_library(${PROJECT_NAME} STATIC
    getgateway.c
    natpmp.c
    ${${PROJECT_NAME}_ADD_SOURCES}
)

install(TARGETS ${PROJECT_NAME} DESTINATION lib)
install(FILES natpmp_declspec.h natpmp.h DESTINATION include)

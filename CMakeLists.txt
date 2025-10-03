cmake_minimum_required( VERSION 3.22 )

project( r8brain LANGUAGES C CXX )

add_library( ${PROJECT_NAME} STATIC )

target_sources( ${PROJECT_NAME}
    PRIVATE
        r8bbase.cpp
)

target_include_directories( ${PROJECT_NAME} PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)

target_compile_options( ${PROJECT_NAME} PRIVATE /fp:fast )

if( CMAKE_OSX_ARCHITECTURES )
  list( JOIN CMAKE_OSX_ARCHITECTURES "-" ARCH_NAME )
elseif( MSVC_CXX_ARCHITECTURE_ID )
  set( ARCH_NAME ${MSVC_CXX_ARCHITECTURE_ID} )
else()
  set( ARCH_NAME ${CMAKE_SYSTEM_PROCESSOR} )
endif()

STRING( TOLOWER "${ARCH_NAME}" ARCH_NAME )
set_target_properties( ${PROJECT_NAME} PROPERTIES
  PREFIX ""
  OUTPUT_NAME "lib_${ARCH_NAME}_${PROJECT_NAME}"
)
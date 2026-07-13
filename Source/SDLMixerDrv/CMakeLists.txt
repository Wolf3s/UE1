project(SDLMixerDrv C CXX)

set(SRC_FILES "SDLMixerDrv.cpp")

add_library(${PROJECT_NAME} ${LIB_TYPE} ${SRC_FILES})

if(PS2)
find_package(SDL2_mixer CONFIG REQUIRED)
else()
include(FindPkgConfig)
pkg_search_module(SDL2_MIXER REQUIRED SDL2_mixer)
endif()

target_include_directories(${PROJECT_NAME}
  PUBLIC
  ${CMAKE_CURRENT_SOURCE_DIR}/Inc
  PRIVATE
  ${SDL2_MIXER_INCLUDE_DIRS}
)

target_link_libraries(${PROJECT_NAME} ${SDL2_MIXER_LIBRARIES})

target_link_libraries(${PROJECT_NAME} Engine Core)

target_compile_definitions(${PROJECT_NAME} PRIVATE NOPENALDRV_EXPORTS UPACKAGE_NAME=${PROJECT_NAME})

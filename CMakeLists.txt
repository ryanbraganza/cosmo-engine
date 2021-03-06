cmake_minimum_required(VERSION 3.8)
project(cosmo_engine)

set(CMAKE_CXX_STANDARD 11)
SET(SDL_VERSION "SDL2")
INCLUDE(FindPkgConfig)

PKG_SEARCH_MODULE(SDL2 REQUIRED sdl2)
INCLUDE_DIRECTORIES(${SDL2_INCLUDE_DIRS})
SET(SDL_LIBS "${SDL2_LIBRARIES}")

set(SOURCE_FILES
        src/actor.c
        src/actor.h
        src/main.c
        src/player.c
        src/player.h src/game.h src/game.c src/palette.c src/palette.h src/util.h src/util.c src/sfx.c src/sfx.h)

include_directories(src)

add_executable(cosmo_engine ${SOURCE_FILES})

IF(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    TARGET_LINK_LIBRARIES(cosmo_engine ${SDL_LIBS} -Wl,-framework,Cocoa)
ENDIF(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")

IF(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    TARGET_LINK_LIBRARIES(cosmo_engine dl ${SDL_LIBS} )
ENDIF(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
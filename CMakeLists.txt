cmake_minimum_required(VERSION 3.0.0)

PROJECT(AntTweakBarSDL2)

set(INCLUDES
  include/AntPerfTimer.h
  include/AntTweakBar.h
  include/LoadOGL.h
  include/LoadOGLCore.h
  include/MiniGLFW.h
  include/MiniGLUT.h
  include/MiniSDL12.h
  include/MiniSDL13.h
  include/MiniSFML16.h
  include/TwBar.h
  include/TwColors.h
  include/TwDirect3D10.h
  include/TwDirect3D11.h
  include/TwDirect3D9.h
  include/TwFonts.h
  include/TwGraph.h
  include/TwMgr.h
  include/TwOpenGL.h
  include/TwOpenGLCore.h
  include/TwPrecomp.h
  include/d3d10vs2003.h
  include/resource.h
  )

set(SOURCES
  src/TwColors.cpp
  src/TwFonts.cpp
  src/TwOpenGL.cpp
  src/TwOpenGLCore.cpp
  src/TwBar.cpp
  src/TwMgr.cpp
  src/TwPrecomp.cpp
  src/LoadOGL.cpp
  src/LoadOGLCore.cpp
  src/TwEventGLFW.cpp
  src/TwEventGLUT.cpp
  src/TwEventSDL.cpp
  src/TwEventSDL12.cpp
  src/TwEventSDL13.cpp
  src/TwEventSDL20.cpp
  src/TwEventSFML.cpp
  src/TwEventX11.cpp
  )
  
set(LIB_NAME AntTweakBar)


set(STATIC_LIB_TARGET  ${LIB_NAME}   )
set(DYNAMIC_LIB_TARGET ${LIB_NAME}Dyn)

ADD_LIBRARY(${STATIC_LIB_TARGET}  "STATIC" ${INCLUDES} ${SOURCES})
ADD_LIBRARY(${DYNAMIC_LIB_TARGET} "SHARED" ${INCLUDES} ${SOURCES})
  
set(Internal_inc "${AntTweakBarSDL2_SOURCE_DIR}/include")

SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D_UNIX")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -D__PLACEMENT_NEW_INLINE")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall")
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fno-strict-aliasing")

set_target_properties(${STATIC_LIB_TARGET} PROPERTIES
  INCLUDE_DIRECTORIES "${Internal_inc}"
  OUTPUT_NAME ${LIB_NAME}
)

set_target_properties(${DYNAMIC_LIB_TARGET} PROPERTIES
  INCLUDE_DIRECTORIES "${Internal_inc}"
  OUTPUT_NAME ${LIB_NAME}
)

install(FILES
  include/AntTweakBar.h
  DESTINATION include
  )

install(TARGETS ${STATIC_LIB_TARGET}
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
  )

install(TARGETS ${DYNAMIC_LIB_TARGET}
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
  )


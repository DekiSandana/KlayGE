SET(DXBC2GLSL_PROJECT_DIR "${KLAYGE_ROOT_DIR}/DXBC2GLSL")

SET(DXBC2GLSL_OUTPUT_DIR "${DXBC2GLSL_PROJECT_DIR}/lib/${KLAYGE_PLATFORM_NAME}")

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${DXBC2GLSL_OUTPUT_DIR})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_DEBUG ${DXBC2GLSL_OUTPUT_DIR})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELEASE ${DXBC2GLSL_OUTPUT_DIR})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_RELWITHDEBINFO ${DXBC2GLSL_OUTPUT_DIR})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY_MINSIZEREL ${DXBC2GLSL_OUTPUT_DIR})

ADD_SUBDIRECTORY(DXBC2GLSLLib)
ADD_SUBDIRECTORY(DXBC2GLSLCmd)
ADD_SUBDIRECTORY(DXBCDisasm)

if (KLAYGE_PLATFORM_WINDOWS_STORE)
	return()
endif()

FIND_PACKAGE(GLES)

IF(NOT KLAYGE_GLES_FOUND)
	return()
ENDIF()

SET(LIB_NAME KlayGE_RenderEngine_OpenGLES)

SET(OPENGLES_RE_SOURCE_FILES
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESFence.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESFrameBuffer.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESGraphicsBuffer.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESQuery.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESRenderEngine.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESRenderFactory.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESRenderLayout.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESRenderStateObject.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESRenderView.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESRenderWindow.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESShaderObject.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESTexture.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESTexture1D.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESTexture2D.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESTexture3D.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESTextureCube.cpp
	${KLAYGE_PROJECT_DIR}/Plugins/Src/Render/OpenGLES/OGLESUtil.cpp
)

SET(OPENGLES_RE_HEADER_FILES
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESFence.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESFrameBuffer.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESGraphicsBuffer.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESQuery.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESRenderEngine.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESRenderFactory.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESRenderLayout.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESRenderStateObject.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESRenderView.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESRenderWindow.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESShaderObject.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESTexture.hpp
	${KLAYGE_PROJECT_DIR}/Plugins/Include/KlayGE/OpenGLES/OGLESUtil.hpp
)

SOURCE_GROUP("Source Files" FILES ${OPENGLES_RE_SOURCE_FILES})
SOURCE_GROUP("Header Files" FILES ${OPENGLES_RE_HEADER_FILES})

ADD_LIBRARY(${LIB_NAME} ${KLAYGE_PREFERRED_LIB_TYPE}
	${OPENGLES_RE_SOURCE_FILES} ${OPENGLES_RE_HEADER_FILES}
)

target_compile_definitions(${LIB_NAME}
	PRIVATE
		-DGLLOADER_GLES_SUPPORT
)

target_include_directories(${LIB_NAME}
	PRIVATE
		${KLAYGE_PROJECT_DIR}/Plugins/Include
)

SET_TARGET_PROPERTIES(${LIB_NAME} PROPERTIES
	PROJECT_LABEL ${LIB_NAME}
	OUTPUT_NAME ${LIB_NAME}${KLAYGE_OUTPUT_SUFFIX}
	FOLDER "KlayGE/Engine/Plugins/Render"
)
if(KLAYGE_PREFERRED_LIB_TYPE STREQUAL "SHARED")
	set_target_properties(${LIB_NAME} PROPERTIES
		CXX_VISIBILITY_PRESET hidden
		VISIBILITY_INLINES_HIDDEN ON
	)
endif()

KLAYGE_ADD_PRECOMPILED_HEADER(${LIB_NAME} "${KLAYGE_PROJECT_DIR}/Core/Include/KlayGE/KlayGE.hpp")

target_link_libraries(${LIB_NAME}
	PRIVATE
		${KLAYGE_CORELIB_NAME}
		glloader_es
)
if(KLAYGE_IS_DEV_PLATFORM)
	target_link_libraries(${LIB_NAME}
		PRIVATE
			DXBC2GLSLLib
	)
endif()

ADD_DEPENDENCIES(AllInEngine ${LIB_NAME})

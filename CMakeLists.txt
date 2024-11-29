cmake_minimum_required (VERSION 3.8)

# Enable Hot Reload for MSVC compilers if supported.
if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("dollsstudio")

add_executable (dollsstudio WIN32 "SampleViewer.cpp")

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET dollsstudio PROPERTY CXX_STANDARD 17)
endif()

target_compile_definitions (dollsstudio PUBLIC 
    PLATFORM_WIN32
    D3D12_SUPPORTED
    _MSC_VER=1941
	)

target_include_directories (dollsstudio PRIVATE
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Common/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Graphics/GraphicsEngine/include
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Graphics/GraphicsEngine/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Graphics/GraphicsTools/include
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Graphics/GraphicsTools/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentTools/TextureLoader/include
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentTools/TextureLoader/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Platforms/include
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Platforms/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentTools/ThirdParty/imgui
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentTools/Imgui/interface 
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentTools/NativeApp/include
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Graphics/GraphicsAccessories/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentFX/Components/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentFX/PostProcess/Common/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentFX/PostProcess/ScreenSpaceReflection/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentFX
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Platforms/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Primitives/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentTools/AssetLoader/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentFX/PBR/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Platforms/Basic/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Platforms/Basic/include
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Platforms/Win32/interface
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Graphics/GraphicsEngineD3D12/include
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/DiligentCore/Graphics/GraphicsEngineD3D12/interface
    ${PROJECT_SOURCE_DIR}/SampleBase/include
    ${PROJECT_SOURCE_DIR}/SampleBase/include/Win32
	)

file (GLOB sources
${PROJECT_SOURCE_DIR}/SampleViewer.cpp
${PROJECT_SOURCE_DIR}/SampleBase/src/SampleApp.cpp 
${PROJECT_SOURCE_DIR}/SampleBase/src/SampleBase.cpp 
${PROJECT_SOURCE_DIR}/SampleBase/src/FirstPersonCamera.cpp
${PROJECT_SOURCE_DIR}/SampleBase/src/Win32/InputControllerWin32.cpp
${PROJECT_SOURCE_DIR}/SampleBase/src/Win32/SampleAppWin32.cpp
${PROJECT_SOURCE_DIR}/SampleViewer.hpp
${PROJECT_SOURCE_DIR}/SampleBase/include/SampleApp.hpp 
${PROJECT_SOURCE_DIR}/SampleBase/include/SampleBase.hpp 
${PROJECT_SOURCE_DIR}/SampleBase/include/FirstPersonCamera.hpp 
${PROJECT_SOURCE_DIR}/SampleBase/include/InputController.hpp 
${PROJECT_SOURCE_DIR}/SampleBase/include/TrackballCamera.hpp
${PROJECT_SOURCE_DIR}/SampleBase/include/Win32/InputControllerWin32.hpp
	)

target_sources (dollsstudio PRIVATE ${sources})

target_link_libraries (dollsstudio PRIVATE 
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentTools/NativeApp/Debug/Diligent-NativeAppBase.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentTools/AssetLoader/Debug/Diligent-AssetLoader.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentFX/Debug/DiligentFX.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsEngineD3D11/Debug/GraphicsEngineD3D11_64d.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsEngineD3D12/Debug/GraphicsEngineD3D12_64d.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsEngineOpenGL/Debug/GraphicsEngineOpenGL_64d.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsEngineVulkan/Debug/GraphicsEngineVk_64d.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentTools/TextureLoader/Debug/Diligent-TextureLoader.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentTools/ThirdParty/libpng/Debug/libpng16_staticd.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentTools/ThirdParty/libtiff/Debug/LibTiff.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentTools/ThirdParty/Debug/ZLib.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentTools/ThirdParty/libjpeg-9e/Debug/LibJpeg.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentTools/Imgui/Debug/Diligent-Imgui.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsTools/Debug/Diligent-GraphicsTools.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/ThirdParty/xxHash/cmake_unofficial/Debug/xxhash.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/Archiver/Debug/Diligent-Archiver-static.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsEngineD3D11/Debug/Diligent-GraphicsEngineD3D11-static.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsEngineD3D12/Debug/Diligent-GraphicsEngineD3D12-static.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsEngineVulkan/Debug/Diligent-GraphicsEngineVk-static.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsEngineNextGenBase/Debug/Diligent-GraphicsEngineNextGenBase.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsEngineOpenGL/Debug/Diligent-GraphicsEngineOpenGL-static.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/ThirdParty/SPIRV-Cross/Debug/spirv-cross-glsld.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/ThirdParty/glew/Debug/glew-static.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsEngineD3DBase/Debug/Diligent-GraphicsEngineD3DBase.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/HLSL2GLSLConverterLib/Debug/Diligent-HLSL2GLSLConverterLib.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/ShaderTools/Debug/Diligent-ShaderTools.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsEngine/Debug/Diligent-GraphicsEngine.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Graphics/GraphicsAccessories/Debug/Diligent-GraphicsAccessories.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Common/Debug/Diligent-Common.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Platforms/Win32/Debug/Diligent-Win32Platform.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Platforms/Basic/Debug/Diligent-BasicPlatform.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/Primitives/Debug/Diligent-Primitives.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/ThirdParty/SPIRV-Cross/Debug/spirv-cross-cored.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/ThirdParty/glslang/SPIRV/Debug/SPIRVd.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/ThirdParty/glslang/glslang/Debug/glslangd.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/ThirdParty/SPIRV-Tools/source/opt/Debug/SPIRV-Tools-opt.lib
    ${PROJECT_SOURCE_DIR}/../DiligentEngine/build/DiligentCore/ThirdParty/SPIRV-Tools/source/Debug/SPIRV-Tools.lib
	)	



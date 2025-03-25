cmake_minimum_required(VERSION 3.20)
project(OpenGL_Learning)

# 设置目标属性前必须先创建目标
add_executable(${PROJECT_NAME}
    src/main.cpp
    # 包含glad加载器实现（关键！）
    ${CMAKE_CURRENT_SOURCE_DIR}/3rd/Includes/glad/glad.c
)

# 三级包含目录设置（精确匹配项目结构）
target_include_directories(${PROJECT_NAME} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/3rd/Includes   # 主包含目录
    ${CMAKE_CURRENT_SOURCE_DIR}/3rd/Includes/glad  # 二级glad目录
    ${CMAKE_CURRENT_SOURCE_DIR}/3rd/Includes/GLFW  # 二级GLFW目录
)

# Windows平台专用配置
if(WIN32)
    # 链接库路径（根据实际架构调整）
    if(CMAKE_SIZEOF_VOID_P EQUAL 8)
        link_directories(${CMAKE_CURRENT_SOURCE_DIR}/3rd/Libs/x64)
    else()
        link_directories(${CMAKE_CURRENT_SOURCE_DIR}/3rd/Libs/x86)
    endif()

    # 必需链接库
    target_link_libraries(${PROJECT_NAME} PRIVATE
        opengl32.lib
       ${CMAKE_CURRENT_SOURCE_DIR}/3rd/Libs/glfw3.lib
    )

endif()
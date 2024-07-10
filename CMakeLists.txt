#[[

    cmake  주석 및 여러줄 주석
    주석 : # 을 입력 하면 주석 처리 됨.

    여러줄 주석 :

    #[[

        주석 처리될 문구
    \]\] 위와 같이

#[[ \]\]으로 사용 하면 된다.


]]

# cmake는 3.14버전 이상일 것
cmake_minimum_required(VERSION 3.14)


#[[
    - set 은 변수 세팅
    
        ex) set(변수명 string)
        변수명에 string 대입

    - 변수의 값 사용 방법 

        ${변수명} 

        ex) project(${PROJECT_NAME})
        
        if) 변수명 이렇게 쓰면 string형식(즉,문자열)로 들어간다.

]]
set(PROJECT_NAME cmake_project_example)
# CXX는 C++를 뉘어서 쓴 문장, CMAKE로 시작하는 변수는 글로벌 변수 
set(CMAKE_CXX_STANDARD 17)

#cmake부분에서 정의해주기
set(WINDOW_NAME "Hello, OpenGL!")
set(WINDOW_WIDTH 640)
set(WINDOW_HEIGHT 480)

#프로젝트 세팅
project(${PROJECT_NAME})
#실행 파일 만들건데, main.cpp 컴파일 해서
add_executable(${PROJECT_NAME} src/main.cpp)

include(Dependency.cmake)

# 우리 프로젝트에 include / lib 관련 옵션 추가
target_include_directories(${PROJECT_NAME} PUBLIC ${DEP_INCLUDE_DIR})
target_link_directories(${PROJECT_NAME} PUBLIC ${DEP_LIB_DIR})
target_link_libraries(${PROJECT_NAME} PUBLIC ${DEP_LIBS})

#cmake부분에서 정의해주기
target_compile_definitions(${PROJECT_NAME} PUBLIC
  WINDOW_NAME="${WINDOW_NAME}"
  WINDOW_WIDTH=${WINDOW_WIDTH}
  WINDOW_HEIGHT=${WINDOW_HEIGHT}
  )

# Dependency들이 먼저 build 될 수 있게 관계 설정
add_dependencies(${PROJECT_NAME} ${DEP_LIST})
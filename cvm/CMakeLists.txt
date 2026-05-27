cmake_minimum_required(VERSION 3.10)
project(cvmplusplus)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

include_directories(src)

set(CORE_SOURCES
    src/lexer.cpp
    src/parser.cpp
    src/compiler.cpp
    src/vm.cpp
)

add_executable(cvm src/main.cpp ${CORE_SOURCES})

add_executable(test_lexer tests/test_lexer.cpp ${CORE_SOURCES})

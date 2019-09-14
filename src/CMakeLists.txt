INCLUDE_DIRECTORIES(.)

# Source
SET(ADD_HEADERS

)

SET(ADD_SOURCE
   
)


FIND_PACKAGE(LLVM REQUIRED CONFIG)
FIND_PACKAGE(Clang REQUIRED CONFIG)
message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "Using LLVMConfig.cmake in: ${LLVM_DIR}")

include_directories(${LLVM_INCLUDE_DIRS})
add_definitions(${LLVM_DEFINITIONS})


llvm_map_components_to_libnames(llvm_libs
    Core
    ExecutionEngine
    MC
    MCJIT
    Object
    OrcJit
    Option
    RuntimeDyld
    Support
    native)
# target_include_directories

ADD_EXECUTABLE(main main.cpp ${ADD_SOURCE} ${ADD_HEADERS})
TARGET_LINK_LIBRARIES(main
    clangBasic
    clangCodeGen
    clangDriver
    clangFrontend
    clangSerialization
    LLVM
)

SET(${CXX_STANDARD_REQUIRED} ON)
SET_PROPERTY(TARGET main PROPERTY CXX_STANDARD 11)



cmake_minimum_required (VERSION 2.7)
project (evernote)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH}
	"${CMAKE_SOURCE_DIR}/cmake/Modules/")

find_package(Thrift REQUIRED)

MESSAGE( STATUS "Thrift: " ${THRIFT_INCLUDE_DIR} )
MESSAGE( STATUS "Thrift: " ${THRIFT_LIBRARIES} )

include_directories(${Thrift_INCLUDE_DIR})
set(LIBS ${LIBS} ${Thrift_LIBRARIES})

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
add_library(evernote SHARED src/Errors_constants.cpp  src/Limits_types.cpp
	src/NoteStore_types.cpp  src/UserStore_constants.cpp
	src/Errors_types.cpp      src/NoteStore_constants.cpp
	src/Types_constants.cpp  src/UserStore.cpp
	src/Limits_constants.cpp  src/NoteStore.cpp
	src/Types_types.cpp      src/UserStore_types.cpp)

# Install library
install(TARGETS ${PROJECT_NAME} DESTINATION lib)

# Install library headers
file(GLOB HEADERS include/*.h)
install(FILES ${HEADERS} DESTINATION include/${PROJECT_NAME})

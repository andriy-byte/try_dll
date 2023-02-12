cmake_minimum_required(VERSION 3.22)
project(experience)

set(CMAKE_CXX_STANDARD 23)


message(STATUS "Project source directory ${PROJECT_SOURCE_DIR}")

# set(EXTERNAL_LIBS_ROOT "${PROJECT_SOURCE_DIR}/externallib")

# add_subdirectory("${EXTERNAL_LIBS_ROOT}/template-string")
# include_directories("${EXTERNAL_LIBS_ROOT}/template-string/include")

#if (WIN32)
#    include_directories("${EXTERNAL_LIBS_ROOT}/template-string/lib/Debug")
#endif (WIN32)

# if (UNIX)
#     include_directories("${EXTERNAL_LIBS_ROOT}/template-string/lib")
# endif (UNIX)

add_executable(experience main.cpp)

set_target_properties(${PROJECT_NAME}
        PROPERTIES
        ARCHIVE_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/lib"
        LIBRARY_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/lib"
        RUNTIME_OUTPUT_DIRECTORY "${PROJECT_SOURCE_DIR}/bin"
        )


if (WIN32)
#    include("${CMAKE_SOURCE_DIR}/conan/windows/conan_paths.cmake")
    include("C:\\vcpkg\\scripts\\buildsystems\\vcpkg.cmake")
    include_directories(C:\\vcpkg\\installed\\x64-windows\\include\\)
    link_directories(C:\\vcpkg\\installed\\x64-windows\\lib\\)

endif (WIN32)

if (UNIX)

    #    include("${CMAKE_SOURCE_DIR}/conan/linux/conan_paths.cmake")
    include("/opt/vcpkg/scripts/buildsystems/vcpkg.cmake")
    include_directories(/opt/vcpkg/installed/x64-linux/include/)
    link_directories(/opt/vcpkg/installed/x64-linux/lib/)

endif (UNIX)

find_package(fmt REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC fmt::fmt)

find_package(Boost REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC ${Boost_LIBRARIES})
if (Boost_FOUND)
    include_directories(${Boost_INCLUDE_DIRS})
    target_link_libraries(${PROJECT_NAME} PUBLIC ${Boost_LIBRARIES})
endif ()

find_package(range-v3 REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC range-v3::range-v3)

find_package(re2 REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC re2::re2)

find_package(folly)
target_link_libraries(${PROJECT_NAME} PUBLIC Folly::folly)

find_package(argparse REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC argparse::argparse)

find_package(Eigen3 REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC Eigen3::Eigen)

# find_package( args-parser REQUIRED )
# target_link_libraries(${PROJECT_NAME} PUBLIC args-parser::args-parser)
find_package(spdlog REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC spdlog::spdlog)

find_package(nlohmann_json REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC nlohmann_json::nlohmann_json)

find_package(tabulate REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC tabulate::tabulate)

find_package(OpenSSL REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC OpenSSL::Crypto)

find_package(sciplot REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC sciplot::sciplot)

find_package(cryptopp REQUIRED)
target_link_libraries(${PROJECT_NAME} PUBLIC cryptopp::cryptopp)
# Copyright © 2023 Pascal JEAN, epsilonrt <epsilonrt@gmail.com>
#
# SPDX-License-Identifier: BSD-1-Clause
#
# @file tests/CMakeLists.txt 

configure_file( ${CMAKE_CURRENT_SOURCE_DIR}/unit-test.h.in 
                ${CMAKE_CURRENT_BINARY_DIR}/unit-test.h @ONLY)

function(configure_libmodbus_test target)
  target_link_libraries(${target} PRIVATE ${PROJECT_SHORTNAME})
  # if(NOT BUILD_SHARED_LIBS AND MSVC)
  #   target_compile_options(${target} PRIVATE /MT)
  #   target_link_options(${target} PRIVATE /INCREMENTAL:NO /NODEFAULTLIB:MSVCRT)
  # endif()

  target_include_directories(${target} BEFORE PRIVATE
    ${CMAKE_BINARY_DIR}
    ${CMAKE_CURRENT_BINARY_DIR}
    ${LIBMODBUS_SRC_DIR}
  )
endfunction()

add_executable(version version.c)
configure_libmodbus_test(version)
add_test(NAME version COMMAND version)

add_executable(random-test-client random-test-client.c)
configure_libmodbus_test(random-test-client)
add_test(NAME random-test-client COMMAND random-test-client)

add_executable(random-test-server random-test-server.c)
configure_libmodbus_test(random-test-server)

add_executable(bandwidth-client bandwidth-client.c)
configure_libmodbus_test(bandwidth-client)
add_test(NAME bandwidth-client COMMAND bandwidth-client)

add_executable(bandwidth-server-one bandwidth-server-one.c)
configure_libmodbus_test(bandwidth-server-one)

add_executable(unit-test-server unit-test-server.c)
configure_libmodbus_test(unit-test-server)

add_executable(unit-test-client unit-test-client.c)
configure_libmodbus_test(unit-test-client)
add_test(NAME unit-test-client COMMAND unit-test-client)



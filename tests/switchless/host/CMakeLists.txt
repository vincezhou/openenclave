# Copyright (c) Open Enclave SDK contributors.
# Licensed under the MIT License.

set(EDL_FILE ../switchless.edl)

add_custom_command(
  OUTPUT switchless_u.h switchless_u.c
  DEPENDS ${EDL_FILE} edger8r
  COMMAND edger8r --untrusted ${EDL_FILE} --search-path
          ${CMAKE_CURRENT_SOURCE_DIR})

add_executable(switchless_host host.c switchless_u.c)

target_include_directories(switchless_host PRIVATE ${CMAKE_CURRENT_BINARY_DIR})
target_link_libraries(switchless_host oehostapp)

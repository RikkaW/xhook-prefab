cmake_minimum_required(VERSION 3.4.1)

project(xhook)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra -Werror -fvisibility=hidden -Wno-builtin-macro-redefined -D__FILE__=__FILE_NAME__")

add_library(xhook STATIC xhook.c xh_core.c xh_elf.c xh_log.c xh_util.c xh_version.c)
include_directories("include")
target_link_libraries(xhook)

add_custom_command(TARGET xhook POST_BUILD
        COMMAND ${CMAKE_OBJCOPY} --remove-section=.comment --strip-debug "libxhook.a")

cmake_minimum_required(VERSION 3.21)

project(socket)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 使用 clang++
# set(CMAKE_CXX_COMPILER g++)
set(CMAKE_CXX_COMPILER clang++)

# 使用 ninja
set(CMAKE_GENERATOR Ninja)

# 添加可执行文件
add_executable(ch01-server ch01/server.cc)
add_executable(ch01-client ch01/client.cc)
add_executable(ch01-fd-spec ch01/fd-spec.cc)
add_executable(ch01-rw-spec ch01/rw-spec.cc)

add_executable(ch02-tcp-client ch02/tcp-client.cc)
add_executable(ch02-tcp-server ch02/tcp-server.cc)

add_executable(ch03-inet-spec ch03/inet-spec.cc)

add_executable(ch04-echo-client ch04/echo-client.cc)
add_executable(ch04-echo-server ch04/echo-server.cc)

add_executable(ch06-conn-client ch06/conn-client.cc)
add_executable(ch06-udp-client ch06/udp-client.cc)
add_executable(ch06-udp-server ch06/udp-server.cc)

add_executable(ch07-file-client ch07/file-client.cc)
add_executable(ch07-file-server ch07/file-server.cc)

add_executable(ch08-get-host-by-addr-spec ch08/get-host-by-addr-spec.cc)
add_executable(ch08-get-host-by-name-spec ch08/get-host-by-name-spec.cc)

add_executable(ch09-reuse-addr-server ch09/reuse-addr-server.cc)
add_executable(ch09-sock-opt-spec ch09/sock-opt-spec.cc)

add_executable(ch10-fork-spec ch10/fork-spec.cc)
add_executable(ch10-kill-zombie-spec ch10/kill-zombie-spec.cc)
add_executable(ch10-proc-client ch10/proc-client.cc)
add_executable(ch10-proc-server ch10/proc-server.cc)
add_executable(ch10-sig-action-spec ch10/sig-action-spec.cc)
add_executable(ch10-signal-spec ch10/signal-spec.cc)
add_executable(ch10-wait-pid-spec ch10/wait-pid-spec.cc)
add_executable(ch10-wait-spec ch10/wait-spec.cc)
add_executable(ch10-zombie-spec ch10/zombie-spec.cc)

add_executable(ch11-pipe-server ch11/pipe-server.cc)
add_executable(ch11-pipe-spec ch11/pipe-spec.cc)
add_executable(ch11-pipe-spec2 ch11/pipe-spec2.cc)
add_executable(ch11-pipe-spec3 ch11/pipe-spec3.cc)

add_executable(ch12-select-server ch12/select-server.cc)
add_executable(ch12-select-spec ch12/select-spec.cc)

add_executable(ch13-oob-client ch13/oob-client.cc)
add_executable(ch13-oob-server ch13/oob-server.cc)
add_executable(ch13-peek-client ch13/peek-client.cc)
add_executable(ch13-peek-server ch13/peek-server.cc)
add_executable(ch13-readv-spec ch13/readv-spec.cc)
add_executable(ch13-writev-spec ch13/writev-spec.cc)

add_executable(ch14-broadcast-client ch14/broadcast-client.cc)
add_executable(ch14-broadcast-server ch14/broadcast-server.cc)
add_executable(ch14-multicast-client ch14/multicast-client.cc)
add_executable(ch14-multicast-server ch14/multicast-server.cc)

add_executable(ch15-io-spec ch15/io-spec.cc)
add_executable(ch15-fd-fp-spec ch15/fd-fp-spec.cc)
add_executable(ch15-echo-client ch15/echo-client.cc)
add_executable(ch15-echo-server ch15/echo-server.cc)

add_executable(ch16-client ch16/client.cc)
add_executable(ch16-server ch16/server.cc)
add_executable(ch16-server2 ch16/server2.cc)
add_executable(ch16-dup-spec ch16/dup-spec.cc)

add_executable(ch17-epoll-server ch17/epoll-server.cc)

add_executable(ch18-pthread ch18/pthread.cc)
add_executable(ch18-pthread2 ch18/pthread2.cc)
add_executable(ch18-pthread3 ch18/pthread3.cc)
add_executable(ch18-pthread4 ch18/pthread4.cc)
add_executable(ch18-pthread-client ch18/pthread-client.cc)
add_executable(ch18-pthread-server ch18/pthread-server.cc)

add_executable(ch24-http-server ch24/http-server.cc)

add_executable(send-file ./send-file.cc)

# 查找 pthread 库
find_package(Threads REQUIRED)

# 链接 pthread 库
target_link_libraries(ch18-pthread  Threads::Threads)
target_link_libraries(ch18-pthread2 Threads::Threads)
target_link_libraries(ch18-pthread3 Threads::Threads)
target_link_libraries(ch18-pthread4 Threads::Threads)
target_link_libraries(ch18-pthread-client Threads::Threads)
target_link_libraries(ch18-pthread-server Threads::Threads)
target_link_libraries(ch24-http-server Threads::Threads)

find_program(CLANG_FORMAT clang-format)

# 使用 clang-format
if(CLANG_FORMAT)
  add_custom_target(format ALL
    COMMAND ${CLANG_FORMAT} -i -style=google
    ${CMAKE_SOURCE_DIR}/ch01/*.cc
    ${CMAKE_SOURCE_DIR}/ch02/*.cc
    ${CMAKE_SOURCE_DIR}/ch03/*.cc
    ${CMAKE_SOURCE_DIR}/ch04/*.cc
    ${CMAKE_SOURCE_DIR}/ch06/*.cc
    ${CMAKE_SOURCE_DIR}/ch07/*.cc
    ${CMAKE_SOURCE_DIR}/ch08/*.cc
    ${CMAKE_SOURCE_DIR}/ch09/*.cc
    ${CMAKE_SOURCE_DIR}/ch10/*.cc
    ${CMAKE_SOURCE_DIR}/ch11/*.cc
    ${CMAKE_SOURCE_DIR}/ch12/*.cc
    ${CMAKE_SOURCE_DIR}/ch13/*.cc
    ${CMAKE_SOURCE_DIR}/ch14/*.cc
    ${CMAKE_SOURCE_DIR}/ch15/*.cc
    ${CMAKE_SOURCE_DIR}/ch16/*.cc
    ${CMAKE_SOURCE_DIR}/ch17/*.cc
    ${CMAKE_SOURCE_DIR}/ch18/*.cc
    ${CMAKE_SOURCE_DIR}/ch24/*.cc
    ${CMAKE_SOURCE_DIR}/*.cc
  )
else()
  message(WARNING "clang-format not found")
endif()

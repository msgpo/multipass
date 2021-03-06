target_sources(multipass_tests
  PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/test_qemu_backend.cpp
    ${CMAKE_CURRENT_LIST_DIR}/test_qemu_vm_process_spec.cpp
    ${CMAKE_CURRENT_LIST_DIR}/test_qemu_vmstate_process_spec.cpp
    ${CMAKE_CURRENT_LIST_DIR}/test_dnsmasq_server.cpp
    ${CMAKE_CURRENT_LIST_DIR}/test_dnsmasq_process_spec.cpp
    ${CMAKE_CURRENT_LIST_DIR}/test_iptables_config.cpp
)

add_executable(qemu-system-x86_64
        mock_qemu_system.cpp)

set_target_properties(qemu-system-x86_64
        PROPERTIES
        RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/mocks"
        RUNTIME_OUTPUT_DIRECTORY_DEBUG "${CMAKE_BINARY_DIR}/bin/mocks"
        RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/mocks")

target_link_libraries(qemu-system-x86_64
        Qt5::Core)

add_executable(dnsmasq
  mock_dnsmasq_server.cpp)

set_target_properties(dnsmasq
  PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/mocks"
  RUNTIME_OUTPUT_DIRECTORY_DEBUG "${CMAKE_BINARY_DIR}/bin/mocks"
  RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/mocks")

target_link_libraries(dnsmasq
        Qt5::Core)

add_executable(dhcp_release
  mock_dhcp_release.cpp)

set_target_properties(dhcp_release
  PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/mocks"
  RUNTIME_OUTPUT_DIRECTORY_DEBUG "${CMAKE_BINARY_DIR}/bin/mocks"
  RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/mocks")

add_executable(qemu-img
  mock_qemuimg.cpp)

set_target_properties(qemu-img
  PROPERTIES
  RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin/mocks"
  RUNTIME_OUTPUT_DIRECTORY_DEBUG "${CMAKE_BINARY_DIR}/bin/mocks"
  RUNTIME_OUTPUT_DIRECTORY_RELEASE "${CMAKE_BINARY_DIR}/bin/mocks")

add_dependencies(multipass_tests
  qemu-system-x86_64
  dnsmasq
  dhcp_release
  qemu-img
)

cmake_minimum_required(VERSION 3.5)

# name your project here
set(ProjectName myproject)

include(pico_sdk_import.cmake)

project(${ProjectName})

pico_sdk_init()

add_compile_options(
	-Wall
	-Wno-format
	-Wno-unused-function
	-Wno-maybe-uninitialized
	-Wextra    			# optional
)

add_executable(${ProjectName})

target_sources(${ProjectName} PRIVATE ${ProjectName}.c)

add_subdirectory(${ProjectName}_library)

target_link_libraries(${ProjectName} PRIVATE
	pico_stdlib
	hardware_pio
	${ProjectName}_library)

pico_add_extra_outputs(${ProjectName})

pico_enable_stdio_usb(${ProjectName} 0)
pico_enable_stdio_uart(${ProjectName} 1)

# example_auto_set_url(${ProjectName})

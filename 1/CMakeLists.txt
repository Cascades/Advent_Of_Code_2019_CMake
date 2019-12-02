project(Advent_Of_Code_1)

cmake_minimum_required(VERSION 3.15)

set(ADVENT_OF_CODE_1_DIR ${CMAKE_CURRENT_LIST_DIR})

function(read_input_data)
	FILE(READ ${ADVENT_OF_CODE_1_DIR}/input_data.txt data_var)
	STRING(REGEX REPLACE "\n" ";" data_var ${data_var})
	set(data ${data_var} PARENT_SCOPE)
endfunction()


macro(calc_fuel_req input_value output_var)
	math(EXPR ${output_var} "(${input_value} / 3) - 2" OUTPUT_FORMAT DECIMAL)
endmacro()

macro(advent_of_code_1)
	message(STATUS "Reading input file to list...")
	read_input_data()
	
	set(sum 0)
	
	message(STATUS "Calculating sum...")
	
	foreach(num ${data})
		message(STATUS ${num})
		calc_fuel_req(${num} value)
		message(STATUS "|_ ${value}")
		math(EXPR sum "${sum} + ${value}" OUTPUT_FORMAT DECIMAL)
	endforeach()
	
	message(STATUS "Final sum: ${sum}")
endmacro()

if(${CMAKE_CURRENT_LIST_DIR} STREQUAL ${CMAKE_SOURCE_DIR})
	advent_of_code_1()
endif()

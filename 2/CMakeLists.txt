project(Advent_Of_Code_1)

cmake_minimum_required(VERSION 3.15)

include(../1/CMakeLists.txt)

message(STATUS "Reading input file to list...")

read_input_data()

set(sum 0)

message(STATUS "Calculating sum...")

foreach(num ${data})
	message(STATUS ${num})
	calc_fuel_req(${num} value)
	set(fuel_total ${value})
	while(${value} GREATER 0)
		calc_fuel_req(${value} value)
		if(${value} GREATER 0)
			math(EXPR fuel_total "${fuel_total} + ${value}" OUTPUT_FORMAT DECIMAL)
		endif()
	endwhile()
	message(STATUS "|_ ${fuel_total}")
	math(EXPR sum "${sum} + ${fuel_total}" OUTPUT_FORMAT DECIMAL)
endforeach()

message(STATUS "Final sum: ${sum}")

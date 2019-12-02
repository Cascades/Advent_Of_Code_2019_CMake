project(Advent_Of_Code_1)

cmake_minimum_required(VERSION 3.15)

message(STATUS "Reading input file to list...")

FILE(READ ${CMAKE_CURRENT_SOURCE_DIR}/input_data.txt data)
STRING(REGEX REPLACE "\n" ";" data ${data})

set(sum 0)

message(STATUS "Calculating sum...")

foreach(num ${data})
	message(STATUS ${num})
	math(EXPR value "(${num} / 3) - 2" OUTPUT_FORMAT DECIMAL)
	message(STATUS "|_ ${value}")
	math(EXPR sum "${sum} + ${value}" OUTPUT_FORMAT DECIMAL)
endforeach()

message(STATUS "Final sum: ${sum}")

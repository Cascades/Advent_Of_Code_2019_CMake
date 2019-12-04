project(Advent_Of_Code_1)

cmake_minimum_required(VERSION 3.15)

include(${CMAKE_CURRENT_SOURCE_DIR}/../2-1/CMakeLists.txt)

read_input_data()

foreach(noun RANGE 99)
	message(STATUS "Trying noun: ${noun} with verb: 0-99")
	set(verb_found 0)
	foreach(verb RANGE 99)
		run_computer("${data}" ${noun} ${verb} output_data)
		list(GET output_data 0 program_output)
		if(${program_output} EQUAL 19690720)
			message(STATUS "Found noun to be: ${noun} and verb to be: ${verb}")
			set(final_noun ${noun})
			set(final_verb ${verb})
			set(verb_found 1)
			break()
		endif()
	endforeach()
	if(${verb_found})
		break()
	endif()
endforeach()

MATH(EXPR output_value "(100 * ${final_noun}) + ${final_verb}" OUTPUT_FORMAT DECIMAL)
message(STATUS "100 * noun + verb = ${output_value}")

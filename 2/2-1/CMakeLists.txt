project(Advent_Of_Code_1)

cmake_minimum_required(VERSION 3.15)

set(ADVENT_OF_CODE_2_DIR ${CMAKE_CURRENT_LIST_DIR})

function(read_input_data)
	FILE(READ ${ADVENT_OF_CODE_2_DIR}/input_data.txt data_var)
	STRING(REGEX REPLACE "," ";" data_var ${data_var})
	set(data ${data_var} PARENT_SCOPE)
endfunction()

function(run_computer data pos_1 pos_2 output_data)

	macro(LIST_REPLACE LIST INDEX NEWVALUE)
		list(INSERT ${LIST} ${INDEX} ${NEWVALUE})
		MATH(EXPR __INDEX "${INDEX} + 1")
		list (REMOVE_AT ${LIST} ${__INDEX})
	endmacro(LIST_REPLACE)

	LIST_REPLACE(data 1 ${pos_1})
	LIST_REPLACE(data 2 ${pos_2})

	set(pc_offset 0)
	
	while(1)
		list(GET data ${pc_offset} opcode)
		if(${opcode} EQUAL 99)
			break()
		elseif(${opcode} EQUAL 1 OR ${opcode} EQUAL 2)
			MATH(EXPR operand_0_pos_pos "${pc_offset} + 1" OUTPUT_FORMAT DECIMAL) 
			list(GET data ${operand_0_pos_pos} operand_0_pos)
			list(GET data ${operand_0_pos} operand_0)
			MATH(EXPR operand_1_pos_pos "${pc_offset} + 2" OUTPUT_FORMAT DECIMAL)
	                list(GET data ${operand_1_pos_pos} operand_1_pos)
			list(GET data ${operand_1_pos} operand_1)
			MATH(EXPR output_pos_pos "${pc_offset} + 3" OUTPUT_FORMAT DECIMAL)
			list(GET data ${output_pos_pos} output_pos)
			if(${opcode} EQUAL 1)
				MATH(EXPR output "${operand_0} + ${operand_1}" OUTPUT_FORMAT DECIMAL)
			elseif(${opcode} EQUAL 2)
				MATH(EXPR output "${operand_0} * ${operand_1}" OUTPUT_FORMAT DECIMAL)
			endif()
			LIST_REPLACE(data ${output_pos} ${output})
		else()
			message(FATAL_ERROR "BAD_OPCODE")
		endif()
		MATH(EXPR pc_offset "${pc_offset} + 4" OUTPUT_FORMAT DECIMAL)
	endwhile()
	
	set(${output_data} "${data}" PARENT_SCOPE)
endfunction()

if(${CMAKE_CURRENT_LIST_DIR} STREQUAL ${CMAKE_SOURCE_DIR})
	read_input_data()

	run_computer("${data}" 12 2 data)
	
	string(REPLACE "," ";" pretty_data "${data}")
	
	message(STATUS "Final_state: ${pretty_data}")
endif()

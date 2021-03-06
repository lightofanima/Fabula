
#Flex/Bison things
find_package(FLEX REQUIRED)
find_package(BISON REQUIRED)
BISON_TARGET(Parser ${PARSER_DIR}/Grammar.ypp ${CMAKE_CURRENT_BINARY_DIR}/generated_parser.cpp)
FLEX_TARGET(Lexer ${PARSER_DIR}/Grammar.flex ${CMAKE_CURRENT_BINARY_DIR}/generated_lexer.cpp)
ADD_FLEX_BISON_DEPENDENCY(Lexer Parser)

message("Flex Output: ${FLEX_Lexer_OUTPUTS}")
message("Bison Output: ${BISON_Parser_OUTPUTS} ${BISON_Parser_OUTPUT_HEADER}")

add_library(FabulaParser
                Grammar.flex
                Grammar.ypp
                ${PARSER_SOURCES}
                ${PARSER_HEADERS}
                ${COMMON_SOURCES}
                ${BISON_Parser_OUTPUTS}
                ${FLEX_Lexer_OUTPUTS}
                )

include_directories(. ${PARSE_NODE_DIR} ${SRC_DIR}/third_party/poco/Foundation/include)
target_link_libraries(FabulaParser PocoFoundation)

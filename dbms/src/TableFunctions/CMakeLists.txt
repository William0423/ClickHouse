include(${ClickHouse_SOURCE_DIR}/cmake/dbms_glob_sources.cmake)
add_headers_and_sources(clickhouse_table_functions .)

list(REMOVE_ITEM clickhouse_table_functions_sources ITableFunction.cpp TableFunctionFactory.cpp)
list(REMOVE_ITEM clickhouse_table_functions_headers ITableFunction.h TableFunctionFactory.h)

add_library(clickhouse_table_functions ${clickhouse_table_functions_sources})
target_link_libraries(clickhouse_table_functions clickhouse_storages_system dbms ${Poco_Foundation_LIBRARY})

if (Poco_SQLODBC_FOUND)
    target_link_libraries (clickhouse_table_functions ${Poco_SQLODBC_LIBRARY})
    target_include_directories (clickhouse_table_functions PRIVATE ${ODBC_INCLUDE_DIRECTORIES} ${Poco_SQLODBC_INCLUDE_DIRS})
endif ()

if (Poco_DataODBC_FOUND)
    target_link_libraries (clickhouse_table_functions ${Poco_DataODBC_LIBRARY})
    target_include_directories (clickhouse_table_functions PRIVATE ${ODBC_INCLUDE_DIRECTORIES} ${Poco_DataODBC_INCLUDE_DIRS})
endif ()

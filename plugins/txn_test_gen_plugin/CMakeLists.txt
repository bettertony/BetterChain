file(GLOB HEADERS "include/betterchain/txn_test_gen_plugin/*.hpp")
add_library( txn_test_gen_plugin
             txn_test_gen_plugin.cpp
             ${HEADERS} )

target_link_libraries( txn_test_gen_plugin appbase fc http_plugin chain_plugin )
target_include_directories( txn_test_gen_plugin PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include" )

install( TARGETS
   txn_test_gen_plugin

   RUNTIME DESTINATION bin
   LIBRARY DESTINATION lib
   ARCHIVE DESTINATION lib
)
install( FILES ${HEADERS} DESTINATION "include/betterchain/txn_test_gen_plugin" )

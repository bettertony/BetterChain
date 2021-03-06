file(GLOB HEADERS "include/betterchain/chain/*.hpp" "include/betterchain/chain/contracts/*.hpp")

## SORT .cpp by most likely to change / break compile
add_library( betterchain_chain
             chain_config.cpp
             merkle.cpp
             name.cpp
             transaction.cpp
             block.cpp
             wast_to_wasm.cpp
             wasm_interface.cpp
             apply_context.cpp
             rate_limiting.cpp

             fork_database.cpp
             get_config.cpp
             block_log.cpp
             asset.cpp


             global_property_object.cpp
             chain_controller.cpp

             contracts/betterchain_contract.cpp
             contracts/producer_objects.cpp
             contracts/staked_balance_objects.cpp
             contracts/chain_initializer.cpp
             contracts/genesis_state.cpp
             contracts/abi_serializer.cpp


             ${HEADERS}
        )

target_link_libraries( betterchain_chain betterchain_utilities fc chainbase Logging IR WAST WASM Runtime )
target_include_directories( betterchain_chain
                            PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include" "${CMAKE_CURRENT_BINARY_DIR}/include"
                                   "${CMAKE_CURRENT_SOURCE_DIR}/../wasm-jit/Include"
                            )

if(MSVC)
  set_source_files_properties( db_init.cpp db_block.cpp database.cpp block_log.cpp PROPERTIES COMPILE_FLAGS "/bigobj" )
endif(MSVC)

INSTALL( TARGETS
   betterchain_chain

   RUNTIME DESTINATION bin
   LIBRARY DESTINATION lib
   ARCHIVE DESTINATION lib
)
INSTALL( FILES ${HEADERS} DESTINATION "include/betterchain/chain" )

add_subdirectory(test)

#add_executable( test test.cpp )
#target_link_libraries( test betterchain_chain ${CMAKE_DL_LIBS} ${PLATFORM_SPECIFIC_LIBS} ${Intl_LIBRARIES} )



add_executable(test_result_writer
  result_writer.cpp
  result_writer_main.cpp
  )
target_link_libraries(test_result_writer PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(test_result_writer PRIVATE ZLIB::ZLIB)
endif()

add_executable(test_loader
  loader_main.cpp
  )
target_link_libraries(test_loader PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(test_loader PRIVATE ZLIB::ZLIB)
endif()

add_executable(test_gzifstream
  gzifstream_main.cpp
  )
target_link_libraries(test_gzifstream PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(test_gzifstream PRIVATE ZLIB::ZLIB)
endif()

add_executable(test_gzofstream
  gzofstream_main.cpp
  )
target_link_libraries(test_gzofstream PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(test_gzofstream PRIVATE ZLIB::ZLIB)
endif()

add_executable(test_param
  param_main.cpp
  )
target_link_libraries(test_param PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(test_param PRIVATE ZLIB::ZLIB)
endif()

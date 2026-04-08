
add_executable(rclmscheduler
  scheduler.cpp
  )
target_link_libraries(rclmscheduler PRIVATE
  rcsc
  Boost::system
  )

add_executable(rclmtableprinter
  tableprinter.cpp
  )
target_link_libraries(rclmtableprinter PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(rclmtableprinter PRIVATE ZLIB::ZLIB)
endif()

add_executable(rcg2csv
  rcg2csv.cpp
  )
target_link_libraries(rcg2csv PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(rcg2csv PRIVATE ZLIB::ZLIB)
endif()

add_executable(rcg2txt
  rcg2txt.cpp
  )
target_link_libraries(rcg2txt PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(rcg2txt PRIVATE ZLIB::ZLIB)
endif()

add_executable(rcgrenameteam
  rcgrenameteam.cpp
  )
target_link_libraries(rcgrenameteam PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(rcgrenameteam PRIVATE ZLIB::ZLIB)
endif()

add_executable(rcgresultprinter
  resultprinter.cpp
  )
target_link_libraries(rcgresultprinter PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(rcgresultprinter PRIVATE ZLIB::ZLIB)
endif()

add_executable(rcgreverse
  rcgreverse.cpp
  )
target_link_libraries(rcgreverse PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(rcgreverse PRIVATE ZLIB::ZLIB)
endif()

add_executable(rcgvalidator
  rcgvalidator.cpp
  )
target_link_libraries(rcgvalidator PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(rcgvalidator PRIVATE ZLIB::ZLIB)
endif()

add_executable(rcgverconv
  rcgverconv.cpp
  )
target_link_libraries(rcgverconv PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(rcgverconv PRIVATE ZLIB::ZLIB)
endif()

add_executable(rcgversion
  rcgversion.cpp
  )
target_link_libraries(rcgversion PRIVATE
  rcsc
  Boost::system
  )
if(ZLIB_FOUND)
  target_link_libraries(rcgversion PRIVATE ZLIB::ZLIB)
endif()

include_directories(
  ${Boost_INCLUDE_DIRS}
  ${ZLIB_INCLUDE_DIRS}
  ${PROJECT_SOURCE_DIR}
  ${PROJECT_BINARY_DIR}
  )

install(TARGETS
  rclmscheduler
  rclmtableprinter
  rcg2csv
  rcg2txt
  rcgrenameteam
  rcgresultprinter
  rcgreverse
  rcgvalidator
  rcgverconv
  rcgversion
  RUNTIME
  DESTINATION ${CMAKE_INSTALL_BINDIR}
  )

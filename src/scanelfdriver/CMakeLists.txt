set(Scanelf_SRC scanelfdriver.cpp)

add_library(scanelfplugin MODULE ${Scanelf_SRC})
set_target_properties(scanelfplugin PROPERTIES VERSION ${PROJECT_VERSION})
set_target_properties(scanelfplugin PROPERTIES SOVERSION ${PROJECT_VERSION_MAJOR})

target_link_libraries(scanelfplugin driver Qt5::Core Qt5::Widgets)
target_include_directories(scanelfplugin SYSTEM PUBLIC
	$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/include/>
	$<INSTALL_INTERFACE:include/>
)

# Install the executable
install( TARGETS	scanelfplugin
	LIBRARY		DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

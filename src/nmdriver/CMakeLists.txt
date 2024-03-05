set(Nm_SRC nmdriver.cpp)

add_library(nmplugin MODULE ${Nm_SRC})
set_target_properties(nmplugin PROPERTIES VERSION ${PROJECT_VERSION})
set_target_properties(nmplugin PROPERTIES SOVERSION ${PROJECT_VERSION_MAJOR})

target_link_libraries(nmplugin driver Qt5::Core Qt5::Widgets)
target_include_directories(nmplugin SYSTEM PUBLIC
	$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/include/>
	$<INSTALL_INTERFACE:include/>
)

# Install the executable
install( TARGETS	nmplugin
	LIBRARY		DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

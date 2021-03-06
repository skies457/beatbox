find_package(Vala REQUIRED)
include(ValaVersion)
ensure_vala_version("0.16.0" MINIMUM)
include(ValaPrecompile)

add_definitions(${NORMAL_CFLAGS})
include_directories(${CMAKE_BINARY_DIR}/core ${CMAKE_BINARY_DIR}/src)
link_directories(${NORMAL_LINK_DIRS})

vala_precompile(VALA_C
		StorePlugin.vala
		Store.vala
		SearchResult.vala
		
        API/Price.vala
		API/Release.vala
		API/FormatTag.vala
		API/BasketItem.vala
		API/XMLParser.vala
		API/Label.vala
		API/Basket.vala
		API/Artist.vala
		API/Track.vala
		
		Widgets/ArtistView.vala
		Widgets/IconView.vala
		Widgets/SearchResultsPage.vala
		Widgets/TrackList.vala
		Widgets/ReleaseRotator.vala
		Widgets/TagLabel.vala
		Widgets/StoreView.vala
		Widgets/AlbumView.vala
		Widgets/ObjectList.vala
		Widgets/SearchList.vala
		Widgets/HomeView.vala
		Widgets/TagGroup.vala
		Widgets/ClickableImage.vala
		Widgets/TagView.vala
		Widgets/FancyButton.vala
    PACKAGES
        glib-2.0
        gtk+-3.0
        granite
        beatbox
        beatbox-core
        libxml-2.0
        gee-1.0
        gio-unix-2.0
        gstreamer-0.10
        libnotify
        libgpod-1.0
        gstreamer-interfaces-0.10
        gstreamer-pbutils-0.10
        gstreamer-cdda-0.10
        PeasGtk-1.0
        libpeas-1.0
        libsoup-2.4
        ${ADD_PKG}
    OPTIONS
        --target-glib=2.32
        --vapidir=${CMAKE_SOURCE_DIR}/vapi
        --vapidir=${CMAKE_BINARY_DIR}/core/
        --vapidir=${CMAKE_BINARY_DIR}/src/
    )
   
add_library(store MODULE ${VALA_C})
add_definitions(${NORMAL_CFLAGS})
link_directories(${NORMAL_LINK_DIRS})
target_link_libraries (store ${NORMAL_LIBRARIES})
install(TARGETS store DESTINATION ${PLUGIN_DIR}/Store/)
install(FILES store.plugin DESTINATION ${PLUGIN_DIR}/Store/)
add_dependencies(store beatbox)

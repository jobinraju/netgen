add_definitions(-DNGINTERFACE_EXPORTS)
add_library(occ ${NG_LIB_TYPE}
        Partition_Inter2d.cxx Partition_Inter3d.cxx 
        Partition_Loop.cxx Partition_Loop2d.cxx Partition_Loop3d.cxx Partition_Spliter.cxx 
        occconstruction.cpp occgenmesh.cpp occgeom.cpp occmeshsurf.cpp python_occ.cpp
        )
if(USE_GUI)
        add_library(occvis ${NG_LIB_TYPE} vsocc.cpp)
endif(USE_GUI)

target_link_libraries(occ PUBLIC ngcore)

if(NOT WIN32)
    target_link_libraries( occ PUBLIC ${OCC_LIBRARIES} ${PYTHON_LIBRARIES})
    install( TARGETS occ ${NG_INSTALL_DIR})
    if (USE_GUI)
        target_link_libraries( occvis PUBLIC occ )
        install( TARGETS occvis ${NG_INSTALL_DIR})
    endif(USE_GUI)
endif(NOT WIN32)

install(FILES
  occgeom.hpp occmeshsurf.hpp vsocc.hpp
  DESTINATION ${NG_INSTALL_DIR_INCLUDE}/occ COMPONENT netgen_devel
)

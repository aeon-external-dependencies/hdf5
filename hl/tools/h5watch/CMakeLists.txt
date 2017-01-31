cmake_minimum_required (VERSION 3.1.0)
PROJECT (HDF5_HL_TOOLS_H5WATCH)

#-----------------------------------------------------------------------------
# Define Sources
#-----------------------------------------------------------------------------
set (H5WATCH_SOURCES
    ${HDF5_HL_TOOLS_H5WATCH_SOURCE_DIR}/h5watch
)

#-- Add h5watch program
INCLUDE_DIRECTORIES (${HDF5_TOOLS_DIR}/lib)
INCLUDE_DIRECTORIES (${HDF5_HL_TOOLS_DIR}/src)
INCLUDE_DIRECTORIES (${HDF5_HL_TOOLS_H5WATCH_SOURCE_DIR})

add_executable (h5watch ${H5WATCH_SOURCES})
TARGET_NAMING (h5watch STATIC)
TARGET_C_PROPERTIES (h5watch STATIC " " " ")
target_link_libraries (h5watch ${HDF5_HL_LIB_TARGET} ${HDF5_LIB_TARGET} ${HDF5_TOOLS_LIB_TARGET})
set_target_properties (h5watch PROPERTIES FOLDER External/hdf5)

if (BUILD_TESTING)
  #-- Add swmr_check_compat_vfd program
  set (hl_swmr_check_compat_vfd_SOURCES
      ${HDF5_HL_TOOLS_H5WATCH_SOURCE_DIR}/swmr_check_compat_vfd.c
  )
  add_executable (hl_swmr_check_compat_vfd ${hl_swmr_check_compat_vfd_SOURCES})
  TARGET_NAMING (hl_swmr_check_compat_vfd STATIC)
  TARGET_C_PROPERTIES (hl_swmr_check_compat_vfd STATIC " " " ")
  target_link_libraries (hl_swmr_check_compat_vfd ${HDF5_HL_LIB_TARGET} ${HDF5_LIB_TARGET} ${HDF5_TOOLS_LIB_TARGET})
  set_target_properties (hl_swmr_check_compat_vfd PROPERTIES FOLDER External/hdf5)

  #-- Add extend_dset program
  set (extend_dset_SOURCES
      ${HDF5_HL_TOOLS_H5WATCH_SOURCE_DIR}/extend_dset.c
  )
  add_executable (extend_dset ${extend_dset_SOURCES})
  TARGET_NAMING (extend_dset STATIC)
  TARGET_C_PROPERTIES (extend_dset STATIC " " " ")
  target_link_libraries (extend_dset ${HDF5_HL_LIB_TARGET} ${HDF5_LIB_TARGET} ${HDF5_TOOLS_LIB_TARGET})
  set_target_properties (extend_dset PROPERTIES FOLDER External/hdf5)

  add_executable (h5watchgentest ${HDF5_HL_TOOLS_H5WATCH_SOURCE_DIR}/h5watchgentest.c)
  TARGET_NAMING (h5watchgentest STATIC)
  TARGET_C_PROPERTIES (h5watchgentest STATIC " " " ")
  target_link_libraries (h5watchgentest ${HDF5_HL_LIB_TARGET} ${HDF5_LIB_TARGET})
  set_target_properties (h5watchgentest PROPERTIES FOLDER External/hdf5)

  include (CMakeTests.cmake)
endif (BUILD_TESTING)

#-----------------------------------------------------------------------------
# Add file(s) to CMake Install
#-----------------------------------------------------------------------------
install (
    TARGETS
        h5watch
    RUNTIME DESTINATION ${HDF5_INSTALL_BIN_DIR} COMPONENT hltoolsapplications
)

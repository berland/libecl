set( CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake/Modules")
include(init_python)
init_python( 2.7 )

find_python_package(pandas 0.17 ${PYTHON_INSTALL_PREFIX})
if (NOT DEFINED PY_pandas)
   message(FATAL_ERROR "Pandas module not found Python wrappers not enabled. Install with: \"pip install pandas\"")
endif()

find_python_package(numpy 1.7.1 ${PYTHON_INSTALL_PREFIX})
if (NOT DEFINED PY_numpy)
   message(FATAL_ERROR "numpy module not found - Python wrappers not enabled. Install with: \"pip install numpy\"")
endif()

find_python_package(cwrap 1 ${PYTHON_INSTALL_PREFIX})
if (NOT DEFINED PY_cwrap)
   message(FATAL_ERROR "cwrap module not found Python wrappers not enabled. Install with: \"pip install cwrap\"")
endif()

configure_file(test_env.py.in   ${PROJECT_BINARY_DIR}/${PYTHON_INSTALL_PREFIX}/test_env.py )

add_subdirectory( ecl )

if (INSTALL_ERT_LEGACY)
   add_subdirectory( ert )
endif()

if (BUILD_TESTS)
   add_subdirectory( tests )
endif()

if(RST_DOC)
  add_subdirectory( docs )
endif()

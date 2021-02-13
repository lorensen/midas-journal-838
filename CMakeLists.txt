if(NOT VTK_SOURCE_DIR)
  cmake_minimum_required(VERSION 3.3 FATAL_ERROR)
  project(PoissonReconstruction)
  find_package(VTK REQUIRED)
endif()
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${VTK_CMAKE_DIR}")
if(NOT VTK_SOURCE_DIR)
  include(vtkExternalModuleMacros)
endif()

message(STATUS "SplineDrivenImageSlicer: Building as a Remote VTK module")

set(Module_SRCS
  vtkFrenetSerretFrame.cxx
  vtkSplineDrivenImageSlicer.cxx  
)

if (VTK_VERSION VERSION_LESS "8.90.0")
  vtk_module_library(SplineDrivenImageSlicer ${Module_SRCS})
else()
  vtk_module_add_module(VTK::SplineDrivenImageSlicer
    SOURCES ${Module_SRCS}
    )
endif()

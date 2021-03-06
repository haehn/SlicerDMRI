
#-----------------------------------------------------------------------------
set(CLP ${MODULE_NAME})
set(DATADIR ${CMAKE_CURRENT_SOURCE_DIR}/../../DWIToDTIEstimation/Data/Baseline)
#-----------------------------------------------------------------------------
add_executable(${CLP}Test ${CLP}Test.cxx)
add_dependencies(${CLP}Test ${CLP})
target_link_libraries(${CLP}Test ${CLP}Lib ${SlicerExecutionModel_EXTRA_EXECUTABLE_TARGET_LIBRARIES})

set_target_properties(${CLP}Test PROPERTIES LABELS ${CLP})
set_target_properties(${CLP}Test PROPERTIES FOLDER ${${CLP}_TARGETS_FOLDER})

set(testname ${CLP}Test)
add_test(NAME ${testname} COMMAND ${SEM_LAUNCH_COMMAND} $<TARGET_FILE:${CLP}Test>
  ${CLP}Test
  --seedspacing 4
  --clthreshold 0.3
  --minimumlength 10
  --maximumlength 800
  --thresholdmode FractionalAnisotropy
  --stoppingvalue 0.1
  --stoppingcurvature 0.8
  --integrationsteplength 0.5
  --label 1
  ${DATADIR}/helix-DTI.nhdr
  ${TEMP}/${CLP}Test_helixTracts.vtp
  )
set_property(TEST ${testname} PROPERTY LABELS ${CLP})

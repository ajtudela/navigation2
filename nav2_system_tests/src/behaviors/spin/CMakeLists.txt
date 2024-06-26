set(test_spin_behavior_exec test_spin_behavior_node)

ament_add_gtest_executable(${test_spin_behavior_exec}
  test_spin_behavior_node.cpp
  spin_behavior_tester.cpp
)

ament_target_dependencies(${test_spin_behavior_exec}
  ${dependencies}
)

ament_add_test(test_spin_behavior
  GENERATE_RESULT_FOR_RETURN_CODE_ZERO
  COMMAND "${CMAKE_CURRENT_SOURCE_DIR}/test_spin_behavior_launch.py"
  WORKING_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}"
  TIMEOUT 180
  ENV
    TEST_EXECUTABLE=$<TARGET_FILE:${test_spin_behavior_exec}>
    BT_NAVIGATOR_XML=navigate_to_pose_w_replanning_and_recovery.xml
)

ament_add_test(test_spin_behavior_fake
  GENERATE_RESULT_FOR_RETURN_CODE_ZERO
  COMMAND "${CMAKE_CURRENT_SOURCE_DIR}/test_spin_behavior_fake_launch.py"
  WORKING_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}"
  TIMEOUT 180
  ENV
    TEST_EXECUTABLE=$<TARGET_FILE:${test_spin_behavior_exec}>
    MAKE_FAKE_COSTMAP=true
)

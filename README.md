robot_capsule_urdf
==================

Generation of capsule collision models urdf files.


Quickstart
----------
 1.  Clone repository recursively:
    `git clone --recurse-submodules https://github.com/max-assel/robot_capsule_urdf.git`

 1.  Compile `robot_capsule_urdf` by usual ros commands.

 1.  Given a robot description package in the form
     `robot_name_description`, and given a capsule parameters file in
     robot_name_description/etc/robot_name_capasule_param you can run
     the following command to generate a new urdf file for your robot:

     ```sh
     rosrun robot_capsule_urdf robot_capsule_urdf robot_name > robot_name_capsule.urdf
     ```

 1. If you want to generate automatically the capsule urdf when
    building robot_name_descrition, you can include the following in
    `CmakeLists.txt`:

    ```sh
    rosbuild_find_ros_package(robot_capsule_urdf)
    set(_robot_capsule_urdf ${robot_capsule_urdf_PACKAGE_PATH}/bin/robot_capsule_urdf)

    macro(generate_capsule_urdf robot_name)
      execute_process(
      COMMAND ${_robot_capsule_urdf} ${robot_name}
      OUTPUT_VARIABLE _capsule_output)
      file(WRITE ${CMAKE_SOURCE_DIR}/urdf/${robot_name}_capsule.urdf ${_capsule_output})
    endmacro()

    generate_capsule_urdf(robot_name)
    ```

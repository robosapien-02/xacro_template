<!--===============================================================================
                           XACRO URDF MACRO LIBRARY
        Author: ROBOSAPIEN (AAYUSH KHANDELWAL)   |    Version: 1.0

      PURPOSE:
      --------
      This file provides reusable, parameterized Xacro macros for generating
      URDF links and joints. You can quickly build consistent, error-free
      URDF robot models by reusing these templates and customizing only what
      you need for each link or joint.

      COMPONENTS:
      -----------
      1. Materials
         - Common colors/materials for visuals.
      2. joint_template
         - Macro for defining URDF joints (all types, incl. limits, dynamics,
           safety, mimic, calibration).
      3. link_template
         - Macro for defining URDF links (geometry, inertial, visuals,
           collisions, optional sensors, mesh support).

      HOW TO USE:
      -----------
      1. In your main .urdf.xacro file, first load this file:
         <xacro:include filename="your_macro_library.xacro" />

      2. Create links using the macro, overriding defaults as needed:
         <xacro:link_template
             link_name="base_link"
             mass="2.5"
             visual_geometry_type="box"
             visual_geometry_size="1 1 0.5"
             visual_material="gray"
         />

      3. Create joints between links:
         <xacro:joint_template
             joint_name="shoulder"
             joint_type="revolute"
             parent_link="base_link"
             child_link="shoulder_link"
             origin_xyz="0 0 0.5"
             axis_xyz="0 0 1"
             lower_limit="-1.57"
             upper_limit="1.57"
             effort="10"
             velocity="2"
         />

      4. (Optional) Customize other parameters as needed for each macro call.
         All macro parameters have sensible defaults; override only what you need.

      EXAMPLE ROBOT SKELETON:
      -----------------------
      <robot xmlns:xacro="http://www.ros.org/wiki/xacro" name="my_robot">
        <xacro:include filename="your_macro_library.xacro"/>
        <!-- Define links -->
        <xacro:link_template link_name="base_link"/>
        <xacro:link_template link_name="shoulder_link" visual_geometry_type="cylinder" visual_geometry_size="0.1 0.3"/>
        <!-- Define joints -->
        <xacro:joint_template joint_name="shoulder" joint_type="revolute" parent_link="base_link" child_link="shoulder_link" axis_xyz="0 0 1"/>
      </robot>

      NOTES:
      ------
      - All macro parameters can be overridden in each use.
      - Defaults are just for convenience—**always provide correct mass/inertia/limits for real robots!**
      - For mesh geometry, set type to 'mesh' and provide filename (e.g., package://my_robot/meshes/part.stl).
      - Sensors are optional and can be added to links.
      - Sensor tags are for SDF/Gazebo; standard URDF will ignore them.

===============================================================================-->

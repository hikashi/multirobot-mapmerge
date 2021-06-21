 ``` xml
 <!-- Map megring (know inital position case)-->
  <group ns="/$(arg first_tb3)/map_merge">
    <param name="init_pose_x" value="$(arg first_tb3_x_pos)"/>
    <param name="init_pose_y" value="$(arg first_tb3_y_pos)"/>
    <param name="init_pose_z" value="$(arg first_tb3_z_pos)"/>
    <param name="init_pose_yaw" value="$(arg first_tb3_yaw)"/>
  </group>
  <group ns="/$(arg second_tb3)/map_merge">
    <param name="init_pose_x" value="$(arg second_tb3_x_pos)"/>
    <param name="init_pose_y" value="$(arg second_tb3_y_pos)"/>
    <param name="init_pose_z" value="$(arg second_tb3_z_pos)"/>
    <param name="init_pose_yaw" value="$(arg second_tb3_yaw)"/>
  </group>
  <group ns="/$(arg third_tb3)/map_merge">
    <param name="init_pose_x" value="$(arg third_tb3_x_pos)"/>
    <param name="init_pose_y" value="$(arg third_tb3_y_pos)"/>
    <param name="init_pose_z" value="$(arg third_tb3_z_pos)"/>
    <param name="init_pose_yaw" value="$(arg third_tb3_yaw)"/>
  </group>

  <!-- perform static transform publisher for three robots -->
  <node pkg="tf" type="static_transform_publisher" name="world_to_$(arg first_tb3)_tf_broadcaster"  args="0 0 0 0 0 0 /map /$(arg first_tb3)/map 100"/>
  <node pkg="tf" type="static_transform_publisher" name="world_to_$(arg second_tb3)_tf_broadcaster" args="0 0 0 0 0 0 /map /$(arg second_tb3)/map 100"/>
  <node pkg="tf" type="static_transform_publisher" name="world_to_$(arg third_tb3)_tf_broadcaster"  args="0 0 0 0 0 0 /map /$(arg third_tb3)/map 100"/>

    <!-- Launch the map_merge node along with transform publishers -->
    <node pkg="multirobot_map_merge" type="map_merge" respawn="false" name="map_merge" output="screen">
      <param name="robot_map_topic" value="map"/>
      <param name="robot_namespace" value="tb3"/>
      <param name="merged_map_topic" value="map"/>
      <param name="world_frame" value="map"/>
      <param name="known_init_poses" value="true"/>
      <param name="merging_rate" value="4.0"/>
      <param name="discovery_rate" value="0.1"/>
      <param name="estimation_rate" value="0.2"/>
      <!-- <param name="merging_rate" value="4.0"/> -->
      <!-- <param name="discovery_rate" value="0.05"/>
      <param name="estimation_rate" value="0.1"/> -->
      <param name="estimation_confidence" value="1.0"/>
  </node>
```

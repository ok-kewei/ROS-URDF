# ROS-URDF
Robot Creation: URDF for Robot Modeling course from Robot Ignite Academy

The course covers:- 
- How to build a visual robot model with URDF
- How to add physical properties to a URDF Model (Collision, Frictions…)
- How to use XACRO to clean up URDF files.
- How to use URDF in Gazebo-ROS ecosystem.


**My Key Take Aways:-**

- to check the model in the world : rosservice call /gazebo/get_world_properties "\{\}"
- to delete the model (eg: Mira) in the world : rosservice call /gazebo/delete_model "model_name: 'mira'"

- Unit 2: Adapt URDF for Gazebo Simulator

To make a model appear in Gazebo you need to add the following:

    Inertias: The inertias and mass of the model is important if you want it to have physics applied
    Gazebo Physical Properties: Here you specify the frictions and material properties like colour or softness.
    Collisions: Without collisions the Robot models would just go through the floor.
    Visual Properties: We add colour to the visual, which only will affect the URDF in RVIZ, the colour in the simulation is defined in the Gazebo Physical Properties.
    Gazebo Sensors: Here is when you add cameras, motor controllers and all the robots systems.

- Inertia : rosrun my_mira_description inertia_calculator.py to return the inertia by providing the mass and the dimension of the object and include the inertia in the urdf file. 


- Gazebo Physical Properties:
The "gazebo" tag that refers to the link that is setting the physical properties for.

Here the main physical properties of the link are defined:

    mu1: The static friction coefficient. In simple terms, it would be how much friction there is until the object starts moving.
    mu2: The dynamic friction coefficient. In simple terms, it would be how much friction there is when the object is moving.

Here we have the same issue. These values should be calculated through friction tests with elements with the same mass as the links you are setting these values to. You should also bear in mind the materials they are made of, and so on. But in reality, it's setting them with the values that makes the robot behave correctly, not necessarily the real ones.

    kp: This coefficient sets the static contact stiffness. This determines if the link material is closer to marble (very rigid, bigger values) or more like rubber (soft material, lower values).
    kd: This coefficient sets the dynamic contact stiffness. This determines if the link material is closer to marble (very rigid, bigger values) or more like rubber (soft material, lower values). It's essentially how much it deforms over a long period of time, exerting its pressure.

And then we have the material, that is not more than the colour of the geometric visual shape. If its a dae, then it serves no purpose because the colours are enmbeded in the 3Dfile.

Add the following tag in URDF file.  
\<gazebo reference="base_link"\>  
   \<kp\>100000.0\</kp\>  
    \<kd\>100000.0\</kd\>  
    \<mu1\>10.0\</mu1\>  
    \<mu2\>10.0\</mu2\>  
    \<material\>Gazebo\/Grey\</material\>  
\</gazebo\>


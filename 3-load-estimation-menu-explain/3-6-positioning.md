# 3.6 Posture Setting

Specify the starting posture for the estimation motion.
The user must manually move the robot axes to a position where no interference occurs between the robot, tool, or surrounding environment, and then press "**Set pose**(Set Main-Axis Position)" to register the starting posture.

There is no restriction for the S-axis; however, the H and V axes must be set so that the V-axis frame angle remains within ±60° relative to the ground reference. For optimal estimation accuracy, it is recommended to set the V-axis angle as close to 0° as possible.

If the user attempts to press "Set Position" while the V-axis angle exceeds ±60°, a message will appear stating:
"The V-axis angle must be within ±60° relative to the ground."

1.  **Current Axis Angles**

    Displays the current angles of the main robot axes (S, H, V).

2.  **Starting Position**

    Displays the registered S, H, and V axis angles used as the starting posture for load estimation. Once the **Play check** or **Play normal** button is executed, the robot posture will move to the specified position.

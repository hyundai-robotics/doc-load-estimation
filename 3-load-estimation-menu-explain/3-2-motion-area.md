# 3.2 Operating Range

This screen displays the motion range of each axis used for load estimation.
“Axis Angle” shows the current value of each robot axis, and “Start Position” indicates the initial position where load estimation begins.
The “Min” and “Max” values in the “Motion Range” represent the minimum and maximum axis limits used during the estimation motion.
For the B axis and R1 axis, the minimum and maximum motion ranges can be configured.

The default motion range settings are as follows:

\[**Default Motion Range**]

&#x20;  B Axis Motion Range (min): (60° − H-axis angle − V-axis angle)

&#x20;  B Axis Motion Range (max): (120° − H-axis angle − V-axis angle)

&#x20;  R1 Axis Motion Range (min): 0°

&#x20;  R1 Axis Motion Range (max): 90°

Depending on the configured wrist-axis motion range, certain payload properties may not be measurable. In such cases, the user must manually input the payload data.

![Fig 5. Warning Message When Center of Gravity (Cx, Cy) and Inertia Cannot Be Estimated](<../_assets/image_3.png>)

The required motion range conditions for the B axis and R1 axis to estimate all payload properties are as follows:

\[**Motion Range Conditions for Full Payload Estimation**]

&#x20;  \- B-Axis Motion Range: Must be within (40° − H − V) to (140° − H − V)

&#x20;  \- Minimum Motion Angle of B-Axis: 20° or greater

&#x20;  \- Minimum Motion Angle of R1-Axis: 60° or greater

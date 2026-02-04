
[__SOURCE](README.md)
# ${cont_model} Controller Function Manual - Load Estimation

[__SOURCE](1-load-estimation-intro/README.md)
# 1. Overview
[__SOURCE](1-load-estimation-intro/1-definition.md)
# 1.1 What Is Load Estimation


The load estimation function calculates the wegiht and center of gravity position of the payload mounted on the robot's end effector.
To control the robot based on a dynamic model, both the dynamic parameters of the robot itself and those of the payload are required. Since the payload attached to the robot can vary depending on the application, and calculating the tool data may be difficult in some cases, the values estimated by the load estimation function can be used as substitutes.

![Fig 1. Tool Coordinate System](../_assets/image.png)


[__SOURCE](1-load-estimation-intro/2-info.md)
# 1.2 Precautions and Instructions


- The payload estimated during load estimation is based on the tool coordinate system.

- The load estimation function is intended to support stable and optimal robot operation. It is not suitable for precise measurement of payload weight or other physical values.

- The load estimation function can only be used when the robot is installed on the floor. Robots installed on a wall or ceiling do not support this function.

- The smaller the physical properties of the tool (weight, center of gravity, and inertia), the greater the estimation error may be. If the tool has very small physical values, it is recommended that the user manually inputs the tool data.

- If the robot uses multiple conditions such as the tool alone or the tool combined with a workpiece, separate tool data must be registered for each case. Perform load estimation for each condition: (Tool only) and (Tool + Workpiece).

{% hint style="info" %}
Robots with a payload capacity of less than 50 kg do not support the load estimation function.
{% endhint %}

- For the most accurate results, it is recommended to perform load estimation after sufficient warm-up and after turning off the controller for at least one hour. As the motor temperature increases, the estimation accuracy may decrease.

{% hint style="info" %}
The recommended temperature range is 35-40°C. Encoder temperature can be checked through the system characteristic data or the load estimation log file.
{% endhint %}

- If accurate tool data such as design values or measured values (e.g., weight, center of gravity) are available, manually entering the values into the tool data settings provides higher accuracy. (Executing "Apply CAD Data" is required.)

![Fig 1.2 Apply CAD Data](../_assets/image_12_eng.png)

- Values tuned on one robot model do not necessarily guarantee the same estimation performance on other units of the same model. Mechanical and operating characteristics vary by robot, including mechanical tolerances, motor performance deviation, lubrication conditions, and temperature environment.

[__SOURCE](1-load-estimation-intro/3-procedure.md)
# 1.3 Simple Operating Procedure


![Fig 2. Simple Procedure](../_assets/image_4_eng.png)


[__SOURCE](2-load-estimation-result/README.md)
# 2. Load Estimation Details


[__SOURCE](2-load-estimation-result/2-1-weight.md)
# 2.1 Weight

This value represents the total weight of the payload mounted on the robot's end effector. The unit is kilograms (kg).

[__SOURCE](2-load-estimation-result/2-2-weight-center-of-gravity.md)
# 2.2 Center of Gravity

The center of gravity is defined as the distance from the robot's end effector to the payload's center of gravity in the X, Y, and Z directions. The unit used is millimeters (mm).

[__SOURCE](2-load-estimation-result/2-3-inertia.md)
# 2.3 Inertia

This value represents the payload's moment of inertia. It refers to the sum of each distributed weight multiplied by the square of its distance from the rotational axis, assuming rotation around the X, Y, and Z axes. The moment of inertia is determined by how the weight is distributed around each axis - greater values occur when more of the payload's weight is located farther from the rotation axis. The unit used is kg·m² for the X, Y, and Z axes.

![Fig 3. Inertia Calculation](<../_assets/image_10_eng.png>)


[__SOURCE](3-load-estimation-menu-explain/README.md)
# 3. Load Estimation Menu Description

Execute the load estimation from 『**system**』 → 『**6.Auto calibration**』 → 『**4:Load estimation function**』.

{% hint style="info" %}

When selecting the 『**4:Load estimation function**』 menu, if the current control mode is set to "Vibration Suppression Control," the motor will automatically turn Off to switch the mode to "PPI."
After load estimation is completed, the mode will automatically return to "Vibration Suppression Control," and the motor will again turn Off.

{% endhint %}

![Fig 4. Load Estimation Screen](<../_assets/image_2_eng.png>)



[__SOURCE](3-load-estimation-menu-explain/3-1-tool-number.md)
# 3.1 Tool Number

Assign the tool number that represents the tool to be used.
When the assigned tool number is applied to the teaching program, the robot will operate based on the estimated payload properties.
Only registered tool data can be used as a tool number.

[__SOURCE](3-load-estimation-menu-explain/3-2-motion-area.md)
# 3.2 Operating Range

This screen displays the motion range of each axis used for load estimation.
"Axis Angle" shows the current value of each robot axis, and "Start Position" indicates the initial position where load estimation begins.
The "Min" and "Max" values in the "Motion Range" represent the minimum and maximum axis limits used during the estimation motion.
For the B axis and R1 axis, the minimum and maximum motion ranges can be configured.

The default motion range settings are as follows:

\`Default Motion Range`

  - B Axis Motion Range (min): (60° - H-axis angle - V-axis angle)

  - B Axis Motion Range (max): (120° - H-axis angle - V-axis angle)

  - R1 Axis Motion Range (min): 0°

  - R1 Axis Motion Range (max): 90°

Depending on the configured wrist-axis motion range, certain payload properties may not be measurable. In such cases, the user must manually input the payload data.

![Fig 5. Warning Message When Center of Gravity (Cx, Cy) and Inertia Cannot Be Estimated](<../_assets/image_3_eng.png>)

The required motion range conditions for the B axis and R1 axis to estimate all payload properties are as follows:

\`Motion Range Conditions for Full Payload Estimation`

 - B-Axis Motion Range: Must be within (40° - H - V) to (140° - H - V)

 - Minimum Motion Angle of B-Axis: 20° or greater

 - Minimum Motion Angle of R1-Axis: 60° or greater

[__SOURCE](3-load-estimation-menu-explain/3-3-check-operation.md)
# 3.3 Test Operation

This function is used to check for possible interference. Load estimation is not performed when executing the "**Play check**" function.

Since load estimation operates the robot in a predefined motion pattern to obtain payload data, attention must be given to interference with surrounding equipment or the robot itself during motion. Therefore, before running "**Play normal**", the user must perform "**Play check**" to verify that no collision risk exists. If interference occurs, press the Emergency Stop button or switch the Enable Switch to Off to stop the robot.

If the robot stops before the check operation is completed, the load estimation menu must be executed again.

[**Operating condition**]

  - Robot controller : manual mode

  - Enable Switch : On

[__SOURCE](3-load-estimation-menu-explain/3-4-normal-operation.md)
# 3.4 Normal Operation

This menu executes the load estimation. Since the operation runs at high speed, it must only be executed after verifying interference safety using "**Play check**".

[**Operating condition**]

  - Robot controller : manual mode

  - Enable Switch : On
[__SOURCE](3-load-estimation-menu-explain/3-5-additional-mass-by-axis.md)
# 3.5 Additional Weights by Axis


Navigate to the Additional weights per Axis menu.
To perform accurate load estimation, the additional weight information for Axis 3 (weight, X-axis center of gravity, and Z-axis center of gravity) must be entered.
The additional weights include items such as mounting plates, signal boxes, and cables attached to the frame.

The coordinate system used for entering the additional weights of Axis 3 is shown below.

![Fig 6. Axis-3 Additional Weight Components and Coordinate System](<../_assets/image_9_eng.png>)
[__SOURCE](3-load-estimation-menu-explain/3-6-positioning.md)
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

[__SOURCE](4-load-estimation-motion-area/README.md)
# 4. Load Estimation Operating Range

The motion pattern used for load estimation varies depending on the robot type, such as 6-axis robots (HX165, HS165, HS200, HA006, HA020, etc.), 4-axis palletizing robots (HP160), and painting robots (YP020). The corresponding motion ranges are as follows.
[__SOURCE](4-load-estimation-motion-area/4-1-6-axis-robot.md)
# 4.1 6-Axis Robot

![Fig 7.  Load Estimation Operating Range (6-axis robot)](<../_assets/image_5_eng.png>)

[__SOURCE](4-load-estimation-motion-area/4-2-4-axis-palletize-robot.md)
# 4.2 4-Axis Palletizing Robot

![Fig 8. Load Estimation Operating Range (4-Axis Palletizing Robot)](<../_assets/image_8_eng.png>)

[__SOURCE](4-load-estimation-motion-area/4-3-paint-robot.md)
# 4.3 Painting Robot

![Fig 9. Load Estimation Operating Range (Painting Robot)](<../_assets/image_11_eng.png>)

[__SOURCE](5-load-estimation-result-application-method/README.md)
# 5. How to Apply Load Estimation Results


[__SOURCE](5-load-estimation-result-application-method/5-1-application.md)
# 5.1 Applying Load Estimation Results

After reviewing the load estimation results, press "OK." When the confirmation message "Apply the estimated values?" appears, selecting "Yes" will save the estimated payload data to the assigned tool number. If "No" is selected, the data will not be saved.

![Fig 10. Load Estimation Result Screen](<../_assets/image_1_eng.png>)

<br>

![Fig 11. Confirmation Window for Applying Estimated Results](<../_assets/image_6_eng.png>)

The saved tool data will be applied during robot operation when the corresponding tool number is selected in the teaching program. Therefore, when the tool is changed or when the tool handles a workpiece, the tool data representing that condition must be selected and used in the teaching program.





[__SOURCE](5-load-estimation-result-application-method/5-2-check-modify.md)
# 5.2 Checking and Adjusting Results

The estimated payload data can be checked and modified from:
"Settings" → "3. Robot Parameters" → "1. Tool Data."
The estimation results will appear under the tool number that was used during the load estimation process.

![Fig 12. Tool Data Screen](<../_assets/image_7_eng.png>)

{% hint style="info" %}
The estimated inertia values are expressed with respect to the payload's center of gravity.
If the inertia value in a specific direction is very small, the result may be displayed as 0.
{% endhint %}






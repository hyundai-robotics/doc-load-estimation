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
The recommended temperature range is 35–40°C. Encoder temperature can be checked through the system characteristic data or the load estimation log file.
{% endhint %}

- If accurate tool data such as design values or measured values (e.g., weight, center of gravity) are available, manually entering the values into the tool data settings provides higher accuracy. (Executing “Apply CAD Data” is required.)

![Fig 1.2 Apply CAD Data](../_assets/image_12_eng.png)

- Values tuned on one robot model do not necessarily guarantee the same estimation performance on other units of the same model. Mechanical and operating characteristics vary by robot, including mechanical tolerances, motor performance deviation, lubrication conditions, and temperature environment.

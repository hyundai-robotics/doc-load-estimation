
[__SOURCE](1-load-estimation-intro/README.md)
# 1. 概述
[__SOURCE](1-load-estimation-intro/1-definition.md)
# 1.1 什么是负载估计

负载估计功能计算安装在机器人末端执行器上的有效载荷的重量和重心位置。为了基于动态模型控制机器人，既需要机器人的动态参数，也需要有效载荷的动态参数。由于附着在机器人上的有效载荷可能因应用而异，并且在某些情况下计算工具数据可能较为困难，因此负载估计功能估算的值可以作为替代。

![Fig 1. Tool Coordinate System](../_assets/image.png)
[__SOURCE](1-load-estimation-intro/2-info.md)
# 1.2 注意事项和说明

- 负载估计是在工具坐标系统基础上进行的。

- 负载估计功能旨在支持稳定和最佳的机器人操作。它不适用于精确测量负载重量或其他物理值。

- 负载估计功能仅在机器人安装在地面上时可用。安装在墙壁或天花板上的机器人不支持此功能。

- 工具的物理属性（重量、重心和惯性）越小，估计误差可能越大。如果工具的物理值非常小，建议用户手动输入工具数据。

- 如果机器人使用多个条件，例如单独工具或工具与工件结合，必须为每种情况注册单独的工具数据。分别对每种条件执行负载估计：（仅工具）和（工具 + 工件）。

{% hint style="info" %}
负载能力小于50公斤的机器人不支持负载估计功能。
{% endhint %}

- 为获得最准确的结果，建议在充分预热并在关闭控制器至少一小时后进行负载估计。随着电机温度的增加，估计精度可能会降低。

{% hint style="info" %}
推荐的温度范围是35-40°C。编码器温度可以通过系统特性数据或负载估计日志文件检查。
{% endhint %}

- 如果有准确的工具数据，如设计值或测量值（例如，重量、重心），手动将这些值输入工具数据设置可以提供更高的准确性。（需要执行“应用CAD数据”）。

![图 1.2 应用CAD数据](../_assets/image_12_eng.png)

- 在一种机器人模型上调校的值不一定能保证在同一型号的其他设备上获得相同的估计性能。机械和操作特性因机器人而异，包括机械公差、电机性能偏差、润滑条件和温度环境。
[__SOURCE](1-load-estimation-intro/3-procedure.md)
# 1.3 简单操作程序


![Fig 2. Simple Procedure](../_assets/image_4_eng.png)
[__SOURCE](2-load-estimation-result/README.md)
# 2. 负载估算详细信息
[__SOURCE](2-load-estimation-result/2-1-weight.md)
# 2.1 重量

这个值表示安装在机器人末端执行器上的有效载荷的总重量。单位为千克（kg）。
[__SOURCE](2-load-estimation-result/2-2-weight-center-of-gravity.md)
# 2.2 重心

重心定义为机器人末端执行器到有效载荷重心在X、Y和Z方向上的距离。使用的单位是毫米（mm）。
[__SOURCE](2-load-estimation-result/2-3-inertia.md)
# 2.3 惯性

该值表示载荷的惯性矩。它指的是每个分布重量乘以其与旋转轴距离的平方的总和，假设围绕 X、Y 和 Z 轴旋转。惯性矩由重量在每个轴周围的分布方式决定——当载荷的更多重量位于离旋转轴更远的位置时，惯性矩的值更大。使用的单位为 kg·m²，对于 X、Y 和 Z 轴。

![图 3. 惯性计算](<../_assets/image_10_eng.png>)
[__SOURCE](3-load-estimation-menu-explain/README.md)
# 3. 载荷估计菜单描述

从 `[system] - 6.自动 校准 - 4:载荷估计功能 ([system] - 6.Auto calibration - 4:Load estimation function)` 执行载荷估计。

{% hint style="info" %}

当选择 `4:载荷估计功能 (4:Load estimation function)` 菜单时，如果当前控制模式设置为“振动抑制控制”，电机将自动关闭以切换模式为“PPI”。
载荷估计完成后，模式将自动返回“振动抑制控制”，电机将再次关闭。

{% endhint %}

![Fig 4. Load Estimation Screen](<../_assets/image_2_eng.png>)
[__SOURCE](3-load-estimation-menu-explain/3-1-tool-number.md)
# 3.1 工具编号

分配表示要使用的工具的工具编号。
当指定的工具编号应用于教学程序时，机器人将根据估计的负载属性进行操作。
只有注册的工具数据才能用作工具编号。
[__SOURCE](3-load-estimation-menu-explain/3-2-motion-area.md)
# 3.2 工作范围

此屏幕显示用于负载估算的每个轴的运动范围。
"轴角" 显示每个机器人轴的当前值，"起始位置" 指示负载估算开始的初始位置。
“运动范围”中的“最小”和“最大”值表示估算运动期间使用的最小和最大轴限制。
对于B轴和R1轴，最小和最大运动范围可以配置。

默认的运动范围设置如下：

`Default Motion Range`

  - B轴运动范围（最小）：（60° - H轴角 - V轴角）

  - B轴运动范围（最大）：（120° - H轴角 - V轴角）

  - R1轴运动范围（最小）：0°

  - R1轴运动范围（最大）：90°

根据配置的腕轴运动范围，某些有效载荷属性可能无法测量。在这种情况下，用户必须手动输入有效载荷数据。

![图5. 中心点 (Cx, Cy) 和惯性无法估算时的警告信息](<../_assets/image_3_eng.png>)

B轴和R1轴估算所有有效载荷属性所需的运动范围条件如下：

`Motion Range Conditions for Full Payload Estimation`

 - B轴运动范围：必须在（40° - H - V）到（140° - H - V）之间

 - B轴的最小运动角度：20°或更大

 - R1轴的最小运动角度：60°或更大
[__SOURCE](3-load-estimation-menu-explain/3-3-check-operation.md)
# 3.3 测试操作

此功能用于检查可能的干扰。在执行“**播放检查**”功能时，不执行负载估算。

由于负载估算以预定义的运动模式操作机器人以获得载荷数据，因此在运动过程中特别注意与周围设备或机器人自身的干扰。因此，在运行`正常播放 (Play normal)`之前，用户必须先执行`播放检查 (Play check)`以验证没有碰撞风险。如果发生干扰，请按下紧急停止按钮或将使能开关切换为关闭以停止机器人。

如果在检查操作完成之前机器人停止，则必须重新执行负载估算菜单。

`[操作条件]`

  - 机器人控制器：手动模式

  - 使能开关：开
[__SOURCE](3-load-estimation-menu-explain/3-4-normal-operation.md)
# 3.4 正常操作

此菜单执行负载估计。由于操作在高速运行，因此必须在使用 "**Play check**" 验证干扰安全后才可以执行。

`[操作条件]`

  - 机器人控制器 : 手动模式

  - 启用开关 : 开
[__SOURCE](3-load-estimation-menu-explain/3-5-additional-mass-by-axis.md)
# 3.5 额外重量按轴


导航到每轴的额外重量菜单。
为了进行准确的负载估计，必须输入轴 3 的额外重量信息（重量、X轴重心和Z轴重心）。
额外重量包括安装板、信号框和连接到框架的电缆等项目。

用于输入轴 3 额外重量的坐标系统如下所示。

![Fig 6. Axis-3 Additional Weight Components and Coordinate System](<../_assets/image_9_eng.png>)
[__SOURCE](3-load-estimation-menu-explain/3-6-positioning.md)
# 3.6 姿态设置

指定估计运动的起始姿态。用户必须手动移动机器人轴到一个与机器人、工具或周围环境没有干扰的位置，然后按下“**设置姿态**（设置主轴位置）”以注册起始姿态。

S轴没有限制；然而，H轴和V轴必须设置，以确保V轴框架角度相对于地面基准保持在±60°以内。为了获得最佳的估计精度，建议将V轴角度尽可能接近0°。

如果用户在V轴角度超过±60°时尝试按“设置位置”，将出现一条信息，说明：
“V轴角度必须在相对于地面±60°之间。”

1.  **当前轴角度**

    显示主机器人轴（S、H、V）的当前角度。

2.  **起始位置**

    显示注册的用于负载估计的S、H和V轴角度，作为起始姿态。一旦执行“**播放检查**”或“**播放正常**”按钮，机器人姿态将移动到指定位置。
[__SOURCE](4-load-estimation-motion-area/README.md)
# 4. 负载估算操作范围

用于负载估算的运动模式因机器人类型而异，例如 6 轴机器人（HX165、HS165、HS200、HA006、HA020 等）、4 轴码垛机器人（HP160）和喷涂机器人（YP020）。相应的运动范围如下。
[__SOURCE](4-load-estimation-motion-area/4-1-6-axis-robot.md)
# 4.1 6轴机器人

![Fig 7.  载荷估计操作范围 (6轴机器人)](<../_assets/image_5_eng.png>)
[__SOURCE](4-load-estimation-motion-area/4-2-4-axis-palletize-robot.md)
# 4.2 4轴码垛机器人

![图8. 负载估计操作范围 (4轴码垛机器人)](<../_assets/image_8_eng.png>)
[__SOURCE](4-load-estimation-motion-area/4-3-paint-robot.md)
# 4.3 绘画机器人

![Fig 9. Load Estimation Operating Range (Painting Robot)](<../_assets/image_11_eng.png>)
[__SOURCE](5-load-estimation-result-application-method/README.md)
# 5. 如何应用负载估计结果
[__SOURCE](5-load-estimation-result-application-method/5-1-application.md)
# 5.1 应用负载估算结果

在审查负载估算结果后，按 "OK"。当确认消息 "应用估算值吗？" 出现时，选择 "是" 将把估算的有效载荷数据保存到分配的工具编号。如果选择 "否"，则数据将不会被保存。

![Fig 10. 负载估算结果屏幕](<../_assets/image_1_eng.png>)

<br>

![Fig 11. 应用估算结果的确认窗口](<../_assets/image_6_eng.png>)

在机器人操作期间，当在教学程序中选择相应的工具编号时，保存的工具数据将被应用。因此，当更换工具或工具处理工件时，必须在教学程序中选择和使用表示该条件的工具数据。
[__SOURCE](5-load-estimation-result-application-method/5-2-check-modify.md)
# 5.2 检查和调整结果

估计的载荷数据可以从以下位置检查和修改：
"Settings" → "3. Robot Parameters" → "1. Tool Data."
估计结果将显示在载荷估计过程中使用的工具编号下。

![Fig 12. Tool Data Screen](<../_assets/image_7_eng.png>)

{% hint style="info" %}
估计的惯性值是相对于载荷的重心表示的。
如果某个方向上的惯性值非常小，结果可能显示为0。
{% endhint %}

[__SOURCE](README.md)
# ${cont_model} 控制器功能手册 - 负载估计
[__SOURCE](0-about-this-manual/README.md)
# 关于手册
[__SOURCE](0-about-this-manual/precautions.md)
# 注意事项

{% include file="zh/precautions.md" %}
[__SOURCE](0-about-this-manual/safety-notice.md)
# 安全警告

{% include file="zh/safety-notice.md" %}
[__SOURCE](1-load-estimation-intro/README.md)
# 1. 概述
[__SOURCE](1-load-estimation-intro/1-definition.md)
# 1.1 负载估计是什么


负载估计功能计算安装在机器人末端执行器上的有效载荷的重量和重心位置。
为了基于动态模型控制机器人，需要机器人本身的动态参数以及有效载荷的动态参数。由于附加在机器人的有效载荷可以根据应用而有所不同，并且在某些情况下计算工具数据可能很困难，因此通过负载估计功能估计的值可以作为替代使用。

![Fig 1. Tool Coordinate System](../_assets/image.png)
[__SOURCE](1-load-estimation-intro/2-info.md)
# 1.2 注意事项和指示


- 装载估计期间估计的有效载荷基于工具坐标系统。

- 装载估计功能旨在支持稳定和最佳的机器人运行。 不适合精确测量有效载荷重量或其他物理值。

- 仅在机器人安装在地面上时，才能使用装载估计功能。 安装在墙壁或天花板上的机器人不支持该功能。

- 工具的物理特性(重量、重心和惯性)越小，估计误差可能越大。 如果工具的物理值非常小，建议用户手动输入工具数据。

- 如果机器人使用多个条件，例如单独工具或与工件结合的工具，则必须为每种情况单独登记工具数据。 对每个条件执行负载估计: (仅工具)和(工具 + 工件)。

{% hint style="info" %}
有效载荷容量小于50kg的机器人不支持负载估计功能。
{% endhint %}

- 为了获得最准确的结果，建议在充分预热后以及关闭控制器至少一个小时后执行负载估计。 当电机温度升高时，估计精度可能会降低。

{% hint style="info" %}
推荐的温度范围是35-40°C。 可以通过系统特征数据或负载估计日志文件检查编码器温度。
{% endhint %}

- 如果有设计值或测量值(例如重量、重心)等准确的工具数据，手动将这些值输入工具数据设置可以提供更高的精度。(需要执行“应用CAD数据”。)

![Fig 1.2 应用CAD数据](../_assets/image_12_eng.png)

- 在一个机器人模型上调校的值并不一定能保证在同一模型的其他单元上具有相同的估计性能。 机械和操作特性因机器人而异，包括机械公差、电机性能偏差、润滑条件和温度环境。
[__SOURCE](1-load-estimation-intro/3-procedure.md)
# 1.3 快速操作程序

按照下面表格中显示的顺序执行负载估算功能。

<br>

<table>
<tr>
<th><center>步骤</th>
<th> <center>任务</th>
</tr>

<tr>
<td rowspan="2" align="center">1</td>
<td align="center"><b>进入功能菜单 </b></td>
</tr>
<tr>
<td align="center">[F2:系统] - 6:自动校准 - 4:负载估算</td>
</tr>

<tr>
<td rowspan="2" align="center">2</td>
<td align="center"><b>输入添加的重量</td>
</tr>
<tr>
<td align="center">[F4:每轴添加重量]</td>
</tr>

<tr>
<td rowspan="2" align="center">3</td>
<td align="center"><b>设置主轴的姿态</td>
</tr>
<tr>
<td align="center">[F5:设置姿态]</td>
</tr>

<tr>
<td rowspan="2" align="center">4</td>
<td align="center"><b>设置腕轴的移动范围</td>
</tr>
<tr>
<td align="center">输入 B, R1 轴的操作范围 <Br>(某些范围可能无法进行估算)。</td>
</tr>

<tr>
<td rowspan="2" align="center">5</td>
<td align="center"><b>尝试测试操作
</td>
</tr>
<tr>
<td align="center">[F1:播放检查] <br> 检查低速下的干扰。</td>
</tr>

<tr>
<td rowspan="2" align="center">6</td>
<td align="center"><b>插入工具编号并操作 </b></td>
</tr>
<tr>
<td align="center">工具编号编辑框 <br> [F2:正常播放]</td>
</tr>

<tr>
<td rowspan="2" align="center">7</td>
<td align="center"><b>应用估算结果</b></td>
</tr>
<tr>
<td align="center">操作完成后，输入确认。</td>
</tr>

</table>
[__SOURCE](2-load-estimation-result/README.md)
# 2. 载荷估算详细信息
[__SOURCE](2-load-estimation-result/2-1-weight.md)
# 2.1 重量

这个值表示安装在机器人末端执行器上的有效载荷的总重量。单位是千克 (kg)。
[__SOURCE](2-load-estimation-result/2-2-weight-center-of-gravity.md)
# 2.2 重心

重心定义为从机器人的末端执行器到负载重心在 X、Y 和 Z 方向上的距离。使用的单位是毫米（mm）。
[__SOURCE](2-load-estimation-result/2-3-inertia.md)
# 2.3 惯性

此值表示有效载荷的转动惯量。它指的是每个分布重量乘以其与旋转轴的距离平方的总和，假设围绕 X、Y 和 Z 轴旋转。转动惯量由重量在每个轴上的分布方式决定——当更多的有效载荷重量位于离旋转轴更远时，值会更大。用于 X、Y 和 Z 轴的单位是 kg·m²。

![Fig 3. Inertia Calculation](<../_assets/image_10_eng.png>)
[__SOURCE](3-load-estimation-menu-explain/README.md)
# 3. 负载估算菜单描述

从 `[system] - 6.自动 校准 - 4:负载预估功能 ([system] - 6.Auto calibration - 4:Load estimation function)` 执行负载估算。

{% hint style="info" %}

当选择 `4:负载预估功能 (4:Load estimation function)` 菜单时，如果当前控制模式设置为 "Vibration Suppression Control"，电机将自动关闭以切换模式至 "PPI"。  
负载估算完成后，模式将自动返回 "Vibration Suppression Control"，电机将再次关闭。

{% endhint %}

![Fig 4. Load Estimation Screen](<../_assets/image_2_eng.png>)
[__SOURCE](3-load-estimation-menu-explain/3-1-tool-number.md)
# 3.1 工具编号

分配表示要使用的工具的工具编号。  
当分配的工具编号应用于教学程序时，机器人将根据估计的有效载荷属性进行操作。  
只有注册的工具数据才能用作工具编号。
[__SOURCE](3-load-estimation-menu-explain/3-2-motion-area.md)
# 3.2 操作范围

此屏幕显示用于负载估算的每个轴的运动范围。
“轴角”显示每个机器人轴的当前值，“起始位置”指示负载估算开始的初始位置。
“运动范围”中的“最小”和“最大”值表示在估算运动过程中使用的最小和最大轴限制。
对于 B 轴和 R1 轴，最小和最大运动范围可以配置。

默认的运动范围设置如下：

`默认运动范围`

  - B 轴运动范围（最小）：（60° - H 轴角 - V 轴角）

  - B 轴运动范围（最大）：（120° - H 轴角 - V 轴角）

  - R1 轴运动范围（最小）：0°

  - R1 轴运动范围（最大）：90°

根据配置的腕轴运动范围，某些负载属性可能无法测量。在这种情况下，用户必须手动输入负载数据。

![图5. 当重心 (Cx, Cy) 和惯性无法估算时的警告信息](<../_assets/image_3_eng.png>)

估算所有负载属性所需的 B 轴和 R1 轴的运动范围条件如下：

`完整负载估算的运动范围条件`

 - B 轴运动范围：必须在（40° - H - V）到（140° - H - V）之间

 - B 轴的最小运动角度：20°或更大

 - R1 轴的最小运动角度：60°或更大
[__SOURCE](3-load-estimation-menu-explain/3-3-check-operation.md)
# 3.3 测试操作

此功能用于检查可能的干扰。在执行“**检查操作 (Play check)**”功能时，不执行载荷估算。

由于载荷估算在预定义的运动模式下操作机器人以获取负载数据，因此在运动过程中必须注意与周围设备或机器人自身的干扰。因此，在运行 `正常运行 (Play normal)` 之前，用户必须执行 `检查操作 (Play check)` 以验证不存在碰撞风险。如果发生干扰，请按下急停按钮或将启用开关切换为关闭以停止机器人。

如果机器人在检查操作完成之前停止，则必须再次执行载荷估算菜单。

`[操作条件]`

  - 机器人控制器 : 手动模式

  - 启用开关 : 开
[__SOURCE](3-load-estimation-menu-explain/3-4-normal-operation.md)
# 3.4 正常操作

此菜单执行负载估算。由于操作以高速运行，必须在使用“**播放检查**”验证干扰安全后才可以执行。

`[操作条件]`

  - 机器人控制器 : 手动模式

  - 使能开关 : 开
[__SOURCE](3-load-estimation-menu-explain/3-5-additional-mass-by-axis.md)
# 3.5 额外的轴重量

导航到每个轴的额外重量菜单。
为了进行准确的负载估算，必须输入轴 3 的额外重量信息（重量、X 轴重心和 Z 轴重心）。
额外重量包括安装板、信号箱和附加到框架上的电缆等项目。

用于输入轴 3 的额外重量的坐标系统如下所示。

![Fig 6. Axis-3 Additional Weight Components and Coordinate System](<../_assets/image_9_eng.png>)
[__SOURCE](3-load-estimation-menu-explain/3-6-positioning.md)
# 3.6 姿态设置

指定估计运动的起始姿态。 用户必须手动移动机器人轴到不与机器人、工具或周围环境发生干扰的位置，然后按“**设置姿态**（设置主轴位置）”以注册起始姿态。

S轴没有限制；然而，H轴和V轴必须设置以保持V轴框架角度相对于地面基准在±60°以内。为了获得最佳的估计准确性，建议将V轴角度设置得尽可能接近0°。

如果用户在V轴角度超过±60°时尝试按“设置位置”，将出现一条消息：
“V轴角度必须相对于地面保持在±60°以内。”

1.  **当前轴角度**

    显示主机器人轴（S、H、V）的当前角度。

2.  **起始位置**

    显示注册的S、H和V轴角度，作为负载估计的起始姿态。一旦执行“**播放检查**”或“**正常播放**”按钮，机器人姿态将移动到指定位置。
[__SOURCE](4-load-estimation-motion-area/README.md)
# 4. 负载估计操作范围

用于负载估计的运动模式因机器人类型而异，例如6轴机器人（HDX系列，HDR系列等），4轴码垛机器人（HDP系列）和喷涂机器人（HDE系列）。相应的运动范围如下。
[__SOURCE](4-load-estimation-motion-area/4-1-6-axis-robot.md)
# 4.1 6-Axis Robot

![Fig 7. 负载估计操作范围 (6-axis robot)](<../_assets/image_5_eng.png>)
[__SOURCE](4-load-estimation-motion-area/4-2-4-axis-palletize-robot.md)
# 4.2 4-Axis Palletizing Robot

![Fig 8. Load Estimation Operating Range (4-Axis Palletizing Robot)](<../_assets/image_8_eng.png>)
[__SOURCE](4-load-estimation-motion-area/4-3-paint-robot.md)
# 4.3 喷漆机器人

![Fig 9. Load Estimation Operating Range (Painting Robot)](<../_assets/image_11_eng.png>)
[__SOURCE](5-load-estimation-result-application-method/README.md)
# 5. 如何应用负载估算结果
[__SOURCE](5-load-estimation-result-application-method/5-1-application.md)
# 5.1 应用负载估计结果

在查看负载估计结果后，按“OK”。当确认消息“应用估计值？”出现时，选择“是”将把估计的有效载荷数据保存到分配的工具编号。如果选择“否”，数据将不会被保存。

![Fig 10. Load Estimation Result Screen](<../_assets/image_1_eng.png>)

<br>

![Fig 11. Confirmation Window for Applying Estimated Results](<../_assets/image_6_eng.png>)

保存的工具数据将在机器人操作时应用，当在教学程序中选择相应的工具编号。因此，当工具更改或工具处理工件时，必须在教学程序中选择和使用代表该条件的工具数据。
[__SOURCE](5-load-estimation-result-application-method/5-2-check-modify.md)
# 5.2 检查和调整结果

估计的有效载荷数据可以从：
"设置" → "3. 机器人参数" → "1. 工具数据" 检查和修改。
估计结果将显示在用于负载估计过程的工具编号下。

![Fig 12. Tool Data Screen](<../_assets/image_7_eng.png>)

{% hint style="info" %}
估计的惯性值是相对于有效载荷的重心表示的。
如果特定方向的惯性值非常小，结果可能会显示为0。
{% endhint %}
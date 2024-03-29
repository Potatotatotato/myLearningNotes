# 降压（BUCK）电路
### 常用芯片
1. XL1509
2. 
### 低EMC设计要点
0. 采用晶圆倒装工艺的芯片，选择把Ci集成到内部的dcdc芯片。
1. 降低高di/dt回路面积。注意不是流过电感回路的面积，因为流过电感的回路电流连续变化，不是高di/dt回路。  
<div align="center"><image src="https://github.com/Potatotatotato/myLearningNotes/blob/main/DCDC_PCB/Images/Buck_schematicDigram.jpg" width=300></div>  

2. SW走线不能太窄，因为要通过大电流。SW节点电压跳变大，所以引脚不要大面积铺铜，避免SW铜皮化身天线辐射干扰。
3. 芯片、电感、输出电容回路面积尽可能降低以减小辐射。
4. Cin电容一般使用一个大电容，外加一个`0.1uf`的小电容来滤除高频干扰，两个电容的摆放位置应该尽可能靠近降压芯片的输入引脚，并且0.1uf的`小电容紧贴输入引脚`。Cout大电容应该紧贴输入引脚,`0.1uf`的小电容在大电容之后滤除高频干扰。输入电容的引脚布线应该粗而短。
5. FB回路面积应尽可能降低，2个分压电阻要紧贴FB引脚。Vout的取样点应在Cout`0.1uf`电容之后，滤除Vout上的高频干扰。
6. 小信号地与功率地应分开，并采用`0Ω`电阻单点接PGND。如果无法做到，可以把小信号地全部布在表层，最后通过一个过孔与底层GND相连。
7. 如果无法做到第5条，应注意FB分压电阻的GND应`与VoutGND相连`，并远离VinGND。这是因为输出回路中存在电感，由于电感上的电流不能突变，所以`VoutGND上噪声更小`。
8. FB走线应远离`电感/二极管`，特别是避免与电感平行。
9. 尽量采用单面布局，如果必须要双面布局，也要注意表面和底面的走线尽量`垂直`，不要平行走线，避免串扰。
10. 电感下面的表层GND应挖空，降低涡流损耗；底层铺GND减小对其他元器件的干扰，中间层最好也铺GND。
12. 电感尽量采用有屏蔽的电感。
13. 一般来说电容类型的选用应参考`MLCC > 钽电容 > 固态电容 > 高频低阻电解电容 > 普通铝电解电容`。
14. 电容的选型应注意：耐压稍微高一点，容值稍微大一点。MLCC电容存在直流偏压现象，即在MLCC两端施加直流电压，其容值会降低。
15. 3个容量一样的电容搭配，叫做“V型滤波”，因为频率特性就呈现一个V字，此时，要注意电路频率范围，必须保证你的滤波电容要时刻呈现容性。3个容量不同的电容搭配，滤波频率响应更宽更好，但是不同容量的电容会形成反谐振，所以推荐电容之间大小要相差两个数量级。但即使这样反谐振仍然不会消失，必须防止噪声频率落在反谐振点上。总之各有各的好处，但关键是一定对电路的噪声频率有个大致的预估。盲目的搭配电容可能反而恶化噪声。  
<div align="center"><image src="https://github.com/Potatotatotato/myLearningNotes/blob/main/DCDC_PCB/Images/Capacitor_frequency Response.jpg" width=300></div>   
  
### 参考视频
[唐老师讲电赛——电源大师6——BUCK 降压电路降低EMI与EMC设计，开关电源PCB layout宝典](https://www.bilibili.com/video/BV1ef4y1n7x1/?spm_id_from=333.788&vd_source=e6cfc8577ccc9621465b12d49ef2c1c3)   
  
# 升压（BOOST）电路
### 常用芯片
1. XL6008/XL6019
2. SX1308/MT3608(丝印B628)
### 低EMC设计要点
0. 采用晶圆倒装工艺的芯片，选择把Ci集成到内部的dcdc芯片。
1. 降低高di/dt回路面积。注意不是流过电感回路的面积，因为流过电感的回路电流连续变化，不是高di/dt回路。  
<div align="center"><image src="https://github.com/Potatotatotato/myLearningNotes/blob/main/DCDC_PCB/Images/Boost_schematicDigram.jpg" width=300></div>  

2. SW走线不能太窄，因为要通过大电流。芯片SW引脚与电感之间的距离应尽可能近一点。
3. Cin电容一般使用一个大电容，外加一个`0.1uf`的小电容来滤除高频干扰，两个电容的摆放位置应该尽可能靠近降压芯片的输入引脚，并且0.1uf的`小电容紧贴输入引脚`。Cout大电容应该紧贴输入引脚,`0.1uf`的小电容在大电容之后滤除高频干扰。
5. FB回路面积应尽可能降低，2个分压电阻要紧贴FB引脚。Vout的取样点应在Cout`0.1uf`电容之后，滤除Vout上的高频干扰。
6. 小信号地与功率地应分开，并采用`0Ω`电阻单点接PGND。如果无法做到，可以把小信号地全部布在表层，最后通过一个过孔与底层GND相连。
7. 如果无法做到第5条，应注意FB分压电阻的GND应`与VinGND相连`，并远离VoutGND。这是因为输出回路中存在电感，由于电感上的电流不能突变，所以`VinGND上噪声更小`。
8. FB走线应远离`电感/二极管`，特别是避免与电感平行。
9. 尽量采用单面布局，如果必须要双面布局，也要注意表面和底面的走线尽量`垂直`，不要平行走线，避免串扰。
10. 电感下面的表层GND应挖空，降低涡流损耗；底层铺GND减小对其他元器件的干扰，中间层最好也铺GND。
11. 电感之间的焊盘间距尽量大一些。
12. 电感尽量采用固态电感。
13. 一般来说电容类型的选用应参考`MLCC > 钽电容 > 固态电容 > 高频低阻电解电容 > 普通铝电解电容`，但也不排除某些芯片就要用“垃圾”电容。
14. 电容的选型应注意：耐压稍微高一点，容值稍微大一点。MLCC电容存在`直流偏压现象`，即在MLCC两端施加直流电压，其容值会降低。
  
### 参考视频
[唐老师讲电赛——电源大师8—BOOST升压电路EMI与EMC设计，BOOST升压电路PCB layout宝典](https://www.bilibili.com/video/BV1xU4y1A7GU/?spm_id_from=333.788&vd_source=e6cfc8577ccc9621465b12d49ef2c1c3)  
  
# 升降压（BUCK and BOOST）电路
### 常用芯片
1. 
### 原理图
  
# 开关电源提升效率的方法
1. 选择RDS(on)较小的MOS管
2. 采用同步整流。如果使用异步整流，选择导通电压小的续流二极管，选择反向恢复时间短的续流二极管
3. 对于电感，选择铁损小的磁芯或者降低电感上的电流变化量以`减小铁损`；选择线圈直流电阻`LDR`小的电感以`减小铜损`  

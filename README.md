#时间轴的编写方法
[act_timeline使用编写指南(日语)](https://coding.net/s/28de1f90-b4e3-4af0-a974-9ce0f52a86a6)
##时间轴文本放置位置
时间轴TXT文本放置在ACT文件夹中resources/timeline内
##自动加载
如果将时间轴文件命名为区域名称，则可以在移动区域后自动加载文件。
```
The Final Coil Of Bahamut - Turn (1).txt
欧米茄零式时空狭缝 德尔塔幻境1.txt
```
##时间轴主体书写

标准格式
```
战斗开始后秒数 "技能名称" [duration 提前倒数秒数] [sync /正则/ [window 误差调整]]
[]为选填项目。
```
例: 战斗开始90秒后使用破浪斩
```
90 "破浪斩"
```
- `xxx正在发动“技能名称”`
- `xxx发动了“技能名称”`

```
333 "八咫镜" sync /须佐之男发动了“八咫镜”/ window 2, 2
...
666 "云间放电" duration 2 sync /雷云正在发动“云间放电”/ window 2, 2
```
##增加删除对象

- `Added new combatant`
- `Removing combatant`

```
666 "天之丛云" sync /Added new combatant 天之丛云/ window 10
```
##隐藏
隐藏不需要的提示

```
hideall "技能名称"
```
##提示

标准格式
```
alertall "技能名称" before 技能发动前几秒播报 sound "提示音"
```
提示音需保存在 resources/wav 内
例："云间放电"发动3秒前播放se_maoudamasii_chime10.wav
```
alertall "云间放电" before 3 sound "se_maoudamasii_chime10.wav"
```
-TTS
直接调用电脑TTS
```
alertall "云间放电" before 3 sound  "tts 云间放电"
```
-提示音命名调用
```
define alertsound "提示音" "提示音.wav"
alertall "强击" before 3 sound "提示音"
```
#### 阶段性调整

一般调阶段时请将误差设为`10000`

```
1 "--开始--" sync /欢庆吧！跳舞吧！/ window 10000
...
666 "--Phase 2--" sync /有意思，真有意思！/ window 10000
```

<br />

##跳转

- `jump` 跳转时间

##循环

```
333 "岩户隐" sync /须佐之男发动了“岩户隐”/ window 2, 2
...
666 "岩户隐" sync /须佐之男发动了“岩户隐”/ window 100 jump 333
```

##重置

- 使用 `Removing combatant` 判断Boss重置
- 如果指定了0秒，将在起始位置进入待机状态。

```
0 "--重置--" sync /Removing combatant 须佐之男/ window 10000 jump 0
```
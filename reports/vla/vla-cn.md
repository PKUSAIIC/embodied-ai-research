# VLA（视觉-语言-动作）研究综述（2026）

**Organization:** PKUSAIIC  
**Language:** Chinese  
**Topic:** Vision-Language-Action (VLA) / Embodied AI  
**Status:** Public Release  

---

## 摘要
本文系统梳理视觉-语言-动作（VLA）模型的定义框架、能力层级、核心架构、训练范式、关键技术挑战与产业发展趋势，重点分析其从实验室原型走向工业级具身智能系统所面临的核心瓶颈与代表性突破路径。

---

## 目录
- 一、VLA的定义框架、能力层级与现状评估
- 二、VLA的核心架构设计与实现机理
- 三、VLA训练范式
- 四、核心技术挑战：从“实验室 Demo”到“通用 AI”的阻碍
- 五、应对路径与发展趋势：迈向工业级具身智能

---

<p align="center">
<b>一、 VLA的定义框架、能力层级与现状评估</b>
</p>


<p class=MsoNormal style='margin-top:7.8pt;margin-right:0cm;margin-bottom:7.8pt;
margin-left:0cm;line-height:120%'><b><span lang=EN-US style='line-height:120%;
font-family:SimSun'>1.1  VLA</span></b><b><span lang=ZH-CN style='line-height:
120%;font-family:SimSun'>的核心定义与技术范畴</span></b></p>


<p class=MsoNormal style='text-indent:21.0pt;line-height:120%'><b><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>VLA</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>（视觉</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>-</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>语言</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>-</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>动作）模型是当前具身智能领域的核心模型</span></b><b><span
lang=ZH-CN style='font-family:SimSun'>。</span></b><span lang=EN-US
style='font-family:SimSun'>VLA</span><span lang=ZH-CN style='font-family:SimSun'>能够直接将机器视觉画面和语言指令融合在一起，一步到位地输出机器人应该执行的动作，这种端到端的范式<span
style='color:black'>——即直接从原始感官输入映射到最终动作输出，彻底打破了传统系统中“感知</span></span><span
lang=EN-US style='font-family:SimSun;color:black'>-</span><span lang=ZH-CN
style='font-family:SimSun;color:black'>建图</span><span lang=EN-US
style='font-family:SimSun;color:black'>-</span><span lang=ZH-CN
style='font-family:SimSun;color:black'>规划</span><span lang=EN-US
style='font-family:SimSun;color:black'>-</span><span lang=ZH-CN
style='font-family:SimSun;color:black'>控制”层层解耦的繁琐中间模块——极</span><span
lang=ZH-CN style='font-family:SimSun'>大提升了系统的反应效率。</span></p>


<p class=MsoNormal style='text-indent:21.0pt;line-height:120%'><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>动作表征的粒度选择，决定了机器人是笨拙还是灵巧。</span></b><span
lang=ZH-CN style='font-family:SimSun'>在</span><span lang=EN-US
style='font-family:SimSun'>VLA</span><span lang=ZH-CN style='font-family:SimSun'>的架构里，动作可以是抽象的高级指令（如：拿杯子），也可以是底层连续的电流信号（如：各个关节转动多少度）。这种从宏观到微观的跨度被称为动作表征谱系（注：可理解为机器人的动作词典），词典越底层、越精细，机器人的动作就越丝滑，但模型的训练难度也呈指数级上升。</span></p>


<p class=MsoNormal style='text-indent:21.0pt;line-height:120%'><b><span
lang=EN-US style='font-family:SimSun'>VLA</span></b><b><span lang=ZH-CN
style='font-family:SimSun'>并不等同于单纯的</span></b><b><span lang=EN-US
style='font-family:SimSun'>“</span></b><b><span lang=ZH-CN style='font-family:
SimSun'>看图说话</span></b><b><span lang=EN-US style='font-family:SimSun'>”</span></b><b><span
lang=ZH-CN style='font-family:SimSun'>机器人，其核心分水岭在于能否生成物理动作。</span></b><span
lang=ZH-CN style='font-family:SimSun'>传统的视觉语言模型（</span><span lang=EN-US
style='font-family:SimSun'>VLM</span><span lang=ZH-CN style='font-family:SimSun'>）即便具备强大的图文理解能力，能进行复杂的逻辑推理甚至生成详细的行动步骤文本（例如告诉你</span><span
lang=EN-US style='font-family:SimSun'>“</span><span lang=ZH-CN
style='font-family:SimSun'>需要先避开水杯，再抓取苹果</span><span lang=EN-US
style='font-family:SimSun'>”</span><span lang=ZH-CN style='font-family:SimSun'>），但只要它无法直接输出驱动电机的物理控制信号，那它依然只是</span><span
lang=EN-US style='font-family:SimSun'>VLM</span><span lang=ZH-CN
style='font-family:SimSun'>；只有当它能伸出机械臂去抓取苹果时，才算跨入了</span><span lang=EN-US
style='font-family:SimSun'>VLA</span><span lang=ZH-CN style='font-family:SimSun'>的门槛。</span></p>


<p class=MsoNormal style='margin-top:7.8pt;margin-right:0cm;margin-bottom:7.8pt;
margin-left:0cm;line-height:120%'><b><span lang=EN-US style='line-height:120%;
font-family:SimSun'>1.2  VLA</span></b><b><span lang=ZH-CN style='line-height:
120%;font-family:SimSun'>能力分级框架：从技术原理到应用效能</span></b></p>


<p class=MsoNormal style='text-indent:21.0pt;line-height:120%'><span
lang=ZH-CN style='font-family:SimSun'>为了直观评估</span><span lang=EN-US
style='font-family:SimSun'>VLA</span><span lang=ZH-CN style='font-family:SimSun'>的进化水平，我们将其能力划分为四个递进的能力层级，如表</span><span
lang=EN-US style='font-family:SimSun'>1</span><span lang=ZH-CN
style='font-family:SimSun'>所示。随着层级的提升，机器人面对的任务复杂度越来越高，对未知环境的适应能力（即泛化能力）也越来越强。只有跨越前三个层级，</span><span
lang=EN-US style='font-family:SimSun'>VLA</span><span lang=ZH-CN
style='font-family:SimSun'>才能最终触及通用具身智能（</span><span lang=EN-US
style='font-family:SimSun'>AGI</span><span lang=ZH-CN style='font-family:SimSun'>）的终极目标。</span></p>


<p class=MsoNormal align=center style='margin-top:7.8pt;margin-right:0cm;
margin-bottom:7.8pt;margin-left:0cm;text-align:center;line-height:120%'><span
lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun'>表</span><span
lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun'>1 </span><span
lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun'>：</span><span
lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun'>VLA</span><span
lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun'>（视觉</span><span
lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun'>-</span><span
lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun'>语言</span><span
lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun'>-</span><span
lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun'>动作）模型能力分级全景评估表</span></p>


<div align=center>


<table class=MsoNormalTable border=1 cellspacing=30 cellpadding=0 width=609
 style='width:456.9pt;border:none #1F1F1F 1.0pt'>
 <thead>
  <tr style='height:32.4pt'>
   <td width=68 style='width:50.8pt;border-top:solid windowtext 1.5pt;
   border-left:none;border-bottom:solid windowtext 1.0pt;border-right:none;
   padding:3.0pt 4.5pt 3.0pt 4.5pt;height:32.4pt'>
   <p class=MsoNormal align=center style='text-align:center;line-height:120%;
   page-break-after:avoid;layout-grid-mode:char'><span lang=ZH-CN
   style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>能力层级</span></p>
   <p class=MsoNormal align=center style='text-align:center;line-height:120%;
   page-break-after:avoid;layout-grid-mode:char'><span lang=EN-US
   style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>(Level)</span></p>
   </td>
   <td width=97 style='width:72.65pt;border-top:solid windowtext 1.5pt;
   border-left:none;border-bottom:solid windowtext 1.0pt;border-right:none;
   padding:3.0pt 4.5pt 3.0pt 4.5pt;height:32.4pt'>
   <p class=MsoNormal align=center style='text-align:center;line-height:120%;
   page-break-after:avoid;layout-grid-mode:char'><span lang=ZH-CN
   style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>核心通俗理解</span></p>
   </td>
   <td width=90 style='width:67.4pt;border-top:solid windowtext 1.5pt;
   border-left:none;border-bottom:solid windowtext 1.0pt;border-right:none;
   padding:3.0pt 4.5pt 3.0pt 4.5pt;height:32.4pt'>
   <p class=MsoNormal align=center style='text-align:center;line-height:120%;
   page-break-after:avoid;layout-grid-mode:char'><span lang=ZH-CN
   style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>典型应用场景</span></p>
   </td>
   <td width=197 style='width:147.9pt;border-top:solid windowtext 1.5pt;
   border-left:none;border-bottom:solid windowtext 1.0pt;border-right:none;
   padding:3.0pt 4.5pt 3.0pt 4.5pt;height:32.4pt'>
   <p class=MsoNormal align=center style='text-align:center;line-height:120%;
   page-break-after:avoid;layout-grid-mode:char'><span lang=ZH-CN
   style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>当前痛点与技术瓶颈</span></p>
   </td>
   <td width=146 style='width:109.15pt;border-top:solid windowtext 1.5pt;
   border-left:none;border-bottom:solid windowtext 1.0pt;border-right:none;
   padding:3.0pt 4.5pt 3.0pt 4.5pt;height:32.4pt'>
   <p class=MsoNormal align=center style='text-align:center;line-height:120%;
   page-break-after:avoid;layout-grid-mode:char'><span lang=EN-US
   style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>2025-2026</span><span
   lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
   color:#1F1F1F'>代表性进展</span></p>
   </td>
  </tr>
 </thead>
 <tr style='height:57.25pt'>
  <td width=68 style='width:50.8pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:57.25pt'>
  <div style='border:none #1F1F1F 1.0pt;padding:0cm 0cm 0cm 0cm'>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><b><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>Level 1</span></b><b><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>：指令</span></b><b><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>-</span></b><b><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>动作映射</span></b><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> </span></p>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><i><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>(</span></i><i><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>任务复现</span></i><i><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>)</span></i></p>
  </div>
  </td>
  <td width=97 style='width:72.65pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:57.25pt'>
  <div style='border:none #1F1F1F 1.0pt;padding:0cm 0cm 0cm 0cm'>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> </span></p>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>听到单一指令，执行一个确定的抓取动作。</span></p>
  </div>
  </td>
  <td width=90 style='width:67.4pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:57.25pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>工业流水线分拣、实验室桌面物品拾取。</span></p>
  </td>
  <td width=197 style='width:147.9pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:57.25pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><b><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>泛化能力极弱：</span></b><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> 换个背景、光线或物体位置稍微偏移，机器人就会彻底罢工。</span></p>
  </td>
  <td width=146 style='width:109.15pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:57.25pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><b><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>工业大模型化：</span></b><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> Covariant</span><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>、梅卡曼德等企业在结构化产线实现</span><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>“</span><span lang=ZH-CN style='font-size:9.0pt;line-height:
  120%;font-family:SimSun;color:#1F1F1F'>开箱即用</span><span lang=EN-US
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>”</span><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>的高精度抓取。</span></p>
  </td>
 </tr>
 <tr style='height:67.3pt'>
  <td width=68 style='width:50.8pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:67.3pt'>
  <div style='border:none #1F1F1F 1.0pt;padding:0cm 0cm 0cm 0cm'>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><b><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>Level 2</span></b><b><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>：技能序列组合</span></b><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> </span></p>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><i><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>(</span></i><i><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>程序性任务</span></i><i><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>)</span></i></p>
  </div>
  </td>
  <td width=97 style='width:72.65pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:67.3pt'>
  <div style='border:none #1F1F1F 1.0pt;padding:0cm 0cm 0cm 0cm'>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>把</span><span lang=EN-US style='font-size:9.0pt;line-height:
  120%;font-family:SimSun;color:#1F1F1F'>“</span><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>走、抓、放</span><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>”</span><span lang=ZH-CN style='font-size:9.0pt;line-height:
  120%;font-family:SimSun;color:#1F1F1F'>等已有技能串联成组合拳执行。</span></p>
  </div>
  </td>
  <td width=90 style='width:67.4pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:67.3pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>家庭机器人</span><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>“</span><span lang=ZH-CN style='font-size:9.0pt;line-height:
  120%;font-family:SimSun;color:#1F1F1F'>泡茶</span><span lang=EN-US
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>”</span><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>、仓储机器人</span><span lang=EN-US style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>“</span><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>取货</span><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>-</span><span lang=ZH-CN style='font-size:9.0pt;line-height:
  120%;font-family:SimSun;color:#1F1F1F'>打包</span><span lang=EN-US
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>”</span><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>流水线。</span></p>
  </td>
  <td width=197 style='width:147.9pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:67.3pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><b><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>环境抗扰动差：</span></b><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> 中间任何一步出错（如没抓稳），后续步骤就会引发灾难性崩溃；严重依赖预先编程或学习的固定技能库，灵活性受限。</span></p>
  </td>
  <td width=146 style='width:109.15pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:67.3pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><b><span lang=EN-US
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>LLM</span></b><b><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>智能调度：</span></b><span lang=EN-US style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'> SayCan</span><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>等模型利用大模型做大脑，动态编排底层死板的动作库。</span></p>
  </td>
 </tr>
 <tr style='height:63.65pt'>
  <td width=68 style='width:50.8pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:63.65pt'>
  <div style='border:none #1F1F1F 1.0pt;padding:0cm 0cm 0cm 0cm'>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><b><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>Level 3</span></b><b><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>：连续轨迹生成</span></b><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> </span></p>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><i><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>(</span></i><i><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>动态交互</span></i><i><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>)</span></i></p>
  </div>
  </td>
  <td width=97 style='width:72.65pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:63.65pt'>
  <div style='border:none #1F1F1F 1.0pt;padding:0cm 0cm 0cm 0cm'>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>直面物理环境，实时输出平滑、精细的连续动作。</span></p>
  </div>
  </td>
  <td width=90 style='width:67.4pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:63.65pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>柔性线缆插拔、动态避障、人机递送工具协作。</span></p>
  </td>
  <td width=197 style='width:147.9pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:63.65pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><b><span lang=EN-US
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>Sim2Real</span></b><b><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>跨越难：</span></b><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'> 仿真训练好，但在真机物理环境容易因传感器噪声和摩擦力影响；<b>真机数采成本极高：</b>真实物理世界的高质量连续轨迹数据高度依赖人工遥操作录制，成本高昂且极难实现规模化扩展。</span></p>
  </td>
  <td width=146 style='width:109.15pt;border:none;padding:3.0pt 4.5pt 3.0pt 4.5pt;
  height:63.65pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><b><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>基础模型爆发：</span></b><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> 采用流匹配技术的</span><span lang=EN-US style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>π0 (Pi0)</span><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>、及极低算力成本的开源模型</span><span lang=EN-US style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'> SmolVLA</span><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>。</span></p>
  </td>
 </tr>
 <tr style='height:65.6pt'>
  <td width=68 style='width:50.8pt;border:none;border-bottom:solid windowtext 1.5pt;
  padding:3.0pt 4.5pt 3.0pt 4.5pt;height:65.6pt'>
  <div style='border:none #1F1F1F 1.0pt;padding:0cm 0cm 0cm 0cm'>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><b><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>Level 4</span></b><b><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>：长时程开放任务</span></b><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> </span></p>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><i><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>(</span></i><i><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>高层智能</span></i><i><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>)</span></i></p>
  </div>
  </td>
  <td width=97 style='width:72.65pt;border:none;border-bottom:solid windowtext 1.5pt;
  padding:3.0pt 4.5pt 3.0pt 4.5pt;height:65.6pt'>
  <div style='border:none #1F1F1F 1.0pt;padding:0cm 0cm 0cm 0cm'>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> </span></p>
  <p class=MsoNormal align=left style='margin-top:5.0pt;margin-right:0cm;
  margin-bottom:5.0pt;margin-left:0cm;text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char;border:none;padding:0cm'><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>无需明确步骤，自主推理并完成极其复杂的任务。</span></p>
  </div>
  </td>
  <td width=90 style='width:67.4pt;border:none;border-bottom:solid windowtext 1.5pt;
  padding:3.0pt 4.5pt 3.0pt 4.5pt;height:65.6pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>整理陌生凌乱房间、根据模糊图纸组装未知家具。</span></p>
  </td>
  <td width=197 style='width:147.9pt;border:none;border-bottom:solid windowtext 1.5pt;
  padding:3.0pt 4.5pt 3.0pt 4.5pt;height:65.6pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><b><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>常识与长程记忆缺失：</span></b><span
  lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> 极易发生</span><span lang=EN-US style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>“</span><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>做到一半忘了要做什么</span><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>”</span><span lang=ZH-CN style='font-size:9.0pt;line-height:
  120%;font-family:SimSun;color:#1F1F1F'>的规划漂移现象。</span></p>
  </td>
  <td width=146 style='width:109.15pt;border:none;border-bottom:solid windowtext 1.5pt;
  padding:3.0pt 4.5pt 3.0pt 4.5pt;height:65.6pt'>
  <p class=MsoNormal align=left style='text-align:left;line-height:120%;
  page-break-after:avoid;layout-grid-mode:char'><b><span lang=ZH-CN
  style='font-size:9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>引入</span></b><b><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>“</span></b><b><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>机器慢思考</span></b><b><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'>”</span></b><b><span lang=ZH-CN style='font-size:9.0pt;
  line-height:120%;font-family:SimSun;color:#1F1F1F'>：</span></b><span
  lang=EN-US style='font-size:9.0pt;line-height:120%;font-family:SimSun;
  color:#1F1F1F'> Gemini Robotics 1.5 </span><span lang=ZH-CN style='font-size:
  9.0pt;line-height:120%;font-family:SimSun;color:#1F1F1F'>采用双系统，行动前先调用常识库进行逻辑推理。</span></p>
  </td>
 </tr>
</table>
<p class=MsoNormal align=left style='text-align:left;line-height:120%'><span
lang=EN-US>&nbsp;</span></p>


<p class=MsoNormal style='margin-top:8.0pt;margin-right:0cm;margin-bottom:4.0pt;
margin-left:0cm;line-height:120%;page-break-after:avoid'><b><span lang=ZH-CN
style='font-size:14.0pt;line-height:120%;font-family:SimSun'>二</span></b><b><span
lang=EN-US style='font-size:14.0pt;line-height:120%;font-family:SimSun'>.VLA </span></b><b><span
lang=ZH-CN style='font-size:14.0pt;line-height:120%;font-family:SimSun'>的核心架构设计与实现机理</span></b></p>


<p class=MsoNormal style='line-height:120%'><b><span lang=EN-US
style='font-size:12.0pt;line-height:120%;font-family:SimSun'><img width=415
height=227 src="./images/image001.png"></span></b></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><b><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>2.1 </span></b><b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>多模态感知编码与时空对齐</span></b></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=EN-US style='line-height:120%;font-family:SimSun'>VLA
</span></b><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>的第一步是把摄像头等传感器的</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>非结构化信息</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>编码成可计算的表征，并在时间与空间上对齐，为后续决策提供稳定输入。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>与传统机器人</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>感知</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>—</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>规划</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>—</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>控制</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>强模块化流水线不同，</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>VLA </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>通常更强调把</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>多模态理解</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>—</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>动作生成</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>尽量在同一策略内端到端联训，使模型同时处理视觉语义、语言约束与环境几何关系，从而减少跨模块接口损失与误差传递。对比来看，</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>VLM</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>（</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>Vision-Language Model</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>）本质上以</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>理解</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>/</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>生成语义</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>为主，落到机器人系统时更常见两条集成路径：其一是<strong><span
style='font-family:SimSun'>端到端</span></strong>路线，将</span><span lang=EN-US
style='line-height:120%;font-family:SimSun'> VLM </span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun'>与策略学习</span><span lang=EN-US
style='line-height:120%;font-family:SimSun'>/</span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun'>动作头联训，让视觉</span><span lang=EN-US
style='line-height:120%;font-family:SimSun'>—</span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun'>语言表征直接服务于动作输出；其二是<strong><span
style='font-family:SimSun'>分层式</span></strong>路线，把</span><span lang=EN-US
style='line-height:120%;font-family:SimSun'> VLM </span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun'>作为上层感知与推理模块（例如目标识别、关系推断、任务分解与约束生成），再由下层规划器与控制器完成可执行轨迹与高频闭环。无论采用哪条路径，感知侧的上限往往直接决定系统在真实场景下的成功率，尤其体现在遮挡、视角变化、光照扰动与动态物体等因素下的鲁棒性。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>当前架构演进的主趋势，是从以</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'> 2D </span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>语义为主的被动观测走向更强调</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'> 3D </span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>几何一致性的主动空间理解。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>早期</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> VLA/</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>视觉策略模型常用预训练</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> CNN </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>或</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> ViT </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>提取单帧或短序列的</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> 2D </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>特征，擅长</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>识别这是什么</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>，但在</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>它在哪里、怎么抓、会不会碰撞</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>这些与可执行动作强相关的问题上容易出现信息缺失。为缓解这一矛盾，越来越多工作把深度、点云、体素、可微重建等显式或隐式的</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> 3D </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>信息纳入编码过程，使模型不仅能做语义分类，还能在特征层面保留几何约束与跨视角一致性。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=EN-US style='line-height:120%;font-family:SimSun'>2D
</span></b><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>到</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'> 3D </span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>的升级，本质是在减少几何信息丢失，从而提升对遮挡与深度相关任务的可控性。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>纯</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> 2D </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>表征常把三维世界压缩到二维投影，导致同一物体在不同视角下的特征分布不稳定；同时，抓取与操作通常依赖</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>物体表面可达区域、法向、姿态</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>等几何量，</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>2D </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>特征很难直接提供这些可操作信息。因此，体素网格与点云编码等方法通过显式空间占位表达，增强了对三维结构的利用能力；而一些更前沿的可微三维表示（例如基于多视角一致性的重建）则把</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>几何先验</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>融入特征学习，使视觉特征更接近真实空间结构而非单视角纹理。</span></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><span
lang=EN-US style='line-height:120%;font-family:SimSun'><img width=415
height=227 src="./images/image002.png"></span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>跨模态语义对齐决定了语言如何</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>指挥</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>视觉聚焦与动作生成，是</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'> VLA </span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>从感知走向可控执行的关键桥梁。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>在</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> VLA </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>中，语言指令不仅是任务描述，更是对注意力分配与决策约束的显式输入：例如</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>把左边的红色杯子放到托盘上</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>，模型需要把</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>左边</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>/</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>红色</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>/</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>杯子</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>/</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>托盘</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>与视觉中的具体实例对齐，并把</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>放到</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>映射为一类可执行的运动模式。工程上常见做法是构建共享嵌入空间并通过多模态融合模块（如融合</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> Transformer</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>）让语言与视觉</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> token </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>交互：语言提供</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>查询与约束</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>，视觉提供</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>候选与证据</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>，融合模块学习两者之间的匹配与依赖关系，从而把语义落实到可操作对象与关键区域上。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>时序建模与对齐让</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'> VLA </span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>不只</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>看一眼做一次</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>，而是能在动态环境中形成稳定的行动依据。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>真实机器人任务往往具有部分可观测性：目标可能短暂离开视野，或被手臂遮挡；同时执行会引入延迟与误差。因而，感知侧通常需要把多帧观测与历史动作纳入表示，形成带时间上下文的状态表征。常见策略包括对图像序列进行时序编码、引入记忆模块或在融合层显式使用历史</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> token</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>，使模型能够在短期内维持对目标与场景的连续理解，为后续</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>滚动重规划</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>提供信息基础。</span></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><b><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>2.2 </span></b><b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>决策生成模型：从序列预测到分布建模</span></b></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=EN-US style='line-height:120%;font-family:SimSun'>VLA
</span></b><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>的决策模块负责把</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>对齐后的多模态表征</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>转化为动作，其核心矛盾是既要高精度控制，又要覆盖多种合理策略。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>机器人操作并非总是单一最优解：绕障可以左绕或右绕，抓取点可能有多个可行位置，放置也可能存在多种稳定姿态。决策模型一方面要具备足够表达能力以覆盖这些多峰解，另一方面还要输出可执行、平滑、与控制约束兼容的动作序列。当前主流路线大体分为两类：把动作离散化后做自回归序列建模，或直接在连续空间中学习动作分布并生成轨迹（扩散策略等）。</span></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><span
lang=EN-US style='line-height:120%;font-family:SimSun'><img width=415
height=227 id="图片 2" src="./images/image003.png"></span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>自回归范式通过</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>离散动作</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'> token + </span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>下一步预测</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>把控制问题转化为标准序列建模，优点是成熟、易扩展，但面临离散化精度与稳定控制的权衡。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>该路线借鉴语言模型的训练与推理机制：将连续动作（例如末端位姿增量、关节增量）量化成有限集合的离散符号，然后像生成文本一样逐步生成动作序列。其优势在于可直接利用大规模序列建模经验与预训练能力，尤其适合高层动作组合与长任务链；但离散化不可避免带来分辨率问题：</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>bins</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>（</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>连续动作离散化时的</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>档位数量与每档的间隔</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>）太粗会导致动作不够精细甚至抖动，</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>bins </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>太细又会显著扩大输出空间并增加学习难度。因此实际系统中，自回归</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> VLA </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>常更偏向输出</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>高层可执行意图</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>（例如下一段轨迹的粗略目标或动作片段），而把高频稳定性留给底层控制器闭环保证。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>扩散策略等分布建模方法更强调</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>生成一段平滑轨迹并显式覆盖多种可能</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>，在多解与精细操作场景中更具优势。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>这类方法把动作生成视为条件生成问题：模型学习在给定观测与指令条件下的动作轨迹分布，而不是只输出单一动作点。扩散策略的直觉是从噪声出发逐步去噪得到动作轨迹，它天然适合表达多峰分布：同一条件下可以采样得到不同但都合理的动作方案，从而提升在复杂场景中的成功率。与此同时，许多实现会采用</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>一次预测未来 </span><span
lang=EN-US style='font-size:10.5pt;font-family:"Calibri",sans-serif;position:
relative;top:4.0pt'><img width=10 height=16
src="./images/image004.png"></span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun'>步</span><span lang=EN-US
style='line-height:120%;font-family:SimSun'>”</span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun'>的块状输出，使得轨迹在时间上更一致、动作更平滑，也更容易与后续的分层控制框架衔接。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>从工程落地角度看，决策模型的选择通常不是二选一，而是与任务复杂度、实时性预算与安全需求共同决定。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>当任务以长序列语义规划为主、对精细控制要求相对较低时，自回归路线往往更易集成并具备较好可扩展性；当任务存在明显多解、需要更细腻的轨迹与接触过程（如插入、对齐、精细放置）时，分布建模路线更能提供稳定收益。实际系统也常采用混合方案：上层用更强的多模态模型决定策略与约束，下层用更专门的轨迹生成或控制策略确保平滑与可执行。</span></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><span
lang=EN-US style='line-height:120%;font-family:SimSun'>&nbsp;</span></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><b><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>2.3 </span></b><b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>系统集成与分层控制架构</span></b></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=EN-US style='line-height:120%;font-family:SimSun'>VLA
</span></b><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>在真实机器人上必须通过分层控制解决</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>推理频率低</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>和</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>执行需要高频闭环</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>之间的结构性矛盾。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>大模型（尤其</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> Transformer </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>类多模态模型）通常推理频率较低，而电机控制与力控制需要高频闭环以抑制扰动与误差积累。若让</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> VLA </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>直接输出电机级控制信号，不仅实时性难以满足，也会放大模型不确定性带来的风险。因而业界普遍采用分层架构：</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>VLA </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>在上层低频输出动作片段或轨迹目标，底层由传统控制器或专用控制策略以高频执行与跟踪，从而在可解释性与稳定性上形成互补。</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>分层架构是机器人领域长期沿用的</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>任务</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>/</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>规划</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>—</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>轨迹生成</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>—</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>伺服控制</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>范式。随着端到端学习与</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> VLA </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>上机实践推进，直接输出低层控制在样本效率、分布外安全与实时性上暴露出更多工程瓶颈，使得</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>高层学习</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>/</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>推理、底层高带宽闭环</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>的折中路径逐步成为主流。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=EN-US style='line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>动作分块</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'> + </span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>滚动视界控制</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>的组合，使低频的</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'> VLA </span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>能以闭环方式驱动机器人并持续纠偏。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>上层</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> VLA </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>往往一次性预测未来一段动作序列（动作分块），而非只预测下一步，但执行时并不照单全收，而是只执行其中前若干步，再基于最新观测重新调用模型生成新的动作分块（滚动视界</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>/</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>递推式重规划），执行一小段后基于新观测重新规划，形成闭环纠偏。这种设计把端到端模型纳入闭环：一方面缓解模型推理慢的问题，另一方面降低对单次预测正确性的依赖，使系统能够在环境变化、目标移动或执行误差出现时及时修正。</span></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><span
lang=EN-US style='line-height:120%;font-family:SimSun'><img width=415
height=227 id="图片 3" src="./images/image005.png"></span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>安全过滤器是端到端系统走向可部署的必备组件，用于把</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>黑盒输出</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>约束在可达、无碰撞、满足规则的安全集合内。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>端到端</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> VLA </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>的失败模式往往难以在训练阶段完全覆盖，部署时必须考虑最坏情况。工程上常在</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'> VLA </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>输出与执行器之间串联安全模块：先做运动学可达性检查（例如逆运动学验证目标位姿是否可行），再做碰撞检测与安全约束修正（例如基于几何检测、约束投影或控制障碍函数思想），必要时对动作进行裁剪、重定向或触发降级策略（如停机、回撤、重新规划）。这类</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>可证明或可检验</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>的安全层能显著降低端到端策略直接造成硬件损坏或人员风险的概率。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>在移动操作（</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun'>Loco-manipulation</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>）等复杂形态下，系统还需要考虑底盘与机械臂的协同，否则上层语义正确也可能因可达性失败而无法完成任务。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>当机器人同时具备移动与操作能力时，动作不仅是</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>手怎么动</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>，还包括</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>车怎么停</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>。上层策略需要把任务约束转化为全身可达的子目标（例如先移动到合适观察与操作位置，再执行抓取），下层则需要在导航与操作之间做时间与空间的协调，并在动态环境中持续避障与纠偏。分层控制在此类系统中尤为关键：</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>VLA </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>提供语义与策略层面的决策，传统模块提供可达性、稳定性与安全性保障，二者共同构成可部署的闭环系统。</span></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><span
lang=EN-US style='line-height:120%;font-family:SimSun'>&nbsp;</span></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><b><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>2.4 </span></b><b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>小结</span></b></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.1pt;
line-height:120%'><b><span lang=EN-US style='line-height:120%;font-family:SimSun'>VLA
</span></b><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>的核心架构可以概括为：以多模态感知获得对环境与指令的对齐表征，以生成式决策模型输出动作意图或轨迹，再通过分层控制与安全过滤把模型能力转化为可稳定执行的机器人行为。</span></b><span
lang=EN-US style='line-height:120%;font-family:SimSun'><br>
</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun'>这一链路的关键不在于单点模型</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>“</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>更大</span><span
lang=EN-US style='line-height:120%;font-family:SimSun'>”</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun'>，而在于感知的几何一致性、跨模态对齐的可控性、动作生成对多解与精度的兼容，以及系统工程层面对实时性与安全性的闭环保障。</span></p>


<p class=MsoNormal style='line-height:120%'><span lang=EN-US>&nbsp;</span></p>

<p class=MsoNormal style='margin-top:8.0pt;margin-right:0cm;margin-bottom:4.0pt;
margin-left:0cm;line-height:120%;page-break-after:avoid'><b><span lang=ZH-CN
style='font-size:14.0pt;line-height:120%;font-family:SimSun'>三、</span></b><b><span
lang=EN-US style='font-size:14.0pt;line-height:120%;font-family:SimSun'> VLA</span></b><b><span
lang=ZH-CN style='font-size:14.0pt;line-height:120%;font-family:SimSun'>训练范式</span></b></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
line-height:120%'><b><span lang=EN-US style='line-height:120%;font-family:SimSun;
color:black'>3.1 </span></b><b><span lang=ZH-CN style='line-height:120%;
font-family:SimSun;color:black'>训练阶段及数据来源</span></b></p>


<p class=MsoNormal style='line-height:120%'><span lang=EN-US style='font-family:
SimSun'>    </span><span lang=ZH-CN style='font-family:SimSun'>典型的</span><span
lang=EN-US style='font-family:SimSun'>VLA</span><span lang=ZH-CN
style='font-family:SimSun'>模型采用“预训练视觉语言模型（</span><span lang=EN-US
style='font-family:SimSun'>VLM</span><span lang=ZH-CN style='font-family:SimSun'>）</span><span
lang=EN-US style='font-family:SimSun'>+ </span><span lang=ZH-CN
style='font-family:SimSun'>动作生成模块”的两段式架构。首先，预训练</span><span lang=EN-US
style='font-family:SimSun'>VLM</span><span lang=ZH-CN style='font-family:SimSun'>作为感知与语义核心，将图像等多模态输入与文本指令编码至统一隐空间，形成结构化任务表征；随后，在该语义表示基础上引入动作解码模块，将高层语义映射为机器人控制序列。常见做法是将连续控制信号离散化为</span><span
lang=EN-US style='font-family:SimSun'>token</span><span lang=ZH-CN
style='font-family:SimSun'>，使动作生成与语言生成同构，从而复用大模型的序列建模能力，实现端到端控制输出。这一架构兼顾语义泛化能力与可执行性，已成为当前</span><span
lang=EN-US style='font-family:SimSun'>VLA</span><span lang=ZH-CN
style='font-family:SimSun'>的主流实现路径。</span></p>


<p class=MsoNormal style='text-indent:21.0pt;line-height:120%'><span
lang=EN-US style='font-family:SimSun'>VLA</span><span lang=ZH-CN
style='font-family:SimSun'>（视觉</span><span lang=EN-US style='font-family:SimSun'>-</span><span
lang=ZH-CN style='font-family:SimSun'>语言</span><span lang=EN-US
style='font-family:SimSun'>-</span><span lang=ZH-CN style='font-family:SimSun'>动作）模型的训练本质上依赖多种学习范式的融合，需要将互联网规模的语义知识与机器人领域的具身任务数据进行系统整合。由于其多模态统一架构同时承担语言理解、视觉感知与动作控制功能，模型必须在多样化数据分布上进行训练，才能建立跨模态对齐与可执行决策能力。根据训练阶段的不同大致可以分为两个阶段。</span></p>


<p class=MsoNormal style='line-height:120%'><b><span lang=ZH-CN
style='font-family:SimSun'>（</span></b><b><span lang=EN-US style='font-family:
SimSun'>1</span></b><b><span lang=ZH-CN style='font-family:SimSun'>）语义预训练阶段为</span></b><b><span
lang=EN-US style='font-family:SimSun'>VLA</span></b><b><span lang=ZH-CN
style='font-family:SimSun'>提供通用世界理解能力</span></b></p>


<p class=MsoNormal style='line-height:120%'><span lang=EN-US style='font-family:
SimSun'>    </span><span lang=ZH-CN style='font-family:SimSun'>该阶段依托大规模互联网多模态数据进行预训练，包括图文对数据（如</span><span
lang=EN-US style='font-family:SimSun'>COCO</span><span lang=ZH-CN
style='font-family:SimSun'>、</span><span lang=EN-US style='font-family:SimSun'>LAION</span><span
lang=ZH-CN style='font-family:SimSun'>）、视频指令数据（如</span><span lang=EN-US
style='font-family:SimSun'>HowTo100M</span><span lang=ZH-CN style='font-family:
SimSun'>、</span><span lang=EN-US style='font-family:SimSun'>WebVid</span><span
lang=ZH-CN style='font-family:SimSun'>）以及视觉问答数据（如</span><span lang=EN-US
style='font-family:SimSun'>VQA</span><span lang=ZH-CN style='font-family:SimSun'>、</span><span
lang=EN-US style='font-family:SimSun'>GQA</span><span lang=ZH-CN
style='font-family:SimSun'>），用于构建跨模态语义先验。训练通常采用对比学习（如</span><span lang=EN-US
style='font-family:SimSun'>CLIP</span><span lang=ZH-CN style='font-family:SimSun'>）、掩码建模或语言建模目标，将视觉与语言编码到统一嵌入空间，使模型获得关于物体、动作与概念的通用表征能力。该阶段奠定了</span><span
lang=EN-US style='font-family:SimSun'>VLA</span><span lang=ZH-CN
style='font-family:SimSun'>的语义基础，提升了组合泛化、语义对齐与零样本迁移能力。该阶段通常以预训练视觉语言模型（</span><span
lang=EN-US style='font-family:SimSun'>VLM</span><span lang=ZH-CN
style='font-family:SimSun'>）作为骨架，例如，</span><span lang=EN-US style='font-family:
SimSun'>Google </span><span lang=ZH-CN style='font-family:SimSun'>开发的</span><span
lang=EN-US style='font-family:SimSun'> PaLM-E </span><span lang=ZH-CN
style='font-family:SimSun'>及其扩展模型</span><span lang=EN-US style='font-family:
SimSun'> PaLI-X </span><span lang=ZH-CN style='font-family:SimSun'>被用于</span><span
lang=EN-US style='font-family:SimSun'> RT-2 </span><span lang=ZH-CN
style='font-family:SimSun'>等</span><span lang=EN-US style='font-family:SimSun'>
VLA </span><span lang=ZH-CN style='font-family:SimSun'>系统；</span><span
lang=EN-US style='font-family:SimSun'>PaliGemma</span><span lang=ZH-CN
style='font-family:SimSun'>（</span><span lang=EN-US style='font-family:SimSun'>Gemma
+ SigLIP</span><span lang=ZH-CN style='font-family:SimSun'>）被应用于</span><span
lang=EN-US style='font-family:SimSun'> Physical Intelligence </span><span
lang=ZH-CN style='font-family:SimSun'>的 π</span><span lang=EN-US
style='font-family:SimSun'>0 </span><span lang=ZH-CN style='font-family:SimSun'>系列；</span><span
lang=EN-US style='font-family:SimSun'>PrismaticVLM</span><span lang=ZH-CN
style='font-family:SimSun'>（</span><span lang=EN-US style='font-family:SimSun'>LLaMA2
+ DINOv2 + SigLIP</span><span lang=ZH-CN style='font-family:SimSun'>）广泛用于</span><span
lang=EN-US style='font-family:SimSun'> OpenVLA </span><span lang=ZH-CN
style='font-family:SimSun'>和</span><span lang=EN-US style='font-family:SimSun'>
CogACT</span><span lang=ZH-CN style='font-family:SimSun'>；</span><span
lang=EN-US style='font-family:SimSun'>Qwen2.5-VL </span><span lang=ZH-CN
style='font-family:SimSun'>被用于</span><span lang=EN-US style='font-family:SimSun'>
NORA</span><span lang=ZH-CN style='font-family:SimSun'>、</span><span
lang=EN-US style='font-family:SimSun'>Interleave-VLA </span><span lang=ZH-CN
style='font-family:SimSun'>等模型；</span><span lang=EN-US style='font-family:SimSun'>LLaVA</span><span
lang=ZH-CN style='font-family:SimSun'>（</span><span lang=EN-US
style='font-family:SimSun'>Vicuna + CLIP</span><span lang=ZH-CN
style='font-family:SimSun'>）则被</span><span lang=EN-US style='font-family:SimSun'>
OpenHelix</span><span lang=ZH-CN style='font-family:SimSun'>、</span><span
lang=EN-US style='font-family:SimSun'>OE-VLA </span><span lang=ZH-CN
style='font-family:SimSun'>和</span><span lang=EN-US style='font-family:SimSun'>
RationalVLA </span><span lang=ZH-CN style='font-family:SimSun'>等系统采用。</span></p>


<p class=MsoNormal style='line-height:120%'><b><span lang=ZH-CN
style='font-family:SimSun'>（</span></b><b><span lang=EN-US style='font-family:
SimSun'>2</span></b><b><span lang=ZH-CN style='font-family:SimSun'>）具身任务学习后训练阶段负责将语义理解转化为可执行控制能力</span></b></p>


<p class=MsoNormal style='line-height:120%'><span lang=EN-US style='font-family:
SimSun'>    </span><span lang=ZH-CN style='font-family:SimSun'>后训练阶段引入真实或仿真机器人轨迹数据（如</span><span
lang=EN-US style='font-family:SimSun'>RoboNet</span><span lang=ZH-CN
style='font-family:SimSun'>、</span><span lang=EN-US style='font-family:SimSun'>BridgeData</span><span
lang=ZH-CN style='font-family:SimSun'>、</span><span lang=EN-US
style='font-family:SimSun'>RT-X</span><span lang=ZH-CN style='font-family:SimSun'>），通过监督学习（如行为克隆）、模仿学习或强化学习，将融合后的视觉</span><span
lang=EN-US style='font-family:SimSun'>—</span><span lang=ZH-CN
style='font-family:SimSun'>语言表示映射为动作序列，实现从感知到控制的闭环学习。主流训练策略通常采用多阶段流程：先进行视觉</span><span
lang=EN-US style='font-family:SimSun'>-</span><span lang=ZH-CN
style='font-family:SimSun'>语言预训练，再在机器人演示数据上进行自回归动作微调，部分方法结合课程学习（</span><span
lang=EN-US style='font-family:SimSun'>curriculum learning</span><span
lang=ZH-CN style='font-family:SimSun'>）、领域自适应或</span><span lang=EN-US
style='font-family:SimSun'>sim-to-real</span><span lang=ZH-CN style='font-family:
SimSun'>迁移以提升泛化能力。通过联合微调，模型能够对齐语义先验与任务执行数据，学习物体可供性与动作结果之间的因果关系，从而实现跨任务与跨场景迁移。以</span><span
lang=EN-US style='font-family:SimSun'>RT-2</span><span lang=ZH-CN
style='font-family:SimSun'>为代表的系统进一步将动作离散化为</span><span lang=EN-US
style='font-family:SimSun'>token</span><span lang=ZH-CN style='font-family:
SimSun'>并统一为文本生成问题，在互联网规模数据与机器人演示上联合训练，实现对新指令与新任务的零样本泛化，体现了</span><span
lang=EN-US style='font-family:SimSun'>VLA</span><span lang=ZH-CN
style='font-family:SimSun'>向可扩展具身智能体发展的关键路径。</span></p>


<p class=MsoNormal align=center style='text-align:center;line-height:120%'><span
lang=EN-US style='font-family:SimSun'><img width=360 height=200 id="图片 1"
src="./images/image006.png"></span></p>


<p class=MsoNormal align=center style='text-align:center;line-height:120%'><b><span
lang=ZH-CN style='font-family:SimSun'>训练范式：</span></b><b><span lang=EN-US
style='font-family:SimSun'>VLA</span></b><b><span lang=ZH-CN style='font-family:
SimSun'>的数据来源及训练策略（</span></b><span lang=EN-US><a
href="https://arxiv.org/abs/2505.04769v2"><b><span style='font-family:SimSun'>https://arxiv.org/abs/2505.04769v2</span></b></a></span><b><span
lang=ZH-CN style='font-family:SimSun'>）</span></b></p>


<p class=MsoNormal style='line-height:120%'><b><span lang=EN-US
style='font-family:SimSun'>3.2 </span></b><b><span lang=ZH-CN style='font-family:
SimSun'>训练范式与方法</span></b></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
text-indent:21.0pt;line-height:120%'><b><span lang=EN-US style='line-height:
120%;font-family:SimSun;color:black'>VLA</span></b><b><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>模型的训练方法可以归纳为三类核心范式：监督学习、自监督学习与强化学习，同时还有结合多种方法的混合范式，这些范式共同构成当前</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>VLA</span></b><b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>训练的基础框架。</span></b><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>下文将围绕各训练范式的核心特征与代表性方法进行概述。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>（</span></b><b><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>1</span></b><b><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>）监督学习（</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>Supervised
Learning</span></b><b><span lang=ZH-CN style='line-height:120%;font-family:
SimSun;color:black'>）</span></b></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
line-height:120%'><span lang=EN-US style='line-height:120%;font-family:SimSun;
color:black'>    </span><span lang=ZH-CN style='line-height:120%;font-family:
SimSun;color:black'>大多数</span><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>VLA</span><span lang=ZH-CN style='line-height:
120%;font-family:SimSun;color:black'>模型采用监督学习进行训练，基于图像—语言—动作三元组数据，将训练目标设定为“下一步动作预测”，形式上类似大语言模型的</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>token</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>生成。监督学习最常使用的方法是模仿学习（</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>Imitation
Learning</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>）。模仿学习（</span><span lang=EN-US style='line-height:120%;font-family:
SimSun;color:black'>Imitation Learning, IL</span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>）旨在通过专家示范轨迹学习一个策略，使其在未知奖励函数下的表现接近专家策略。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
text-indent:21.0pt;line-height:120%'><span lang=ZH-CN style='line-height:120%;
font-family:SimSun;color:black'>根据是否允许与环境或专家交互，模仿学习可分为离线（</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>offline</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）与在线（</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>online</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）两种范式。离线</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>IL</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>仅依赖预先收集的专家轨迹数据进行训练，不再与环境交互，结构简单、成本较低，因此成为</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>等大规模模型的主流方案。在线</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>IL</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>则允许模型在训练过程中与环境互动并查询专家，从而缓解分布偏移与误差累积问题，但在真实机器人系统中实现成本较高，因此应用相对有限。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
text-indent:21.0pt;line-height:120%'><span lang=ZH-CN style='line-height:120%;
font-family:SimSun;color:black'>行为克隆（</span><span lang=EN-US style='line-height:
120%;font-family:SimSun;color:black'>Behavior Cloning, BC</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）是最典型的离线</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>IL</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>方法，其核心是将序列决策问题转化为监督学习任务：输入状态，预测专家动作。通过最小化分类或回归损失，</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>BC</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>能够直接利用深度模型进行端到端训练，易于扩展到</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>Transformer</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>或多模态架构。尽管</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>BC</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>存在分布偏移与误差放大的风险，早期理论也指出其样本复杂度可能随时序长度呈二次增长，但最新分析表明，在合适损失函数与策略类约束下，离线</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>BC</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>可以获得更优的理论界限。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
text-indent:21.0pt;line-height:120%'><span lang=ZH-CN style='line-height:120%;
font-family:SimSun;color:black'>在</span><span lang=EN-US style='line-height:
120%;font-family:SimSun;color:black'>VLA</span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>系统中，模仿学习通常嵌入多阶段训练流程：预训练阶段利用大规模多模态或行为数据学习通用表示与跨模态对齐能力；后训练阶段通过监督学习在高质量任务数据上微调以适配具体场景；进一步，一些方法通过</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>in-context
learning</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>在测试时利用少量示例轨迹引导动作生成而无需额外更新参数。整体而言，这一流程仍以行为克隆为核心，通过不同阶段的数据与参数调节，实现从通用能力到场景化控制的逐步收敛。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>（</span></b><b><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>2</span></b><b><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>）自监督学习（</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>Self-Supervised
Learning</span></b><b><span lang=ZH-CN style='line-height:120%;font-family:
SimSun;color:black'>）</span></b></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
line-height:120%'><span lang=EN-US style='line-height:120%;font-family:SimSun;
color:black'>    </span><span lang=ZH-CN style='line-height:120%;font-family:
SimSun;color:black'>在</span><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>VLA</span><span lang=ZH-CN style='line-height:
120%;font-family:SimSun;color:black'>模型中，自监督学习主要承担三类功能。首先是跨模态对齐，通过对比学习等方法在共享潜在空间中对齐当前状态、未来状态以及语言目标，实现时间一致性与任务一致性对齐。其次是视觉表示学习，利用</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>MAE</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>、</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>CLIP</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>、</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>DINOv2</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>等自监督视觉编码器从图像或视频中提取高质量特征，这些预训练模型已成为</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>中的基础视觉骨干。第三是潜在动作表示学习，通过从初始图像与目标图像中提取</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>latent
action</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>，并利用该潜变量重构目标图像，在无需显式动作标签的情况下学习可泛化的动作嵌入。这种机制具有良好的可扩展性，尤其适用于大规模无标注数据场景。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>（</span></b><b><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>3</span></b><b><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>）强化学习（</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>Reinforcement
Learning, RL</span></b><b><span lang=ZH-CN style='line-height:120%;font-family:
SimSun;color:black'>）</span></b></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
line-height:120%'><span lang=EN-US style='line-height:120%;font-family:SimSun;
color:black'>    </span><span lang=ZH-CN style='line-height:120%;font-family:
SimSun;color:black'>强化学习（</span><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>RL</span><span lang=ZH-CN style='line-height:
120%;font-family:SimSun;color:black'>）在</span><span lang=EN-US
style='line-height:120%;font-family:SimSun;color:black'>VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>中的引入，核心目标是弥补纯模仿学习在分布外泛化与闭环控制能力上的不足，使模型能够在真实环境中基于奖励信号进行自我修正与策略优化。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
line-height:120%'><span lang=EN-US style='line-height:120%;font-family:SimSun;
color:black'>    </span><b><span lang=ZH-CN style='line-height:120%;font-family:
SimSun;color:black'>在结构层面</span></b><span lang=ZH-CN style='line-height:120%;
font-family:SimSun;color:black'>，</span><span lang=EN-US style='line-height:
120%;font-family:SimSun;color:black'>RL</span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>在</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>中的应用主要呈现两种典型模式。第一种是“</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>RL</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>强化</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>本体”，即直接对预训练</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>进行策略优化或微调，使其在真实环境奖励信号下获得更强的鲁棒性与闭环控制能力。这类方法通常结合示范数据与</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>RL</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>交替优化，以提升样本效率并避免灾难性遗忘，研究重点包括策略稳定性、样本效率、奖励建模与训练基础设施扩展等。第二种是“</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>作为大脑、</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>RL</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>作为身体”，即由</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>负责高层语义理解与任务决策，而由</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>RL</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>训练的低层控制策略负责动力学执行与精细控制。该分层结构能够在保持语义泛化能力的同时，保证物理层面的稳定性与实时性，是当前真实机器人系统中更具工程可行性的方案。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
text-indent:21.0pt;line-height:120%'><b><span lang=ZH-CN style='line-height:
120%;font-family:SimSun;color:black'>从数据使用方式来看</span></b><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>，</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>RL-VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>大体可分为三类：</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>Online
RL-VLA</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>（训练期间直接与环境交互）、</span><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>Offline RL-VLA</span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>（基于静态数据进行价值优化）以及</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>Test-time
RL-VLA</span><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>（部署阶段进行轻量级行为适配）。三者在交互成本与适应能力之间形成递进关系，共同构成当前</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>RL-VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>的技术谱系。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
text-indent:21.0pt;line-height:120%'><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>Online RL-VLA </span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>支持交互式策略学习，智能体通过持续与环境交互收集轨迹，并根据奖励和状态转移不断更新策略，使预训练</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> VLA </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>获得自适应的闭环控制能力，从而更好地适应真实世界的分布外（</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>OOD</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）环境。现有研究主要围绕策略优化、样本效率、主动探索和训练稳定性展开：策略优化多采用</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> PPO </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>及其变体（如</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> FLaRe</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>、</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>RLRC</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>、</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>GRPO</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>），实证结果表明</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> RL </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>微调相较</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> SFT </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>能显著提升</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> OOD </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>泛化能力；样本效率方面通过结合专家演示（如</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> RLDG</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）或</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>
Actor-Critic </span><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>结构（如</span><span lang=EN-US style='line-height:120%;font-family:
SimSun;color:black'> VLAC</span><span lang=ZH-CN style='line-height:120%;
font-family:SimSun;color:black'>）提供更密集信号；主动探索通过规划或数据生成提升探索质量，例如</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>
Plan-Seq-Learn </span><span lang=ZH-CN style='line-height:120%;font-family:
SimSun;color:black'>利用</span><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'> LLM </span><span lang=ZH-CN style='line-height:
120%;font-family:SimSun;color:black'>生成高层任务规划，</span><span lang=EN-US
style='line-height:120%;font-family:SimSun;color:black'>RESample </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>构造具有挑战性的</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> OOD </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>数据；在训练稳定性上，一些方法采用动态推演采样（</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>RIPT-VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）或利用世界模型生成合成轨迹（</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>World-Env</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）以降低交互方差。然而，</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>Online
RL-VLA </span><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>仍面临非平稳动力学与多模态噪声带来的训练稳定性挑战。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
text-indent:21.0pt;line-height:120%'><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>Offline RL-VLA </span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>在静态数据集上进行策略优化，适用于高风险或资源受限场景，但其性能高度依赖数据覆盖度与奖励信息质量。典型案例是采用离线训练的</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> π</span><span
lang=EN-US style='line-height:120%;font-family:"Cambria Math",serif;color:black'>∗</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>0.6</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>，其</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> RECAP </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>方法通过三步实现策略优化：首先在数据采集阶段结合机器人自主执行与人类专家纠正获取反馈数据；随后训练价值函数以预测任务剩余步数并计算动作优势；最后通过优势条件策略更新模型。总体而言，</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>Offline
RL-VLA </span><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>的研究主要集中在数据利用与目标函数设计两方面：前者通过保守约束（如</span><span lang=EN-US
style='line-height:120%;font-family:SimSun;color:black'> CO-RFT</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>、</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>ConRFT </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>中的</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> Cal-QL</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）避免策略偏离数据分布，并通过轨迹重塑或奖励生成（如</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> ReinboT</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）提升策略质量；后者则设计与模型结构匹配的优化目标（如</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> ARFM</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）或利用数据驱动目标生成高质量合成轨迹（如</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> RL-100</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）。然而，数据分布不均与奖励信号不完整仍是限制</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> Offline
RL-VLA </span><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>泛化能力的主要挑战。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
text-indent:21.0pt;line-height:120%'><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>Test-time RL-VLA</span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>则在不更新模型参数的前提下在推理阶段调整动作选择，实现低成本适配。常见方法包括：价值引导，利用预训练的奖励或价值函数影响动作选择（如</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> V-GPS </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>对动作候选进行重新排序，</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>Hume </span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>引入“价值引导思维”）；记忆缓冲引导，在推理阶段检索相关历史经验以提升探索效率与知识复用（如</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'> STRAP</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>、</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>ReSA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>）；以及规划引导适配，通过显式推理未来动作序列选择更优策略（如</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>
VLA-Reasoner </span><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>使用在线</span><span lang=EN-US style='line-height:120%;font-family:
SimSun;color:black'> MCTS</span><span lang=ZH-CN style='line-height:120%;
font-family:SimSun;color:black'>，</span><span lang=EN-US style='line-height:
120%;font-family:SimSun;color:black'>BGR </span><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>利用价值函数进行进度监控与错误纠正）。然而，这类方法在推理阶段需要评估大量动作候选或进行未来轨迹推演，带来了较高计算开销，从而限制了实时部署能力。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
line-height:120%'><span lang=EN-US style='line-height:120%;font-family:SimSun;
color:black'>    </span><span lang=ZH-CN style='line-height:120%;font-family:
SimSun;color:black'>当前</span><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>RL-VLA</span><span lang=ZH-CN style='line-height:
120%;font-family:SimSun;color:black'>已形成“预训练与模仿学习构建通用能力，</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>RL</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>提供任务级优化与环境适配”的协同框架。未来发展重点在于提升样本效率与训练稳定性，并结合世界模型或数字孪生环境进行低风险强化微调，从而实现大规模、可部署、具备真实泛化能力的</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>系统。</span></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
line-height:120%'><b><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>（</span></b><b><span lang=EN-US style='line-height:120%;
font-family:SimSun;color:black'>4</span></b><b><span lang=ZH-CN
style='line-height:120%;font-family:SimSun;color:black'>）混合范式与发展方向</span></b><b><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:#EE0000'> </span></b></p>


<p class=MsoNormal align=left style='margin-bottom:6.0pt;text-align:left;
text-indent:21.0pt;line-height:120%'><span lang=ZH-CN style='line-height:120%;
font-family:SimSun;color:black'>当前具身智能与</span><span lang=EN-US
style='line-height:120%;font-family:SimSun;color:black'>VLA</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>的训练已从单一范式演化为多策略融合的混合学习框架。监督学习（尤其是模仿学习）提供稳定的行为先验，自监督学习提升跨模态表示质量与数据利用效率，强化学习则通过奖励信号实现策略优化与分布外泛化。典型混合方案包括强化模仿学习（在模仿基础上引入奖励校正）、</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>VLM-based</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>协同训练（联合优化语义理解与控制策略）以及一致性约束方法（提升多模态与多阶段输出的稳定性）。整体趋势是整合模拟训练、模仿学习与强化学习优势，并通过</span><span
lang=EN-US style='line-height:120%;font-family:SimSun;color:black'>real-to-sim-to-real</span><span
lang=ZH-CN style='line-height:120%;font-family:SimSun;color:black'>迁移与数据重用技术提升训练效率，同时借助标准化基准体系推动系统性评估。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:21.0pt;
line-height:120%'><span lang=ZH-CN style='line-height:120%;font-family:SimSun;
color:black'>未来发展仍面临若干关键挑战。长时程任务需要引入结构化推理与记忆机制以保持轨迹一致性；样本效率问题推动基于模型的强化学习成为重要方向，通过世界模型生成更丰富的中间监督信号；真实机器人训练的高成本与安全风险要求多机器人共享训练与安全探索机制；此外，训练稳定性与可重复性亟需标准化流程支持。总体而言，未来具身智能将以“表示学习—模仿学习—强化优化”的协同框架为核心，在效率、稳定性与安全性之间实现更平衡的系统演进。</span></p>


<p class=MsoNormal style='line-height:120%'><span lang=EN-US>&nbsp;</span></p>

<p class=MsoNormal style='margin-top:8.0pt;margin-right:0cm;margin-bottom:4.0pt;
margin-left:0cm;line-height:120%;page-break-after:avoid'><b><span lang=ZH-CN
style='font-size:14.0pt;line-height:120%;font-family:SimSun'>四、 核心技术挑战：从</span></b><b><span
lang=EN-US style='font-size:14.0pt;line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='font-size:14.0pt;line-height:120%;font-family:SimSun'>实验室</span></b><b><span
lang=EN-US style='font-size:14.0pt;line-height:120%;font-family:SimSun'> Demo”</span></b><b><span
lang=ZH-CN style='font-size:14.0pt;line-height:120%;font-family:SimSun'>到</span></b><b><span
lang=EN-US style='font-size:14.0pt;line-height:120%;font-family:SimSun'>“</span></b><b><span
lang=ZH-CN style='font-size:14.0pt;line-height:120%;font-family:SimSun'>通用</span></b><b><span
lang=EN-US style='font-size:14.0pt;line-height:120%;font-family:SimSun'> AI”</span></b><b><span
lang=ZH-CN style='font-size:14.0pt;line-height:120%;font-family:SimSun'>的阻碍</span></b></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.0pt;
line-height:120%'><span lang=EN-US style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>VLA</span><span lang=ZH-CN style='font-size:
11.0pt;line-height:120%;font-family:SimSun;color:black'>模型正处于从特定场景迈向通用化的关键节点。然而，受限于泛化能力、工业级性能和评测体系的碎片化，当前技术仍面临多重瓶颈。</span></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>4.1 </span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>泛化能力的局限性：跨越分布边界的难题</span></b></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.0pt;
line-height:120%'><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>泛化能力是衡量模型是否具备通用性的核心标准。目前，</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>VLA </span><span lang=ZH-CN style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>模型在跨越既有训练数据分布时表现出明显脆弱性：</span></p>


<ul type=disc>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>跨任务泛化瓶颈</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>VLA</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>模型普遍高度依赖</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>&quot;</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>指令</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>-</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>动作</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>&quot;</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>数据对的统计拟合。早期模型受限于训练数据规模与任务多样性，在训练集之外的复杂逻辑任务上性能大幅下降；当前规模更大的模型（如</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>RT-2</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>、</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>OpenVLA</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>）虽借助预训练视觉语言模型提升了语义理解能力，但在需要多步推理、因果判断的任务场景中，仍难以稳定理解任务本质，泛化边界尚未被突破。</span></li>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>跨环境的</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>仿真</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>-</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>现实</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>鸿沟</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：虽然仿真平台提升了数据量，但在触觉交互（如物体滑移感知）和非刚体操作（如布料折叠）的物理还原度上，仍难以完全模拟真实世界的复杂性。此外，光照、材质等细微变量的变化易引发</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>环境分布偏移</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>，导致模型失效。</span></li>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>跨实体的控制难题</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：硬件异构性是实现</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>&quot;</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>一套算法适配多种硬件</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>&quot;</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>的最大障碍。不同机器人的关节空间与自由度差异巨大，归一化控制框架的构建长期缺乏突破。不过这一方向已出现积极进展</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>——Gemini
     Robotics</span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
     font-family:SimSun'>于</span><span lang=EN-US style='font-size:11.0pt;
     line-height:120%;font-family:SimSun'>2025</span><span lang=ZH-CN
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>年展示了跨本体泛化能力，首次在多类异构硬件上达到工业级操作标准，标志着通用控制框架的探索正从概念验证走向实质落地。</span></li>
</ul>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>4.2 </span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>工业级可靠性瓶颈：长时程、实时性与安全的制约</span></b></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.0pt;
line-height:120%'><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>工业级部署对机器人提出了长时程稳定性、实时响应和确定性安全的三重硬性要求，而这与当前</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'> VLA </span><span lang=ZH-CN style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>模型的底层逻辑存在冲突</span><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>&nbsp;</span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>：</span></p>


<ul type=disc>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>长时程任务的</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>复合误差深渊</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：在连续作业中，自回归推理模式下的局部微小误差会随步骤累积，产生策略漂移，导致长序列任务（如超过</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>
     50</span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
     font-family:SimSun'>步的任务）失败率显著上升。</span></li>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>推理延迟与实时控制的矛盾</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：大规模</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>
     VLA </span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
     font-family:SimSun'>模型的高计算负载导致推理延迟通常在</span><span lang=EN-US
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>100-300ms</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>之间。这难以满足工业控制所需的</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>50Hz</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>（每秒</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>50</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>次决策）以上的实时性需求，直接影响机器人的动态避障与反应速度。这一矛盾催生了<b>云端推理</b>与<b>端侧推理</b>两种路径的分歧：云端推理依托强算力可支撑更大参数规模的模型，但网络延迟与带宽波动引入了不可控的时延抖动，在断网或低延迟敏感场景下可靠性存疑；端侧推理将模型直接部署于机器人本体，可实现毫秒级响应并规避网络依赖，但受限于本体算力与功耗约束，模型规模与推理能力难以兼顾。目前业界的主流探索方向集中于</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>&quot;</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>云端大脑</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>+</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>端侧小脑</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>&quot;</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>的层级协同架构</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>——</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>以云端模型负责高层语义规划，端侧轻量模型承接低层实时控制，以此在性能与延迟之间寻求平衡。</span></li>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>概率模型与</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>零容忍</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>安全的冲突</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>VLA
     </span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
     font-family:SimSun'>模型本质上是概率模型，其输出具有不可完全预测性。在医疗或精密制造等严苛场景下，缺乏刚性的安全边界约束，难以通过数学方法和在真机操作中证明系统在极端情况下的安全性。</span></li>
</ul>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>4.3 </span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>评价体系：碎片化与非标化挑战</span></b></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.0pt;
line-height:120%'><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>评测标准的缺失是具身智能领域目前面临的主要非技术障碍</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>——</span><span lang=ZH-CN style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>准确地说，问题并非</span><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>&quot;</span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>无标准可依</span><span lang=EN-US style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>&quot;</span><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>，而是现有基准高度碎片化，且正在滋生一系列系统性失真。目前学界已有若干代表性评测基准：任务操作类有</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'> RLBench</span><span lang=ZH-CN style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>、</span><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>MetaWorld</span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>、</span><span lang=EN-US style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>LIBERO</span><span lang=ZH-CN style='font-size:
11.0pt;line-height:120%;font-family:SimSun;color:black'>，侧重桌面抓取与多步操作；导航与场景理解类有</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'> Habitat</span><span lang=ZH-CN style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>、</span><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>AI2-THOR</span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>、</span><span lang=EN-US style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>BEHAVIOR-1K</span><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>；全身</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>/</span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>移动操作类有</span><span lang=EN-US style='font-size:
11.0pt;line-height:120%;font-family:SimSun;color:black'> Open X-Embodiment</span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>（汇聚多实验室跨平台数据集）；语言指令跟随类有</span><span lang=EN-US style='font-size:
11.0pt;line-height:120%;font-family:SimSun;color:black'> ALFRED</span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>、</span><span lang=EN-US style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>CALVIN</span><span lang=ZH-CN style='font-size:
11.0pt;line-height:120%;font-family:SimSun;color:black'>。然而，这些基准普遍建立在仿真环境或特定硬件平台之上，彼此之间缺乏统一的任务定义、评分协议与硬件接口，实验室之间的横向对比实际上并不成立。具体体现在：</span></p>


<ul type=disc>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>硬件异构与环境非标化</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：不同实验室的执行器、传感器及场景配置各异，导致所谓的</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>
     SOTA</span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
     font-family:SimSun'>性能难以进行横向对标。物理世界的不可标准化使得在计算机视觉领域通用的</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“ImageNet</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>式</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>评测范式难以在具身智能中复现。</span></li>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>评价指标的错位</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：传统的</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>单次成功率</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>指标难以反映机器人的真实商业价值。在工业界，衡量连续自主作业能力的指标（如接管率或平均干预间隔
     </span><b><span lang=EN-US style='font-size:11.0pt;line-height:120%;
     font-family:SimSun'>MPI<sup>*</sup></span></b><span lang=ZH-CN
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>）尚未形成统一的国际标准，导致技术评估与产业需求之间存在断层。</span></li>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>基准污染与</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>&quot;</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>高分低能</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>&quot;</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>困境：</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>部分模型直接或间接地在评测数据集上进行训练或调优，导致基准分数虚高，却在真实场景中表现平平。此外，研究者倾向于选择对自身模型有利的子任务进行汇报，回避困难场景；评测环境的仿真参数也可能被针对性地调校以提升成绩。</span></li>
</ul>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><i><span
lang=ZH-CN style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>注释：</span></i><i><span lang=EN-US style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>MPI </span></i><i><span
lang=ZH-CN style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>意为平均干预间隔。在长程任务（如打扫一整个房间）中，模型可能会拆分成多个子任务段（</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>Partitions</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>）。</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>MPI </span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>衡量的是：机器人平均能自主完成多少个子任务段才需要人类伸手</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>帮一把</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>”</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>。</span></i></p>


<h2 style='line-height:120%'><b><span lang=ZH-CN style='font-size:14.0pt;
line-height:120%;font-family:SimSun;color:windowtext'>五、 应对路径与发展趋势：迈向工业级具身智能</span></b></h2>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>针对前文提到的三大挑战，</span><span lang=EN-US style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>2026 </span><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>年的技术路径已展现出清晰的进化趋势。</span></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>5.1 </span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>泛化瓶颈的破局：从</span></b><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>黑盒拟合</span></b><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>”</span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>到</span></b><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>结构化理解</span></b><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>”</span></b></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>泛化的本质是模型在</span><b><span lang=ZH-CN style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>未见分布（</span></b><b><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>OOD</span></b><b><span lang=ZH-CN style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>）</span></b><b><sup><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>1</span></sup></b><span lang=ZH-CN style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>下的鲁棒性</span><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>。目前，行业正从三个逻辑维度进行突破：</span></p>


<ul type=disc>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>组合性泛化（</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>Compositional
     Generalization</span></b><b><span lang=ZH-CN style='font-size:11.0pt;
     line-height:120%;font-family:SimSun'>）</span></b><span lang=ZH-CN
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：为了解决跨任务难题，研究者不再试图让模型</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>死记硬背</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>海量指令。<b>核心路径是将复杂任务解构为</b></span><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>原子技能库</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>（如抓取、旋转、放置）。通过构建结构化的技能表示，模型可以像搭积木一样，通过逻辑组合完成从未见过的复合长程任务。</span></li>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>物理直觉与世界模型（</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>World
     Models</span></b><b><span lang=ZH-CN style='font-size:11.0pt;line-height:
     120%;font-family:SimSun'>）</span></b><span lang=ZH-CN style='font-size:
     11.0pt;line-height:120%;font-family:SimSun'>：跨环境泛化的核心在于让机器人拥有</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>物理常识</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>。通过引入</span><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
     color:black'>GigaWorld<sup>2</sup></span></b><span lang=ZH-CN
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>等生成式世界模型，机器人可以在执行动作前，在潜空间内</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>预演</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>动作后果。这种</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>心理模拟</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>能力使机器人能感知摩擦力、重力等隐性物理变量，从而跨越</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>
     Sim-to-Real</span><span lang=ZH-CN style='font-size:11.0pt;line-height:
     120%;font-family:SimSun'>（仿真到现实）的鸿沟。</span></li>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>动作空间归一化（</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>Action
     Space Normalization</span></b><b><span lang=ZH-CN style='font-size:11.0pt;
     line-height:120%;font-family:SimSun'>）</span></b><span lang=ZH-CN
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：针对异构硬件（不同自由度、不同品牌的机械臂），目前的趋势是建立<b>统一的动作描述协议</b>。通过</span><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
     color:black'>形态描述符（</span></b><b><span lang=EN-US style='font-size:11.0pt;
     line-height:120%;font-family:SimSun;color:black'>Morphology Descriptors</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
     color:black'>）</span></b><b><sup><span lang=EN-US style='font-size:11.0pt;
     line-height:120%;font-family:SimSun;color:black'>3</span></sup></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>，模型能将不同实体的关节指令映射到统一的数学空间，实现</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>一套算法，多机协同</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>。</span></li>
</ul>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><i><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>注释：</span></i></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>1</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>、未见分布（</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>Out-of-Distribution </span></i><i><span lang=ZH-CN
style='font-size:10.0pt;line-height:120%;font-family:SimSun;color:black'>，</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>OOD</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>）：机器学习传统上假设训练数据和测试数据是独立同分布（</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>IID</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>）的。但在真实物理世界中，光照、物体材质、甚至背景的微小变动都会导致数据偏离训练集的统计分布，这就是</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'> OOD</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>。</span></i></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>2</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>、</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>GigaWorld</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>（生成式世界模型）：如果说</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'> VLA </span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>是机器人的</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>小脑</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>”</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>（负责动作控制），那么</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>GigaWorld</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>这种世界模型就是机器人的</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>大脑联想区</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>”</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>。它是一个预测性生成模型。给定当前的视觉状态</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'> s<sub>t</sub></span></i><i><span lang=ZH-CN style='font-size:
10.0pt;line-height:120%;font-family:SimSun;color:black'>和动作</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'> a<sub>t</sub></span></i><i><span lang=ZH-CN style='font-size:
10.0pt;line-height:120%;font-family:SimSun;color:black'>，它能预测下一时刻的视觉状态</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'> s<sub>t+1</sub></span></i><i><span lang=ZH-CN style='font-size:
10.0pt;line-height:120%;font-family:SimSun;color:black'>。这为机器人提供了一个</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>内部仿真器</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>”</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>，让它在动作执行前进行想象（</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>Dreaming</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>），通过预演动作后果来规避风险。</span></i></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>3. </span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>形态描述符（</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>Morphology Descriptors</span></i><i><span lang=ZH-CN
style='font-size:10.0pt;line-height:120%;font-family:SimSun;color:black'>）：如何让一套算法既能控制小米的</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'> CyberDog</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>，又能控制宇树的人形机器人？形态描述符是将机器人的硬件参数（如自由度、连杆长度、关节限位）编码为模型可理解的特征向量。它将</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>硬件差异</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>”</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>转化为了</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>输入特征</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>”</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>，使模型能够学习到超越特定硬件的通用运动学先验。这类似于</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'> NLP </span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>中的嵌入（</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>Embedding</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>），只不过它嵌入的是机器人的身体结构。</span></i></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><a
name="OLE_LINK3"><b><span lang=EN-US style='font-size:12.0pt;line-height:120%;
font-family:SimSun;color:black'>5.2 </span></b></a><b><span lang=ZH-CN
style='font-size:12.0pt;line-height:120%;font-family:SimSun;color:black'>性能瓶颈的优化：双系统架构与时延控制</span></b></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.0pt;
line-height:120%'><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>工业场景对实时性和确定性的要求，迫使</span><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'> VLA </span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>模型借鉴人类大脑的</span><span lang=EN-US style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>“</span><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>双系统</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>”</span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>工作模式：</span></p>


<ul type=disc>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>类人双系统架构（</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>System
     1 &amp; 2</span></b><b><span lang=ZH-CN style='font-size:11.0pt;
     line-height:120%;font-family:SimSun'>）</span></b><span lang=ZH-CN
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：该架构的概念根源可追溯至</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>
     Kahneman </span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
     font-family:SimSun'>的“快思慢想”认知框架，并已在多个代表性工作中被显式采用。</span><span lang=EN-US
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>NVIDIA</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>于</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>2025</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>年发布的</span><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>GR00T
     N1</span></b><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
     font-family:SimSun'>是目前最具代表性的落地实现，其架构明确区分了慢速思考模块（</span><span lang=EN-US
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>System 2</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>，负责多模态推理与长程规划）与快速响应模块（</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>System
     1</span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
     font-family:SimSun'>，负责高频底层控制）；</span><b><span lang=EN-US
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>π0</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>同样采用了类似的层级解耦设计。</span></li>
</ul>


<p class=MsoNormal align=left style='margin-left:72.0pt;text-align:left;
line-height:120%'><b><span lang=EN-US style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>System 1</span></b><b><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>（反应层）</span></b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>：负责高频（</span><span lang=EN-US style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>50Hz-200Hz</span><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>）的底层控制，如避障、动态平衡，类似于人类的</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>条件反射</span><span lang=EN-US style='font-size:
11.0pt;line-height:120%;font-family:SimSun;color:black'>”</span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>。</span></p>


<p class=MsoNormal align=left style='margin-left:72.0pt;text-align:left;
line-height:120%'><b><span lang=EN-US style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>System 2</span></b><b><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>（认知层）</span></b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>：负责低频（</span><span lang=EN-US style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>1Hz-5Hz</span><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>）的高级决策和长程规划，类似于人类的</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>理性思考</span><span lang=EN-US style='font-size:
11.0pt;line-height:120%;font-family:SimSun;color:black'>”</span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>。这种解耦架构解决了大模型推理慢（时延高）与机器人控制快（实时性强）之间的矛盾。</span></p>


<ul type=disc>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>动作分块（</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>Action
     Chunking</span></b><b><span lang=ZH-CN style='font-size:11.0pt;line-height:
     120%;font-family:SimSun'>）与时延压缩</span></b><span lang=ZH-CN
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>： 为了缓解自回归预测带来的累积误差，技术上采用了</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>动作分块</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>方案，即一次性预测未来一段时间内的动作序列。配合</span><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>π-FAST<sup>*</sup></span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>等频域压缩算法，极大地降低了</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>
     Token</span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
     font-family:SimSun'>推理的计算量，使端到端控制达到工业级的实时响应标准。</span></li>
</ul>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><i><span
lang=ZH-CN style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>注释：</span></i><i><span lang=EN-US style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>π-FAST</span></i><i><span
lang=ZH-CN style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>（动作令牌压缩）：大模型推理太慢（低频），而机器人控制要求太快（高频），这是一个物理矛盾。</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>π-FAST </span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>的核心在于频域压缩。它利用离散余弦变换（</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>DCT</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>）将连续的动作轨迹从时域转为频域，只保留对动作贡献最大的低频分量。这样可以用极少的</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'> Token </span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>代表复杂的动作序列，从而在不损失精度的前提下，将推理频率从几赫兹提升到工业级的</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'> 50Hz </span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>以上。</span></i></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>5.3 </span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>评价体系的重构：从</span></b><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>实验成功率</span></b><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>”</span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>到</span></b><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>“</span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>商用接管率</span></b><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>”</span></b></p>


<ul type=disc>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>MPI</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>（平均干预间隔）成为金标准</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：在学术界，我们常看</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“Success
     Rate”</span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
     font-family:SimSun'>；但在工业界，</span><b><span lang=EN-US style='font-size:
     11.0pt;line-height:120%;font-family:SimSun'>MPI</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>（</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>Mean
     Partitions per Intervention</span></b><b><span lang=ZH-CN
     style='font-size:11.0pt;line-height:120%;font-family:SimSun'>）</span></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>才是核心。它衡量机器人在连续作业中能独立运行多久。</span></li>
 <li class=MsoNormal style='color:black;text-align:left;line-height:120%'><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>WoW</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>（</span></b><b><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>World-on-Wheels</span></b><b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>）闭环评测</span></b><b><sup><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>*</span></sup></b><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>：新一代评测基准不再是静态的任务测试，而是强调在<b>强干扰、动态环境</b>下的鲁棒性。这意味着评价标准正从</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>能不能做</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>转向</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>“</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>做得多稳</span><span
     lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun'>”</span><span
     lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun'>。</span></li>
</ul>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><i><span
lang=ZH-CN style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>注释：</span></i><i><span lang=EN-US style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>WoW (World-on-Wheels) </span></i><i><span
lang=ZH-CN style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>闭环评测：</span></i><i><span lang=EN-US style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>WoW </span></i><i><span
lang=ZH-CN style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>是</span></i><i><span lang=EN-US style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'> 2026 </span></i><i><span
lang=ZH-CN style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>年最具代表性的评测协议。它强调交互性：评测不再是给机器人一张静止的照片，而是在动态变化的真实</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>/</span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>仿真环境（</span></i><i><span
lang=EN-US style='font-size:10.0pt;line-height:120%;font-family:SimSun;
color:black'>Wheels </span></i><i><span lang=ZH-CN style='font-size:10.0pt;
line-height:120%;font-family:SimSun;color:black'>隐喻移动和动态）中，观察机器人面对突发干扰（比如人突然踢走球）时的即时反应能力。它评估的是模型在连续时间序列中的纠错能力。</span></i></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><a
name="OLE_LINK2"><b><span lang=EN-US style='font-size:12.0pt;line-height:120%;
font-family:SimSun;color:black'>5.4 </span></b></a><b><span lang=ZH-CN
style='font-size:12.0pt;line-height:120%;font-family:SimSun;color:black'>代表性模型与技术路线：核心玩家的战略选择</span></b></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>以下七个案例对应四条主要路线，技术选择背后是不同的资源禀赋与商业逻辑：</span></p>


<table class=MsoNormalTable border=1 cellspacing=0 cellpadding=0 width=539
 style='width:403.95pt;border-collapse:collapse;border:none'>
 <thead>
  <tr>
   <td width=140 style='width:105.0pt;border:solid #C8D4E0 1.0pt;background:
   #1A3A5C;padding:5.5pt 6.5pt 5.5pt 6.5pt'>
   <p class=MsoNormal align=center style='margin-top:1.5pt;margin-right:0cm;
   margin-bottom:1.5pt;margin-left:0cm;text-align:center;line-height:120%'><b><span
   lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
   color:white'>模型</span></b><b><span lang=EN-US style='font-size:9.0pt;
   line-height:120%;font-family:SimSun;color:white'> / </span></b><b><span
   lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
   color:white'>机构</span></b></p>
   </td>
   <td width=219 style='width:164.3pt;border:solid #C8D4E0 1.0pt;border-left:
   none;background:#1A3A5C;padding:5.5pt 6.5pt 5.5pt 6.5pt'>
   <p class=MsoNormal align=center style='margin-top:1.5pt;margin-right:0cm;
   margin-bottom:1.5pt;margin-left:0cm;text-align:center;line-height:120%'><b><span
   lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
   color:white'>核心优势</span></b></p>
   </td>
   <td width=104 style='width:77.95pt;border:solid #C8D4E0 1.0pt;border-left:
   none;background:#1A3A5C;padding:5.5pt 6.5pt 5.5pt 6.5pt'>
   <p class=MsoNormal align=center style='margin-top:1.5pt;margin-right:0cm;
   margin-bottom:1.5pt;margin-left:0cm;text-align:center;line-height:120%'><b><span
   lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
   color:white'>典型应用</span></b></p>
   </td>
   <td width=76 style='width:2.0cm;border:solid #C8D4E0 1.0pt;border-left:none;
   background:#1A3A5C;padding:5.5pt 6.5pt 5.5pt 6.5pt'>
   <p class=MsoNormal align=center style='margin-top:1.5pt;margin-right:0cm;
   margin-bottom:1.5pt;margin-left:0cm;text-align:center;line-height:120%'><b><span
   lang=ZH-CN style='font-size:9.0pt;line-height:120%;font-family:SimSun;
   color:white'>开源状态</span></b></p>
   </td>
  </tr>
 </thead>
 <tr>
  <td width=140 valign=top style='width:105.0pt;border:solid #C8D4E0 1.0pt;
  border-top:none;background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  9.0pt;line-height:120%;font-family:SimSun;color:#1A3A5C'>OpenVLA</span></b></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=EN-US style='font-size:
  7.5pt;line-height:120%;font-family:SimSun;color:#555555'>Stanford / UCB /
  Toyota</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  6.5pt;line-height:120%;font-family:SimSun;color:#888888'>开源基准模型</span></p>
  </td>
  <td width=219 valign=top style='width:164.3pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>7B</span><span lang=ZH-CN style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>参数，超</span><span lang=EN-US
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>RT-2-X</span><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>成功率</span><span lang=EN-US style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'> 16.5%</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>LoRA</span><span lang=ZH-CN style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>微调成本降低</span><span lang=EN-US
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'> 8 </span><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>倍</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>4-bit</span><span lang=ZH-CN style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>量化，</span><span lang=EN-US
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>8GB</span><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>显存即可运行</span></p>
  </td>
  <td width=104 valign=top style='width:77.95pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>学术基准</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>多任务操作</span></p>
  </td>
  <td width=76 valign=top style='width:2.0cm;border-top:none;border-left:none;
  border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:"Segoe UI Symbol",sans-serif;color:#1B6B2F'>✓</span></b><b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:#1B6B2F'> </span></b><b><span lang=ZH-CN style='font-size:8.0pt;
  line-height:120%;font-family:SimSun;color:#1B6B2F'>完全开源</span></b></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#555555'>（代码</span><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:#555555'>+</span><span lang=ZH-CN style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:#555555'>权重）</span></p>
  </td>
 </tr>
 <tr>
  <td width=140 valign=top style='width:105.0pt;border:solid #C8D4E0 1.0pt;
  border-top:none;background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  9.0pt;line-height:120%;font-family:SimSun;color:#1A3A5C'>π0</span></b></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=EN-US style='font-size:
  7.5pt;line-height:120%;font-family:SimSun;color:#555555'>Physical
  Intelligence</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  6.5pt;line-height:120%;font-family:SimSun;color:#888888'>端到端通用</span><span
  lang=EN-US style='font-size:6.5pt;line-height:120%;font-family:SimSun;
  color:#888888'>VLA</span></p>
  </td>
  <td width=219 valign=top style='width:164.3pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>Flow Matching</span><span lang=ZH-CN style='font-size:8.0pt;
  line-height:120%;font-family:SimSun;color:black'>，</span><span lang=EN-US
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>50Hz</span><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>连续控制</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>长程任务能力强（叠衣、冲咖啡）</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>零样本泛化优异</span></p>
  </td>
  <td width=104 valign=top style='width:77.95pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>家庭服务</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>精细操作</span></p>
  </td>
  <td width=76 valign=top style='width:2.0cm;border-top:none;border-left:none;
  border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:"Segoe UI Symbol",sans-serif;color:#1B6B2F'>✓</span></b><b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:#1B6B2F'> </span></b><b><span lang=ZH-CN style='font-size:8.0pt;
  line-height:120%;font-family:SimSun;color:#1B6B2F'>权重开源</span></b></p>
  </td>
 </tr>
 <tr>
  <td width=140 valign=top style='width:105.0pt;border:solid #C8D4E0 1.0pt;
  border-top:none;background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  9.0pt;line-height:120%;font-family:SimSun;color:#1A3A5C'>GR00T N1</span></b></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=EN-US style='font-size:
  7.5pt;line-height:120%;font-family:SimSun;color:#555555'>NVIDIA</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  6.5pt;line-height:120%;font-family:SimSun;color:#888888'>混合架构平台</span></p>
  </td>
  <td width=219 valign=top style='width:164.3pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>VLA + Diffusion + </span><span lang=ZH-CN style='font-size:8.0pt;
  line-height:120%;font-family:SimSun;color:black'>双系统混合架构</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>50Hz</span><span lang=ZH-CN style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>高频控制，约</span><span lang=EN-US
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>50 episodes</span><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>微调</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>Jetson Thor </span><span lang=ZH-CN style='font-size:8.0pt;
  line-height:120%;font-family:SimSun;color:black'>软硬一体优化</span></p>
  </td>
  <td width=104 valign=top style='width:77.95pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>工业制造</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>物流仓储</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>人形机器人</span></p>
  </td>
  <td width=76 valign=top style='width:2.0cm;border-top:none;border-left:none;
  border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:"Segoe UI Symbol",sans-serif;color:#1B6B2F'>✓</span></b><b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:#1B6B2F'> HuggingFace</span></b></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#555555'>开源</span></p>
  </td>
 </tr>
 <tr>
  <td width=140 valign=top style='width:105.0pt;border:solid #C8D4E0 1.0pt;
  border-top:none;background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  9.0pt;line-height:120%;font-family:SimSun;color:#1A3A5C'>Helix</span></b></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=EN-US style='font-size:
  7.5pt;line-height:120%;font-family:SimSun;color:#555555'>Figure AI</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  6.5pt;line-height:120%;font-family:SimSun;color:#888888'>双系统商业部署</span></p>
  </td>
  <td width=219 valign=top style='width:164.3pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>System 1</span><span lang=ZH-CN style='font-size:8.0pt;
  line-height:120%;font-family:SimSun;color:black'>（</span><span lang=EN-US
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>200Hz</span><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>反应）</span><span lang=EN-US style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>+ System 2</span><span lang=ZH-CN
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>（语义规划）</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>全身协同控制，已量产工厂部署</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>VLA</span><span lang=ZH-CN style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>最早规模化落地案例之一</span></p>
  </td>
  <td width=104 valign=top style='width:77.95pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>工厂自动化</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>人形机器人</span></p>
  </td>
  <td width=76 valign=top style='width:2.0cm;border-top:none;border-left:none;
  border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:"Segoe UI Symbol",sans-serif;color:#8B1A1A'>✗</span></b><b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:#8B1A1A'> </span></b><b><span lang=ZH-CN style='font-size:8.0pt;
  line-height:120%;font-family:SimSun;color:#8B1A1A'>闭源</span></b></p>
  </td>
 </tr>
 <tr>
  <td width=140 valign=top style='width:105.0pt;border:solid #C8D4E0 1.0pt;
  border-top:none;background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  9.0pt;line-height:120%;font-family:SimSun;color:#1A3A5C'>GigaBrain-0.5M</span></b></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  7.5pt;line-height:120%;font-family:SimSun;color:#555555'>极佳视界（中科第五纪）</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  6.5pt;line-height:120%;font-family:SimSun;color:#888888'>闭环训练范式</span></p>
  </td>
  <td width=219 valign=top style='width:164.3pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>四阶段</span><span lang=EN-US style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>RLWM</span><span lang=ZH-CN
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>闭环训练</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>长时程任务成功率接近</span><span lang=EN-US style='font-size:8.0pt;
  line-height:120%;font-family:SimSun;color:black'> 100%</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>较</span><span lang=EN-US style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>RECAP</span><span lang=ZH-CN
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>基线提升</span><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'> 30%+</span></p>
  </td>
  <td width=104 valign=top style='width:77.95pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>复杂装配</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>长时程任务</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>自主进化场景</span></p>
  </td>
  <td width=76 valign=top style='width:2.0cm;border-top:none;border-left:none;
  border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#7A5A00'>△</span></b><b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:#7A5A00'> </span></b><b><span lang=ZH-CN style='font-size:8.0pt;
  line-height:120%;font-family:SimSun;color:#7A5A00'>部分开源</span></b></p>
  </td>
 </tr>
 <tr>
  <td width=140 valign=top style='width:105.0pt;border:solid #C8D4E0 1.0pt;
  border-top:none;background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  9.0pt;line-height:120%;font-family:SimSun;color:#1A3A5C'>Spirit v1.5</span></b></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  7.5pt;line-height:120%;font-family:SimSun;color:#555555'>千寻智能</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  6.5pt;line-height:120%;font-family:SimSun;color:#888888'>国产开源标杆</span></p>
  </td>
  <td width=219 valign=top style='width:164.3pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>首个性能超越</span><span lang=EN-US style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>π0.5</span><span lang=ZH-CN
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>的国产开源模型</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>零样本泛化能力强</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>京东零售场景实际部署验证</span></p>
  </td>
  <td width=104 valign=top style='width:77.95pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>零售导购</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>仓储分拣</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>商业服务</span></p>
  </td>
  <td width=76 valign=top style='width:2.0cm;border-top:none;border-left:none;
  border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:#EEF3F8;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:"Segoe UI Symbol",sans-serif;color:#1B6B2F'>✓</span></b><b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:#1B6B2F'> </span></b><b><span lang=ZH-CN style='font-size:8.0pt;
  line-height:120%;font-family:SimSun;color:#1B6B2F'>开源</span></b></p>
  </td>
 </tr>
 <tr>
  <td width=140 valign=top style='width:105.0pt;border:solid #C8D4E0 1.0pt;
  border-top:none;background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  9.0pt;line-height:120%;font-family:SimSun;color:#1A3A5C'>Unitree G1</span></b></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  7.5pt;line-height:120%;font-family:SimSun;color:#555555'>宇树科技</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  6.5pt;line-height:120%;font-family:SimSun;color:#888888'>最广泛部署本体</span></p>
  </td>
  <td width=219 valign=top style='width:164.3pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>全球出货量领先的人形机器人本体</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>原生兼容主流</span><span lang=EN-US style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>VLA</span><span lang=ZH-CN
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>框架（</span><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>GR00T</span><span lang=ZH-CN style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>、</span><span lang=EN-US
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>OpenVLA</span><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>等）</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:#2E5F8C'>• </span></b><span
  lang=ZH-CN style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:black'>开放</span><span lang=EN-US style='font-size:8.0pt;line-height:
  120%;font-family:SimSun;color:black'>SDK</span><span lang=ZH-CN
  style='font-size:8.0pt;line-height:120%;font-family:SimSun;color:black'>生态，学术与产业广泛采用</span></p>
  </td>
  <td width=104 valign=top style='width:77.95pt;border-top:none;border-left:
  none;border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>科研平台</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>工业巡检</span></p>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><span lang=ZH-CN style='font-size:
  8.0pt;line-height:120%;font-family:SimSun;color:black'>具身智能研发</span></p>
  </td>
  <td width=76 valign=top style='width:2.0cm;border-top:none;border-left:none;
  border-bottom:solid #C8D4E0 1.0pt;border-right:solid #C8D4E0 1.0pt;
  background:white;padding:5.0pt 6.5pt 5.0pt 6.5pt'>
  <p class=MsoNormal style='margin-top:1.5pt;margin-right:0cm;margin-bottom:
  1.5pt;margin-left:0cm;line-height:120%'><b><span lang=EN-US style='font-size:
  8.0pt;line-height:120%;font-family:"Segoe UI Symbol",sans-serif;color:#1B6B2F'>✓</span></b><b><span
  lang=EN-US style='font-size:8.0pt;line-height:120%;font-family:SimSun;
  color:#1B6B2F'> SDK</span></b><b><span lang=ZH-CN style='font-size:8.0pt;
  line-height:120%;font-family:SimSun;color:#1B6B2F'>开源</span></b></p>
  </td>
 </tr>
</table>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.1pt;
line-height:120%'><b><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>端到端派（</span></b><b><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>OpenVLA</span></b><b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>、</span></b><b><span lang=EN-US style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>π0</span></b><b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>）</span></b><span lang=ZH-CN style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>：系统简洁、通用任务覆盖广，适合以能力边界探索为目标的机构。代价是调试困难、数据与算力门槛高，难以在特定工业场景快速落地。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.1pt;
line-height:120%'><b><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>混合派（</span></b><b><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>GR00T
N1</span></b><b><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>、</span></b><b><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>GigaBrain-0.5M</span></b><b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>）</span></b><span lang=ZH-CN style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>：性能与工程成本之间取得平衡，是当前工业部署的主流选择。模块化设计也让这条路线对合作伙伴更友好，生态扩展阻力小。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.1pt;
line-height:120%'><b><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>垂直整合派（</span></b><b><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>Helix
/ Figure AI</span></b><b><span lang=ZH-CN style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>）</span></b><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>：全栈自研带来最强的数据飞轮与软硬协同优势，壁垒极高。但同等量级的资本投入和长期承诺，使这条路线只对少数头部机构开放。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.1pt;
line-height:120%'><b><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>开源生态派（</span></b><b><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>OpenVLA</span></b><b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>、</span></b><b><span lang=EN-US style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>Spirit v1.5</span></b><b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>、</span></b><b><span lang=EN-US style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>Unitree G1</span></b><b><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>）</span></b><span lang=ZH-CN style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>：以社区速度换单点性能，适合以标准制定和生态入口为目标的玩家。国产开源模型在</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>2026</span><span lang=ZH-CN style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>年首次在综合性能上追平国际一线，是这条路线阶段性成熟的重要信号。</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.0pt;
line-height:120%'><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>四条路线并非非此即彼，更大概率的未来是：开源模型提供通用基底，垂直整合团队在此之上做场景精调与硬件适配，混合架构成为产业部署的工程标准答案。</span></p>


<p class=MsoNormal align=left style='text-align:left;line-height:120%'><a
name="OLE_LINK4"><b><span lang=EN-US style='font-size:12.0pt;line-height:120%;
font-family:SimSun;color:black'>5.5 2026</span></b></a><b><span lang=ZH-CN
style='font-size:12.0pt;line-height:120%;font-family:SimSun;color:black'>年展望：</span></b><b><span
lang=EN-US style='font-size:12.0pt;line-height:120%;font-family:SimSun;
color:black'>2026</span></b><b><span lang=ZH-CN style='font-size:12.0pt;
line-height:120%;font-family:SimSun;color:black'>年展望：从智驾验证到具身落地的规模化跃迁</span></b></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.0pt;
line-height:120%'><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>容易被忽视的是，</span><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>VLA </span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>的产业化进程并非从机器人开始</span><span lang=EN-US style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>——</span><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>自动驾驶才是这一范式最早的工业级验证场。特斯拉的</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'> FSD </span><span lang=ZH-CN style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>系统是迄今最大规模的</span><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'> VLA </span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>工程实践：以摄像头为主传感器、端到端神经网络直接输出控制指令的架构，本质上与</span><span lang=EN-US
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'> VLA </span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>的核心逻辑高度一致。</span><span lang=EN-US style='font-size:11.0pt;
line-height:120%;font-family:SimSun;color:black'>FSD V12 </span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>的发布标志着</span><span lang=EN-US style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>&quot;</span><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>感知</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>-</span><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>规划</span><span lang=EN-US style='font-size:
11.0pt;line-height:120%;font-family:SimSun;color:black'>-</span><span
lang=ZH-CN style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'>控制</span><span lang=EN-US style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>&quot;</span><span lang=ZH-CN
style='font-size:11.0pt;line-height:120%;font-family:SimSun;color:black'>三段式传统架构向端到端范式的实质性切换，为</span><span
lang=EN-US style='font-size:11.0pt;line-height:120%;font-family:SimSun;
color:black'> VLA </span><span lang=ZH-CN style='font-size:11.0pt;line-height:
120%;font-family:SimSun;color:black'>在物理世界大规模部署提供了第一个可信样本。</span></p>
<p class=MsoNormal align=left style='text-align:left;text-indent:22.0pt;
line-height:120%'><span lang=ZH-CN style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>在此基础上，具身机器人正在成为下一个规模化战场。工业制造仍是最确定的落地场景</span><span
lang=EN-US style='font-size:11.0pt;font-family:SimSun;color:black'>——</span><span
lang=ZH-CN style='font-size:11.0pt;font-family:SimSun;color:black'>宁德时代电池产线、汽车总装等精密装配工序提供了可量化的</span><span
lang=EN-US style='font-size:11.0pt;font-family:SimSun;color:black'>ROI</span><span
lang=ZH-CN style='font-size:11.0pt;font-family:SimSun;color:black'>，人形机器人在这些场景的部署规模预计从百台量级向千台量级跃升。消费端，荣耀等消费电子厂商的入场标志着</span><span
lang=EN-US style='font-size:11.0pt;font-family:SimSun;color:black'>B2C</span><span
lang=ZH-CN style='font-size:11.0pt;font-family:SimSun;color:black'>窗口正式开启，但家庭场景的非结构化程度远高于工厂，预计</span><span
lang=EN-US style='font-size:11.0pt;font-family:SimSun;color:black'>2026</span><span
lang=ZH-CN style='font-size:11.0pt;font-family:SimSun;color:black'>年仍以受控环境试点为主，全面商用还需等待安全标准与用户认知同步成熟。</span><span
lang=EN-US style='font-size:11.0pt;font-family:SimSun;color:black'><br>
<br>

  

**参考文献**


<p class=MsoNormal align=center style='text-align:center'><b><span lang=EN-US
style='font-family:"Times New Roman",serif'>&nbsp;</span></b></p>


<p class=MsoNormal style='word-break:break-all'><b><span lang=ZH-CN
style='font-family:SimSun'>学术论文</span></b></p>


<p class=MsoListParagraphCxSpFirst style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[1].<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp; </span></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>Sapkota R, Cao Y,
Roumeliotis K I, et al. Vision-Language-Action (VLA) Models: Concepts,
Progress, Applications and Challenges[R]. arXiv:2505.04769, 2025.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[2].<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp; </span></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>Xu C, Li Q, Luo J, et
al. RLDG: Robotic Generalist Policy Distillation via Reinforcement Learning[R].
arXiv:2412.09858, 2024.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[3].<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp; </span></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>Foster D J, Block A,
Misra D. Is Behavior Cloning All You Need? Understanding Horizon in Imitation
Learning[R]. arXiv:2407.15007, 2024.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[4].<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp; </span></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>Shi L, et al. Beyond
Imitation: Reinforcement Learning-Based Sim-Real Co-Training for VLA Models[R].
arXiv:2602.12628, 2026.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[5].<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp; </span></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>Brohan A, et al. RT-1:
Robotics Transformer for Real-World Control at Scale[C]. Robotics: Science and
Systems (RSS), 2023. arXiv:2212.06817.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[6].<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp; </span></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>Dosovitskiy A, Beyer L,
Kolesnikov A, et al. An Image is Worth 16x16 Words: Transformers for Image
Recognition at Scale[C]. International Conference on Learning Representations
(ICLR), 2021. arXiv:2010.11929.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[7].<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp; </span></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>Shridhar M, Manuelli L,
Fox D. Perceiver-Actor: A Multi-Task Transformer for Robotic Manipulation[C].
Conference on Robot Learning (CoRL), 2022. arXiv:2209.05451.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[8].<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp; </span></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>Kerbl B, Kopanas G,
Leimkühler T, et al. 3D Gaussian Splatting for Real-Time Radiance Field
Rendering[J]. ACM Transactions on Graphics (SIGGRAPH), 2023, 42(4).
arXiv:2308.04079.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[9].<span
style='font:7.0pt "Times New Roman"'>&nbsp;&nbsp;&nbsp; </span></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>Zitkovich B, Yu T, et
al. RT-2: Vision-Language-Action Models Transfer Web Knowledge to Robotic
Control[C]. Conference on Robot Learning (CoRL). PMLR 229: 2165–2183, 2023.
arXiv:2307.15818.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[10].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>Driess D, Xia F, Sajjadi M S M, et
al. PaLM-E: An Embodied Multimodal Language Model[C]. International Conference
on Machine Learning (ICML), 2023. arXiv:2303.03378.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[11].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>Chi C, Feng S, Du Y, et al.
Diffusion Policy: Visuomotor Policy Learning via Action Diffusion[C]. Robotics:
Science and Systems (RSS), 2023. arXiv:2303.04137.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[12].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>Kim M J, Pertsch K, Karamcheti S,
et al. OpenVLA: An Open-Source Vision-Language-Action Model[C]. Conference on
Robot Learning (CoRL), 2024. arXiv:2406.09246.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[13].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>[14] Black K, Brown N, Driess D, et
al. </span><span lang=EN-US style='font-family:SimSun'>π</span><span
lang=EN-US style='font-family:"Cambria Math",serif'>₀</span><span lang=EN-US
style='font-family:SimSun'>:</span><span lang=EN-US style='font-family:"Times New Roman",serif'>
A Vision-Language-Action Flow Model for General Robot Control[R].
arXiv:2410.24164, 2024.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[14].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>Bjorck J, Castañeda F, Cherniadev
N, et al. GR00T N1: An Open Foundation Model for Generalist Humanoid Robots[R].
NVIDIA, arXiv:2503.14734, 2025.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[15].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>Pertsch K, Stachowicz K, Ichter B,
et al. FAST: Efficient Action Tokenization for Vision-Language-Action
Models[R]. arXiv:2501.09747, 2025.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[16].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>Gemini Robotics Team, Google
DeepMind. Gemini Robotics: Bringing AI into the Physical World[R].
arXiv:2503.20020, 2025.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[17].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>Open X-Embodiment Collaboration,
O'Neill A, Rehman A, et al. Open X-Embodiment: Robotic Learning Datasets and
RT-X Models[C]. IEEE International Conference on Robotics and Automation
(ICRA), 2024. arXiv:2310.08864.</span></p>


<p class=MsoListParagraphCxSpMiddle style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[18].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>James S, Ma Z, Rovick Arrojo D, et
al. RLBench: The Robot Learning Benchmark &amp; Learning Environment[J]. IEEE
Robotics and Automation Letters, 2020, 5(2): 3019–3026. arXiv:1909.12271.</span></p>


<p class=MsoListParagraphCxSpLast style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[19].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>Liu B, Zhu Y, Gao C, et al. LIBERO:
Benchmarking Knowledge Transfer for Lifelong Robot Learning[C]. Advances in
Neural Information Processing Systems (NeurIPS), 2023. arXiv:2306.03310.</span></p>


<p class=MsoNormal style='word-break:break-all'><span lang=EN-US
style='font-family:"Times New Roman",serif'>&nbsp;</span></p>


<p class=MsoNormal style='word-break:break-all'><b><span lang=ZH-CN
style='font-family:SimSun'>开源项目</span></b></p>


<p class=MsoListParagraph style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[20].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>Denghaoyuan123.
Awesome-RL-VLA[CP/OL]. GitHub, 2024–2025.&nbsp;</span><span lang=EN-US><a
href="https://github.com/Denghaoyuan123/Awesome-RL-VLA"><span style='color:
windowtext;text-decoration:none'>https://github.com/Denghaoyuan123/Awesome-RL-VLA</span></a></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>.</span></p>


<p class=MsoNormal style='word-break:break-all'><span lang=EN-US
style='font-family:"Times New Roman",serif'>&nbsp;</span></p>


<p class=MsoNormal style='word-break:break-all'><b><span lang=ZH-CN
style='font-family:SimSun'>技术报告</span></b><b><span lang=EN-US style='font-family:
"Times New Roman",serif'> / </span></b><b><span lang=ZH-CN style='font-family:
SimSun'>企业博客</span></b></p>


<p class=MsoListParagraph style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[21].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=EN-US
style='font-family:"Times New Roman",serif'>Figure AI. Helix: A
Vision-Language-Action Model for Generalist Humanoid Control[R/OL]. Figure AI
Official Blog, 2025-02-20.&nbsp;</span><span lang=EN-US><a
href="https://www.figure.ai/news/helix"><span style='color:windowtext;
text-decoration:none'>https://www.figure.ai/news/helix</span></a></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>.</span></p>


<p class=MsoNormal style='word-break:break-all'><span lang=EN-US
style='font-family:"Times New Roman",serif'>&nbsp;</span></p>


<p class=MsoNormal style='word-break:break-all'><b><span lang=ZH-CN
style='font-family:SimSun'>新闻资讯</span></b></p>


<p class=MsoListParagraphCxSpFirst style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[22].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=ZH-CN
style='font-family:SimSun'>环球网资讯</span><span lang=EN-US style='font-family:
"Times New Roman",serif'>. </span><span lang=ZH-CN style='font-family:SimSun'>彭博社等多家外媒关注：荣耀首款人形机器人将亮相</span><span
lang=EN-US style='font-family:"Times New Roman",serif'> MWC 2026[EB/OL]. </span><span
lang=ZH-CN style='font-family:SimSun'>环球网</span><span lang=EN-US
style='font-family:"Times New Roman",serif'>, 2026-02-24.&nbsp;</span><span
lang=EN-US><a
href="https://baijiahao.baidu.com/s?id=1857982794915351595&amp;wfr=spider&amp;for=pc"><span
style='color:windowtext;text-decoration:none'>https://baijiahao.baidu.com/s?id=1857982794915351595&amp;wfr=spider&amp;for=pc</span></a></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>.</span></p>


<p class=MsoListParagraphCxSpLast style='margin-left:22.0pt;text-indent:-22.0pt;
word-break:break-all'><span lang=EN-US style='font-family:"Times New Roman",serif'>[23].<span
style='font:7.0pt "Times New Roman"'> </span></span><span lang=ZH-CN
style='font-family:SimSun'>第一电动编辑部</span><span lang=EN-US style='font-family:
"Times New Roman",serif'>. EV </span><span lang=ZH-CN style='font-family:SimSun'>晨报</span><span
lang=EN-US style='font-family:"Times New Roman",serif'> | </span><span
lang=ZH-CN style='font-family:SimSun'>字节最新交易估值达</span><span lang=EN-US
style='font-family:"Times New Roman",serif'> 5500 </span><span lang=ZH-CN
style='font-family:SimSun'>亿美元；月之暗面新融资超</span><span lang=EN-US
style='font-family:"Times New Roman",serif'> 7 </span><span lang=ZH-CN
style='font-family:SimSun'>亿美元；具身智能新晋四家百亿估值独角兽：星海图、自变量、智平方、千寻智能</span><span
lang=EN-US style='font-family:"Times New Roman",serif'>[EB/OL]. </span><span
lang=ZH-CN style='font-family:SimSun'>第一电动网</span><span lang=EN-US
style='font-family:"Times New Roman",serif'>, 2026-02-26.&nbsp;</span><span
lang=EN-US><a href="https://www.d1ev.com/news/shichang/288995"><span
style='color:windowtext;text-decoration:none'>https://www.d1ev.com/news/shichang/288995</span></a></span><span
lang=EN-US style='font-family:"Times New Roman",serif'>.</span></p>


<p class=MsoNormal style='word-break:break-all'><span lang=EN-US
style='font-family:"Times New Roman",serif'>&nbsp;</span></p>


<p class=MsoNormal align=left style='text-align:left;text-indent:22.0pt;
line-height:120%'><span lang=EN-US style='font-size:11.0pt;line-height:120%;
font-family:SimSun;color:black'>&nbsp;</span></p>


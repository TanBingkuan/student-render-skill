# Skill Test Log

Skill name: view-to-render
Repository / Commit: <填写实际仓库 URL 和 Commit ID>
Runtime: <Codex 版本 / 环境、工具或 MCP>

> 必须用真实记录填写，不要伪造“每人必须发现一次问题”。
> 如所有合理测试都通过，报告测试条件和仍未覆盖的情况。

## T1 Normal run

Date: 2026-11-24
Input file: examples/input/perspective-01.png（Rhino 固定机位透视，1226 x 918，用户 2026-11-24 10:08 发来的截图；已另存为 perspective-01.png）
Request / skill invocation: 请使用 $view-to-render。输入 examples/input/perspective-01.png。目标：日间浅色石材 + 暖木裙楼 / 庭院墙，玻璃、绿化、人物。保留相机、建筑群轮廓、运动场 / 前广场位置、植物大致位置。生成实际 PNG，保存为 examples/output/run-01.png。
Actual tool used: Muse 图像生成工具（media.generate_image），以 perspective-01.png 为底图编辑生成
Output file: examples/output/run-01.png（3.3 MB，可打开）
Expected conditions: 实际 PNG 可打开；目标材质改变；固定对象关系无明显漂移；人物站稳、尺度对得上
Observed result: 第一版：相机、建筑位置与轮廓、庭院空洞、后方高塔、前广场位置都保留了；立面改为浅色暖石材 + 暖木裙楼，玻璃、铺装、绿化、人物都出现了，人物站在地面上。但层数错了：每栋楼被合成 3-4 条大玻璃带，模型里实际是 13-20 层。第一版判定 FAIL（层数）。
修订后（当前 run-01.png）：从模型数出实际层数再重跑——最高塔 20 层（Z 10-90 m，每层 4 m），其余塔 13-15 层（每层约 3-4 m），庭院楼 13-14 层；只把大玻璃带拆成细层，不动相机和布局。现版左塔约 15-16 层、右塔约 15-16 层、后方高塔约 20 层、中部庭院楼约 10-12 层，与模型基本对上。仍有偏差：① 右侧背景多了一片远景，原图没有；② 左上 Rhino 网格在天空中还隐约看得见；③ 各塔层数是“约数”，不是逐层数过的精确值，生成式工具仍可能差 1-2 层。
PASS / FAIL: PASS（修订后，带上述 3 处已记录的偏差）
Evidence location: examples/input/perspective-01.png、examples/input/site-context-macau-aerial.png（场地实景参考，澳门艺术博物馆 / 观音像海滨一带空地，带标注和 Airbus 水印，仅作核对，不作提交源图）、examples/output/run-01.png；被替换的中间版已从输出目录清理，修订过程见本日志。

## T2 Valid variation

Date: 2026-11-24
Changed input: 同一张源视图 examples/input/perspective-01.png，同一机位、同一材料（浅色暖石材 + 暖木裙楼），只把光照从日间改成黄昏暖光，窗户亮灯、广场灯亮。
Request / skill invocation: 请使用 $view-to-render。输入 examples/input/perspective-01.png（先以 run-01.png 为底做光照编辑，以保住相机和布局）。目标：黄昏暖光，窗户亮暖灯，广场灯亮，材料不变。保留相机、建筑群轮廓、层数、人物和树的比例。生成实际 PNG，保存为 examples/output/run-02.png。
Actual tool used: Muse 图像生成工具（media.generate_image），先以 perspective-01.png 直接生成一版（相机漂移较大，已废弃），再以 run-01.png 为底只改光照重做一版，即当前 run-02.png
Actual output: examples/output/run-02.png（3.6 MB，可打开）
Checks and differences: 与 run-01 对照，相机、建筑位置与轮廓、层数（左塔约 15-16 层、后方高塔约 20 层）、人物（约半层高）、树（约 2 层高）都保持了；变化符合要求：天空变黄昏暖色，窗户亮暖灯，广场灯亮，影子变长。仍有偏差：右侧背景的远景和左上 Rhino 网格仍在（继承自 run-01）；第一版直接从源图生成的黄昏版相机漂移较大，已废弃，过程如实记录。
PASS / FAIL: PASS（带上述已记录的偏差）
Evidence location: examples/input/perspective-01.png、examples/output/run-01.png、examples/output/run-02.png

## Run-03 Plan (second variation, new drawing type)

Date: 2026-11-24
Input file: examples/input/plan-01.png（模型平面，Top 正投影，1032 x 910）为主；examples/input/plan-line.png（彩色平面线稿，同场地）为核对参考，只用来看内部划分、庭院和绿化形状，不抄它的颜色。
Request / skill invocation: 请使用 $view-to-render。输入 plan-01.png，参考 plan-line.png。目标：日间平面，浅色暖石材屋面 / 铺装 + 暖木裙楼边，绿化、树（俯视树冠约 4-5 m）、人物俯视小人。保留北向朝上（图上方为北，建筑斜向于北向）、每栋轮廓、庭院空洞、右下角运动场大矩形、五栋主楼位置不变。
Actual tool used: Muse 图像生成工具（media.generate_image），以 plan-01.png 为底、plan-line.png 为参考生成
Output file: examples/output/run-03.png（2.3 MB，可打开）
Expected conditions: 实际 PNG 可打开；方向和轮廓不变；材料与 run-01 一致；树和人是俯视比例
Observed result: 方向、五栋主楼轮廓、庭院空洞、右下角运动场位置都保留了；屋面浅色石材、木边、绿化、俯视树冠和 tiny 人物都出现了，与线稿的有机绿化形状基本对得上。可见偏差：① 右下角运动场在源图里是空白矩形，生成图里加了足球场线和跑道——按 Sports ground 图层推断是合理的，但源图里没有，是生成器补的，要如实说明；② 部分庭院的绿化布局是生成器按线稿形状重新排的，不是逐一对照的精确复制；③ 个别内部划分被简化了。
PASS / FAIL: PASS（带上述已记录的偏差）
Evidence location: examples/input/plan-01.png、examples/input/plan-line.png、examples/output/run-03.png

## Run-04 Section A-A (SUPERSEDED — Y=284 bounding-box version, withdrawn, do not use)

> 本条已作废。源图是按模型外包框在 Y=284 处取交集画的，混入了实际不在该剖切面上的体块，不是真实剖切。正确版本见下面第二条 Run-04。

Date: 2026-11-24
Input file: （已作废）examples/input/section-A-A-diagnostic-Y284-SUPERSEDED.png — 原按 W2_0_3jpt.3dm 在 Y=284 处取交集画的诊断剖面：西塔 81 m、庭院楼 53 m / 14 层、中塔 52 m / 14 层、东塔 90 m / 20 层，裙楼 10-14 m，地面 +/-0.00，运动场为两者之间的开敞地面，人 1.7 m、树 7 m。
Request / skill invocation: 请使用 $view-to-render。输入 section-A-A.png。目标：日间剖面，浅色暖石材 + 暖木裙楼，玻璃按层带，地面和树、人按比例。保留剖切位置、每栋宽度和高度、地面标高。
Actual tool used: Muse 图像生成工具（media.generate_image），以 section-A-A.png 为底生成
Output file: examples/output/run-04.png（2.3 MB，可打开）
Expected conditions: 实际 PNG 可打开；高度和位置不变；层数对得上；人约半层高、树约 2 层高
Observed result: 高度和位置基本保留了：西塔 81 m、庭院 53 m、中塔 52 m、东塔 90 m，裙楼、地面、运动场空隙都在，材料与 run-01 一致。可见偏差：① 生成器给中塔和东塔多加了几层，中塔应为 14 层、生成图约 20 层，东塔应为 20 层、生成图约 22-23 层；曾试过只改层数重跑一版，但那版把中塔高度也改错了，已废弃，仍用第一版；② 人和树偏大了一点，人约 0.4 层高、树约 3 层高左右；③ 西塔在模型里本无分层，生成图按 3-4 m 层高给了层带，这是按其他塔的层高节奏补的，要如实说明。
PASS / FAIL: WITHDRAWN — 本条作废，不计入提交，正确版本见下面第二条 Run-04
Evidence location: （已作废）诊断剖面原文件已移出提交包，保留在本地工作记录 diagnostics/ 里，提交包里不再有该文件

## Run-04 Section A-A (third drawing type) — CORRECTED, current version

Date: 2026-11-24
Input file: examples/input/section-A-A.png（用户 11:39 发来的剖面，裁自 W2_section_A-A_preview.png 右半；全页另存为 section-A-A-sheet.png）
Correction: 我之前建议的剖切线是东西向 Y=284，那是我按模型外包框推测的，是错的。用户实际剖切线是南北向、在场地东侧，平面图上红线标为 A-B，剖面标题为 SECTION A-A；场地长轴 22.1 度。我之前按 Y=284 画的那张诊断剖面已改名为 section-A-A-diagnostic-Y284-SUPERSEDED.png，不再作源图。
Request / skill invocation: 请使用 $view-to-render。输入 section-A-A.png。目标：日间剖面，浅色暖石材 + 暖木裙楼。保留高度和层数：高塔 90 m，裙楼 10 m 空白，其上 20 层、每层约 4 m；右侧三栋低楼各 16 m、4 层；地面线 0 m 平直。人物 1.7 m、树 6-8 m。
Actual tool used: Muse 图像生成工具（media.generate_image），以 section-A-A.png 为底生成
Output file: examples/output/run-04.png（0.86 MB，可打开）
Expected conditions: 实际 PNG 可打开；高度、层数、地面线不变；材料与 run-01 一致；人物和树是剖面比例
Observed result: 高塔 20 层、右侧低楼各 4 层、地面线平直都保留了；立面浅色石材、裙楼暖木、每层玻璃、地面绿带、人物（很小，约 1/53 塔高）和树都出现了。可见偏差：① 裙楼木面约 13-14 m，比源图 10 m 空白裙楼略高，顶上还多了一层通长玻璃（可理解为 10-14 m 首层，但源图首层是带窗带）；② 右侧树约 10-12 m，比 6-8 m 目标略高；③ 剖面标题和刻度数字已按要求去掉，汇报用时需另加标注。
PASS / FAIL: PASS（带上述已记录的偏差）
Evidence location: examples/input/section-A-A.png、examples/input/section-A-A-sheet.png、examples/output/run-04.png

## T3 Missing input / boundary

Date: 2026-11-24
Missing condition: 没有源视图、没有目标材料。用户在 2026-11-24 上午只发了三份任务书和 W2_0_3jpt.3dm，没有发 Rhino 导出视图，也没定目标材料。
Request / skill invocation: （隐含请求）按 Path B 出第一张效果图，但未提供 perspective-01.png。
Actual response: 没有生成任何假图、没有伪造输出路径。先说明了缺一张 Rhino 固定机位导出视图和目标材料，写了 Path-B-第一次出图.md，列出要在 Rhino 里导出 perspective-01.png 并定材料后才能跑。直到用户 10:08 发来透视图、定下日间浅色石材后，才跑了 run-01。
Did it report the missing condition honestly? 是。明确指出缺输入、暂不执行。
PASS / FAIL: PASS
Evidence location: 本对话 2026-11-24 上午记录；examples/input/perspective-01.png（后补的输入）；Path-B-第一次出图.md

## Revision history

Original issue: 2026-11-24，用户指出“层数要对上”，并给了澳门实景图。第一版 run-01 把每栋楼 13-20 层合成 3-4 条大玻璃带，层数 FAIL。
Changed SKILL.md section: Workflow / Fixed 增加一条——出图前必须先从 .3dm 数出每栋楼的层数（最高塔 20 层，其余 13-15 层，每层 3-4 m），生成时逐栋写明层数，禁止把多层合并成一条大玻璃带；检查时逐栋数层。
New commit: （待上传 GitHub 后填）
Retest result: 修订后 run-01 左塔约 15-16 层、右塔约 15-16 层、后方高塔约 20 层，PASS（带偏差，见 T1）。
Unresolved limitations: 生成式工具层数仍可能差 1-2 层；右侧远景和左上 Rhino 网格未完全去掉；实景图的标注 / 水印不能进提交。

## 人物比例修订（2026-11-24，第二轮）

Original issue: 用户指出“人的比例不对”。放大检查发现：上一版人物约 1/3 层高、约 1/3 树高，相对 10 m 裙楼也偏大，约是正确比例的 2 倍。
Changed: 只改人物，不动相机和楼。按 1.7 m 人 / 3-4 m 层高 / 10 m 裙楼 / 6-8 m 树 / 0.45 m 长凳换算：人约半层高、约 1/6 裙楼高、约 1/4 树高，缩小约一半，脚落在地面上。
Retest result: 现版 run-01.png 人物明显变小，广场上的人约半层高，树约 4-6 倍人高，坐凳上的人与长凳比例对得上。仍需用户目测确认。
Unresolved: 生成式工具的人物尺度仍可能在不同位置不一致，远处与近处的人大小要逐处看。

## 树木比例修订（2026-11-24，第三轮）

Original issue: 用户指出“树大了一点吧”。上一版树约 3-4 层高、树冠遮住楼和广场，偏大。
Changed: 只改树，不动相机、楼和人。按树高 6-8 m、约 2 层高、树冠约 4-5 m、约 4 倍人高换算，缩小到原来的约 60%，树干变细，位置留在原花坛里。
Retest result: 现版 run-01.png 树明显变小，中央和两侧的树约 2 层高，树冠不再遮楼，人物比例保持上一版。
Unresolved: 生成式工具的树仍可能在不同位置大小不一致，要逐棵看。

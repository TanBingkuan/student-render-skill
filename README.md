# View to Render (Student Skill)

根据现有 Rhino 固定机位视图，生成建筑或景观材质效果图的学生 Skill。
技术路线：Path B — 基于 Rhino 视图的生成式图像转换（2026-11-24 已定）。
项目模型：W2_0_3jpt.3dm（场地 810 x 558 m，建筑群最高 90 m，中间有运动场；场地在澳门艺术博物馆 / 观音像海滨一带）。
汇报日期：2026年12月11日

> 学号：1250038701　姓名：_谭秉宽　

## Purpose

此 Skill 面向的设计任务是：把 Rhino 固定机位视图转换成日间材质效果图，表现本项目场地与建筑群，图种覆盖 Perspective、Plan、Section 三种。

不适用于：凭空创建设计方案、修改三维结构、结构性能计算、没有源图的纯概念绘图。

## Requirements

- Codex 环境（或实际使用的环境）：本仓库的出图是在 Muse 的图像生成工具上实际跑通的；在 Codex 里使用时，请用你实际验证过的图像生成工具，填入名称：________
- Rhino 版本：用于导出源视图，不直接渲染 .3dm；导出时用的是项目同一版模型 W2_0_3jpt.3dm
- 不需要购买指定 API 或第三方软件来完成本课。

不要把 API Key、账户凭证写进 README 或提交到仓库。需要凭证时，只说明应在本地安全环境中配置什么类型的凭证。

## Skill Location

`.agents/skills/view-to-render/SKILL.md`

## Inputs and Outputs

输入：

- `examples/input/W2_0_3jpt.3dm` — Rhino 模型（14 MB）
- `examples/input/perspective-01.png` — Rhino 固定机位透视，东南往西北，相机抬高约 15-20 m
- `examples/input/plan-01.png` — 模型平面，Top 正投影，图上方为北，建筑斜向于北向；`plan-line.png` 为彩色线稿核对参考
- `examples/input/section-A-A.png` — 剖面 A-A，剖切线南北向在场地东侧（平面红线标 A-B），场地长轴 22.1 度；全页另存为 `section-A-A-sheet.png`
- `examples/input/site-context-macau-aerial.png` — 场地实景参考，带标注和 Airbus 水印，仅作核对，不作提交源图

目标材料：日间浅色暖石材立面 + 暖木裙楼 / 庭院墙，玻璃、铺装、绿化、人物。

必须保留：固定视角；场地范围与底板；建筑群位置与轮廓；运动场位置；每栋楼的层数（最高塔 20 层、其余 13-15 层，每层 3-4 m）；人物 1.7 m（约半层高）；树 6-8 m（约 2 层高，树冠 4-5 m）。

输出：

- `examples/output/run-01.png` — Perspective 日间版
- `examples/output/run-02.png` — Perspective 黄昏版（同一机位、同一材料，只改光照）
- `examples/output/run-03.png` — Plan 日间版
- `examples/output/run-04.png` — Section A-A 日间版

每次生成都另存为新 PNG，不覆盖原始输入。

## How to Run

1. 打开这个仓库作为 Codex 工作项目。
2. 检查所需工具 / 权限实际可用。
3. 使用 `$view-to-render` 及相应输入，例如：

```
请使用 $view-to-render。
输入：examples/input/perspective-01.png。
目标：日间浅色暖石材 + 暖木裙楼，玻璃、绿化、人物。
保留：相机、建筑群轮廓、运动场位置、层数（最高塔 20 层）、人物 1.7 m、树 6-8 m。
生成实际 PNG，不要只返回提示词或文字建议。
将结果保存为 examples/output/run-01.png。
完成后列出实际调用的工具、输出路径和检查结果。
```

4. 在 `examples/output/` 中检查真实图片。

## Testing

请参见 `tests/test-log.md`：

- T1 正常输入（run-01，含层数、人物、树三轮修订）
- T2 合理变化（run-02 黄昏版；run-03 平面；run-04 剖面）
- T3 缺项或边界（缺源视图时如实报告、不伪造输出）

## Limitations and Sources

当前仍不能验证 / 已知偏差：

- 生成式图像的层数、人物和树仍可能差 1-2 层 / 略大略小，须逐栋、逐处数过，见 test-log
- run-01 右侧背景多了一片远景、左上 Rhino 网格仍隐约可见
- run-03 右下角运动场的足球场线和跑道是按 Sports ground 图层推断补的，源图里是空白矩形
- run-04 裙楼木面约 13-14 m，比源图 10 m 略高；右侧树约 10-12 m，比 6-8 m 目标略高

参考来源：

- Agent Skills Specification — https://agentskills.io/specification
- OpenAI — Build skills — https://learn.chatgpt.com/docs/build-skills
- McNeel — Rhino MCP / Codex — https://mcneel.github.io/RhinoAI/docs/getting-started/codex/
- AI Hero Skills — https://www.aihero.dev/skills

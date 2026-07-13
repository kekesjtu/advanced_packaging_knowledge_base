# 2D-IC 集成

2D 集成的共同特征：基板/RDL上有多芯片。

## 1. 引线键合（Wire Bonding）

```txt
塑封料
→ 多颗 silicon die，正面朝上并排，有源层和焊盘位于上表面
→ die attach
→ package substrate（wire bond 从各芯片顶面外围焊盘跨接到基板焊盘）
→ BGA solder balls
→ PCB
```

若芯片直接贴在 PCB 上，则 `package substrate + BGA solder balls` 可由 PCB 本身取代。

![alt text](/images/2D/引线键合.png)

## 2. 倒装芯片（Flip Chip）

```txt
塑封料
→ 多颗 silicon die 的背面，芯片并排且正面朝下
→ die有源层和焊盘
→ C4 / C2 填充 underfill
→ package substrate
→ BGA solder balls
→ PCB
```

## 3. 引线键合与倒装芯片混合集成

```txt
塑封料
→ face-up die（顶面焊盘接 wire bond）+ face-down die
→ die attach（用于 face-up die）+ C4 / C2 填充 underfill（用于 face-down die）
→ package substrate
→ BGA solder balls
→ PCB
```

![alt text](/images/2D/倒装+引线键合.png)

## 4. Chip-first 扇出集成

```txt
塑封料
→ silicon die，通常正面朝下，有源层和焊盘在重构晶圆的下表面
→ 直接制作在芯片焊盘和 EMC 表面的 fan-out RDL
→ BGA solder balls
→ PCB
```

![alt text](/images/2D/chip-first.png)

商业例子：

1. HTC’s Desire 606 W：2013 年出货的早期移动产品 fan-out 应用。baseband modem 与 application processor 采用 chip-first、face-down 方式并排嵌入 EMC，通过两层 organic RDL 扇出后直接以焊球连接 PCB；封装尺寸为 `7.4 mm × 7.4 mm × 0.71 mm`，具有 230 颗 `0.4 mm` pitch 焊球，RDL 的 L/S 为 `20/20 μm`。

## 5. Chip-last 扇出集成

```txt
塑封料
→ 多颗 silicon die，后贴装且正面朝下
→ C2 + molded underfill（即渗入的EMC）⬅ 比chip-first多了这层
→ 预先制作的 fan-out RDL substrate
→ BGA solder balls
→ PCB
```

注：典型 Chip-first、face-down 扇出中，芯片先嵌入 EMC，随后直接在芯片焊盘和 EMC 表面制作 RDL。因此不存在倒装贴片的悬空间隙，没有 `C2+ underfill`。

![alt text](/images/2D/chip-last.png)

商业方案：

1. Amkor’s SWIFT（Silicon Wafer Integrated Fan-out Technology）：采用与 IME chip-last 方案相近的 organic RDL-first 流程。芯片通过 Cu-pillar + solder cap 连接预制 RDL substrate，完成 underfill 和 molding 后，封装以 solder balls 直接连接 PCB。
2. Unimicron’s Fan-Out with Chip-Last：在预制 RDL-first substrate 上集成一颗大芯片和两颗小芯片，分别可对应 application processor 与 memories；最小 RDL L/S 为 `2/2 μm`。大芯片通过 Cu-pillar solder bumps 连接 RDL substrate，封装再以 solder balls 直接连接 PCB。

## 6. 基于 Hybrid RDL 的 Chip-last 扇出集成

整体拓扑与第 5 节相同，仅将其中的 RDL substrate 细分为：

```txt
芯片侧超细间距 inorganic RDL（SiO2 / SiNx + dual-damascene Cu）
→ 多层 organic RDLs（聚合物介质 + 电镀铜），逐级放大线宽、焊盘和间距
```

![alt text](/images/2D/Hybrid-RDLs.png)

商业方案：

1. Amkor’s SLIM（Silicon-Less Integrated Module）：结构与 SWIFT 相近，但使用 hybrid RDL。靠近芯片的 RDL1 采用半导体工艺制作，L/S 可达 `0.5/0.5 μm`；后续 RDL2、RDL3 使用聚合物介质和电镀铜，L/S 分别约为 `5/5 μm` 和 `10/10 μm`。
2. SPIL’s Fan-Out on Hybrid RDLs：SPIL 于 2016 年首次验证 chip-last fan-out 与 hybrid RDL 结合的可行性。芯片侧 M1 使用 `SiO2/SiNx + dual-damascene Cu`，L/S 为 `2/2 μm`；M2、M3 使用 PBO 和有机 RDL 工艺，L/S 分别为 `5/5 μm` 和 `10/10 μm`，芯片通过 microbumps 与 molded underfill 连接这些 RDL。

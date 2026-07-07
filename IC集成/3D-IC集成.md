# 3D-IC 集成

3D 集成的共同特征：3D 集成至少包含**3D IC封装集成**和**3D IC集成**两大范畴。

首先，从定义上讲，3D IC 封装集成和3D IC集成都是在**垂直方向上堆叠芯片**。

在本书中，3D IC集成与3D IC封装的关键区别在于:

1. 3D IC 封装集成先有若干功能完整的芯片，再通过封装组装方法把它们垂直堆起来，例如典型的PoP。
2. 3D IC 集成不只是把芯片叠起来，而是让多个芯片通过高密度垂直互连，在电气上接近一颗复合 IC。
3. 3D IC集成使用硅通孔（TSV）而3D IC封装则不使用（书中原文）。

以下描述均按完成封装后的典型截面从上到下排列。“正面”指包含有源层和芯片焊盘的一面；face-to-face、back-to-back 和 face-to-back 描述相邻芯片的朝向关系。

## 1. 3D IC 封装

### 1.1 引线键合存储器堆叠

```txt
空气 / 塑封料
→ 多层薄化 memory die，通常正面朝上并逐层错位，以露出外围焊盘
→ 各层之间的 die attach film / spacer
→ 底层 die attach
→ coreless organic package substrate
  （每层芯片的外围焊盘分别通过 wire bond 接到基板）
→ BGA solder balls
→ PCB
```

![Samsung SSD 的引线键合存储器堆叠](/pictures/3D/引线键合存储器堆叠.png)

图片来源：`[PDF]` p.349，Figs. 7.7–7.8。

商业例子：

1. Samsung 为 Apple iPhone 制造的 8 层 flash die stack：芯片厚度约 `55–70 μm`，采用外围 wire bonding（p.344）。
2. Samsung `Portable SSD T3 2 TB`：每个封装容纳 16 颗 48-layer V-NAND die，单颗约 `40 μm` 厚（pp.344、349）。

### 1.2 面对面键合并通过引线连接基板

```txt
空气 / 塑封料
→ 上层 die 背面
→ 上层 die，有源面朝下
→ microbumps 或 hybrid-bond interface
→ 较大的下层 die，有源面朝上，外围焊盘保持外露
→ 下层 die 背面 + die attach
→ package substrate（wire bond 从下层 die 外露焊盘接到基板）
→ BGA solder balls
→ PCB
```

![Sony 面对面堆叠并通过引线引出](/pictures/3D/面对面-引线.png)

图片来源：`[PDF]` p.350，Fig. 7.9。

商业例子：

1. Sony PlayStation `CXD53135GG`：5-chip stack；DDR2、spacer 和 DDR2 采用 wire bond 堆叠，wide-I/O SDRAM 与 processor 采用面对面微凸点连接，再由 processor wire bond 引出（pp.344–350）。
2. Sony backside-illuminated CMOS image sensor（BI-CIS）：sensor 与 processor 面对面混合键合，processor 外围通过 wire bond 引出（pp.345、350）。

### 1.3 背对背键合并通过引线连接基板

```txt
空气 / 塑封料
→ 上层 die，有源面朝上；顶面焊盘通过 wire bond 接基板
→ 上层 die 背面
→ die attach，形成 back-to-back 界面
→ 下层 die 背面
→ 下层 die 有源面朝下
→ flip-chip bumps + underfill
→ package substrate
→ BGA solder balls
→ PCB
```

![Intel PMB9955 背对背堆叠](/pictures/3D/背对背-引线.png)

图片来源：`[PDF]` p.351，Fig. 7.11。

商业例子：

1. Intel `PMB9955` modem chipset（用于 iPhone XR）：baseband AP 倒装在 3-layer ETS 上，DRAM 贴在 AP 背面并 wire bond 到 ETS（pp.346、351）。

### 1.4 面对面键合并通过焊凸点/焊球连接基板

```txt
空气 / 塑封料
→ 上层 die 背面
→ 上层 die 有源面朝下
→ C2 / microbumps + underfill
→ 较大的下层 logic / router die，有源面朝上
→ 下层 die 的外围 RDL、焊盘或其他封装级引出结构
→ solder bumps / balls
→ package substrate
→ BGA solder balls
→ PCB
```

![面对面键合并通过焊球连接基板](/pictures/3D/面对面-焊球.png)

图片来源：`[PDF]` p.351，Fig. 7.12。

商业方案 / PDF 收录方案：

1. IME `memory-on-logic`：memory 以 C2 bump 面对面连接 logic，logic 再通过 SnAgCu solder ball 连接刚性或柔性基板（pp.346、351）。
2. Georgia Tech `router + TGV glass`：多颗芯片面对面连接 router，信号经 fan-out RDL 和 through-glass via 引出（pp.347、352）。
3. Fraunhofer IZM `MEMS + ASIC`：MEMS 与 ASIC 面对面连接，ASIC 可通过 solder ball 或 wire bond 引出（pp.347、352）。
4. ASIC-on-FPGA`：ASIC 以`40 μm` pitch microbump 面对面连接 FPGA，FPGA 再以 C4 连接封装基板（pp.347、353）。
5. Amkor `Double-POSSUM`：daughter dies → mother die → grandma die 的两级嵌套堆叠，层间分别使用 C2/C4 bump（pp.347–353）。
6. 3D embedded MEMS/controller：MEMS 与 controller 近面对面连接，使用 fan-out RDL、TPV 和 solder ball 引出（pp.348、354）。

### 1.5 面对背键合

```txt
空气 / 塑封料
→ 顶层 die 背面，顶层 die 有源面朝下
→ microbumps
→ 下层 fan-out package 的背面 RDL
→ TMV / TPV，穿过下层 EMC
→ 下层一颗或多颗 face-down die + EMC
→ 下层 fan-out RDL
→ solder balls
→ PCB
```

![面对背 fan-out 堆叠](/pictures/3D/面对背.png)

图片来源：`[PDF]` p.354，Fig. 7.18。

商业方案 / PDF 收录方案：

1. 3D fan-out face-to-back：上层 Chip 3 倒装到下层 fan-out package 背面，使用 TMV、上下 RDL 和 solder ball 完成垂直互连（pp.352–355）。
2. SPIL `face-to-back 3D package`：顶层芯片经 microbump、fan-out RDL 和 TMV 连接下层芯片，底部以 C4 连接 package substrate（p.355）。

### 1.6 SiP 中的嵌入式芯片（面对面）

```txt
空气 / 塑封料
→ 表面安装的 sensor / IC / passive components
→ 焊点或细间距互连
→ flexible / organic SiP substrate
→ 嵌入基板腔体中的 silicon die，其有源面朝向上方器件，形成 face-to-face 功能界面
→ 基板底部外部焊盘 / BGA solder balls
→ PCB
```

![Fujikura WABE 嵌入式芯片 SiP](/pictures/3D/嵌入式芯片.png)

图片来源：`[PDF]` p.356，Fig. 7.20。

商业方案：

1. Fujikura `WABE`（wafer and board level embedded package）：将 U1 嵌入柔性基板，与上方 sensor face-to-face；封装由 `3.5 mm × 3.5 mm` 缩至 `2.5 mm × 2.5 mm`（pp.355–356）。

### 1.7 基于倒装芯片技术的 PoP

```txt
空气 / 塑封料
→ 顶部 memory die stack，通常正面朝上并以 wire bond 连接
→ top-package coreless substrate
→ PoP solder balls / Cu-core balls
→ 底部封装中的 application processor 背面
→ application processor，正面朝下
→ C4 / C2 bumps + underfill
→ bottom-package build-up substrate
→ BGA solder balls
→ PCB
```

![Apple A9 倒装芯片 PoP](/pictures/3D/PoP-倒装.png)

图片来源：`[PDF]` p.357，Fig. 7.21。

商业例子 / 方案：

1. Apple `A9 + LPDDR4` PoP：A9 倒装在 `2-2-2` build-up substrate，上层为 wire-bonded LPDDR4；PDF 原文将其写作 “iPhone 6 Plus” 截面（pp.356–357）。
2. Qualcomm `Snapdragon 805` + Samsung Galaxy：C2 bump + TC-NCP 连接 Shinko `MCeP` 基板，上层封装通过 Cu-core balls 连接（pp.356、358）。
3. NXP `3D PoP`：底部 4-layer ETS 承载 processor，上层承载 memory，封装间使用双层 solder ball 与 TSV-less interposer（pp.356、358）。
4. Shinko `Cu-core-ball PoP`：底部 memory、顶部 ASIC，层间采用 Cu-core solder balls（pp.356、359）。

### 1.8 基于扇出技术的 PoP

顶部 memory package 与第 1.7 节相同；底部封装改为：

```txt
top-package coreless substrate
→ PoP solder balls，或 TIV / TMV 穿过底部 EMC
→ application processor / chiplets，嵌入 EMC 且有源面朝下
→ fan-out RDL
→ BGA solder balls
→ PCB
```

![Apple TSMC InFO PoP](/pictures/3D/PoP-扇出.png)

图片来源：`[PDF]` p.360，Fig. 7.26。

商业例子 / 方案：

1. STATS ChipPAC `3D fan-out PoP`：底部为约 `450 μm` 厚 AP eWLB，顶部为 wire-bonded memory package（pp.357、359）。
2. Apple / TSMC `InFO-WLP PoP`：PDF 列出 A10、A11、A12、A13、A14 共用相近平台；A12 采用 7 nm、3 层 RDL，并在底部集成 flip-chip IPD（pp.357–360）。
3. TSMC `fan-out chiplet + memory/HBM PoP`：底部为 4～6 层 RDL-first chiplet package，顶部 memory/HBM 通过 laminated TSV-less interposer 连接（pp.358、360）。
4. Samsung smartwatch `ePoP`：上层含 2 DRAM、2 NAND、1 controller；下层 AP 与 PMIC 并排采用 fan-out panel-level packaging（pp.358–361）。
5. IME `RDL-first fan-out PoP`：processor 通过 microbump 连接预制 RDL substrate，顶部 DRAM 直接连接底部封装背面 RDL（pp.359–361）。

## 2. 3D IC 集成

### 2.1 HBM 规范

结构拓扑与第 2.2 节相同。不同代际主要改变 DRAM 层数、通道、速率、容量以及微凸点/混合键合间距，不改变“DRAM 堆叠 → logic base die → 下一级封装”的基本层序。

![HBM HBM2 HBM2E 规格与结构](/pictures/3D/HBM规格.png)

图片来源：`[PDF]` p.363，Fig. 7.31。图中的 HBM3 数值是该书 2021 年出版时的预期值，不应当作现行标准。

商业例子 / 方案：

1. SK hynix `HBM`：PDF 记载首个 HBM memory cube 于 2013 年由 Hynix 制造（pp.363–364）。
2. Samsung 与 SK hynix `HBM/HBM2/HBM2E`：PDF 称两家公司当时是 HBM 模组的 HVM 供应商（pp.362–364）。
3. `HBM2`：2016 年导入；PDF 收录的更新标准上限为 12 die、24 GB、307 GB/s、1024-bit interface（pp.363–364）。
4. `HBM3`：PDF 中仅为当时讨论中的后续规范预测，不是该书确认的量产型号（pp.363–364）。

### 2.2 HBM 组装

```txt
空气 / mold / 可选 heat spreader
→ 顶层 DRAM die 背面
→ 多层薄化 DRAM die
→ 每层之间：TSV + C2 microbumps + NCF（兼作 underfill）
→ logic base die / buffer die，含 TSV 与底部 RDL
→ microbumps
→ passive silicon interposer，或其他下一级高密度载体
→ C4 bumps + build-up package substrate
→ BGA solder balls
→ PCB
```

![HBM TCB-NCF 组装](/pictures/3D/HBM组装.png)

图片来源：`[PDF]` p.364，Fig. 7.33。

商业方案：

1. Samsung / SK hynix `TCB-NCF HBM assembly`：C2 bumped DRAM 逐颗热压键合，NCF 同时承担预置底填材料功能（pp.364–365）。
2. Toray `collective bonding`：先快速预键合，再一次完成多层堆叠后键合，以缩短 4-die stack 的组装时间（pp.365–366）。

### 2.3 基于 TSV 的 CoC

```txt
空气 / mold / 可选 heat spreader
→ 顶层 chip / chiplet 背面，顶层有源面朝下
→ microbumps + underfill
→ 底层 logic / base die，有源面朝上并含 TSV
→ TSV 把正面信号引到背面 RDL / C4 pads
→ C4 bumps
→ package substrate
→ BGA solder balls
→ PCB
```

多层 CoC 时重复“薄化芯片 → microbumps → TSV”单元。

![Intel Foveros 基于 TSV 的 CoC](/pictures/3D/CoC-TSV-Foveros.png)

图片来源：`[PDF]` p.370，Figs. 7.39–7.40。

商业例子 / 方案：

1. Sony `ISX014` stacked camera sensor：BI-CIS 位于 processor 上方，边缘 TSV 将信号引至 processor，再由 wire bond 引出（pp.365–367）。
2. AMD / UCSB active-interposer concept：CPU chiplet、多个 GPU chiplet 与 HBM 集成在带 CMOS 的 active TSV interposer 上（pp.366、368）。
3. Samsung `X-Cube`：2020 年发布，memory 位于带 TSV 的 logic/base die 上方，层间采用 C2 microbump（pp.366、369）。
4. Intel `Foveros`：chiplets/SoC 面对面连接 22FFL active base die；PDF 还收录 `ODI Type 1/2/3` 与 `MDIO` die-to-die interface（pp.366–370）。
5. Intel `Lakefield` mobile processor：2020 年出货，10 nm compute die 堆叠在 22FFL TSV base die 上，是 PDF 给出的 Foveros 具体量产型号（pp.367、370；另见 Chap. 9 pp.429–431）。
6. IME `memory + logic CoC test vehicle`：两颗带 TSV 的芯片通过 `25 μm` pitch microbump 连接（pp.367、371–372）。

### 2.4 带 TSV 的无凸点混合键合 CoC

整体拓扑与第 2.3 节相同，但芯片间界面替换为：

```txt
上层芯片有源面
→ Cu-Cu + dielectric-dielectric hybrid-bond interface（无 microbump、通常无独立 underfill 间隙）
→ 带 TSV 的下层芯片有源面
```

![TSMC SoIC 带 TSV 混合键合](/pictures/3D/混合键合-带TSV-SoIC.png)

图片来源：`[PDF]` p.373，Fig. 7.44。

商业方案 ：

1. Intel `Foveros Hybrid Bonding`：以 Cu-Cu hybrid bonding 取代 Foveros 的 microbump 界面；PDF 收录的是 2020 年公布的技术路线（pp.368、372；Chap. 8 p.406）。
2. TSMC `3DFabric / SoIC`：frontend SoIC 以 bumpless hybrid bonding 将上层 chip 连接到带 TSV 的下层 chip；backend 可组合 `SoIC + InFO` 或 `SoIC + CoWoS`（pp.368、373；Chap. 8 pp.399–400）。
3. TSMC `bumpless HBM stacking`：PDF 展示 4-Hi、8-Hi、12-Hi 等 SoIC/hybrid-bonded memory stack 方案（pp.368、373）。
4. Arm `face-to-face / face-to-back hybrid bonding`：带 TSV 芯片的两类无凸点堆叠及其热分析验证（pp.368–369、374）。

### 2.5 不带 TSV 的无凸点混合键合 CoC

```txt
空气 / mold / 可选 heat spreader
→ 顶层 sensor / logic die 背面
→ 顶层 die 有源面朝下
→ Cu-Cu + dielectric-dielectric hybrid-bond interface
→ 较大的底层 processor / logic die，有源面朝上且不使用 TSV
→ 底层 die 外围焊盘，通过 wire bond 或封装 RDL 引出
→ package substrate / fan-out carrier
→ BGA solder balls
→ PCB
```

![Sony IMX260 无 TSV 混合键合](/pictures/3D/混合键合-无TSV-Sony.png)

图片来源：`[PDF]` p.374，Fig. 7.47。

商业例子：

1. Sony `IMX260` backside-illuminated CMOS image sensor：无 TSV 的 BI-CIS 与 ISP 通过 Cu-Cu + SiO2-SiO2 hybrid bonding 连接；用于 Samsung Galaxy S7，2016 年出货。PDF 将其列为当时已 HVM 的 bumpless hybrid-bonded 产品（Chap. 7 pp.369–371；Chap. 8 pp.391–394）。

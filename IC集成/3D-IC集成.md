# 3D-IC 集成

3D 集成的共同特征是：芯片在垂直方向上堆叠。

本书把 3D 集成分成两个层级：

1. **3D IC Packaging**：通过封装组装方法把功能完整的芯片垂直堆叠，典型互连包括 wire bond、solder bump、fan-out RDL、TMV / TPV、PoP solder balls 等；书中定义为不使用 TSV。
2. **3D IC Integration**：芯片之间通过 TSV、microbump 或 bumpless hybrid bonding 建立更高密度的垂直互连；书中严格定义为使用 TSV，但也把 Sony IMX260 这类无 TSV 的 bumpless hybrid bonding 作为边界案例放在 3D IC integration 小节中。

以下描述均按完成封装后的典型截面从上到下排列。“正面”指包含有源层和芯片焊盘的一面；face-to-face、back-to-back 和 face-to-back 描述相邻芯片的朝向关系。

## 1. 3D IC Packaging：不使用 TSV 的垂直封装

3D IC Packaging 的共同特征是：多个功能芯片垂直堆叠，但垂直互连主要由封装级互连完成，而不是由芯片内 TSV 完成。

![3D IC Packaging 总括拓扑](/images/3D/3D封装总括拓扑-Fig7.1.png)

图片来源：`[PDF]` p.344，Fig. 7.1。

### 1.1 引线键合存储器堆叠

```txt
塑封料
→ 多层薄化 memory die，通常正面朝上并逐层错位，以露出外围焊盘
→ 各层之间的 die attach film / spacer
→ 底层 die attach
→ coreless organic package substrate
  （每层芯片的外围焊盘分别通过 wire bond 接到基板）
→ BGA solder balls
→ PCB
```

这种结构的关键不是芯片间高密度互连，而是把多层存储芯片机械堆叠，并通过外围引线逐层引出到基板。

![Samsung SSD 的引线键合存储器堆叠](/images/3D/引线键合存储器堆叠.png)

图片来源：`[PDF]` p.349，Figs. 7.7-7.8。

商业例子 / PDF 收录方案：

1. Samsung 为 Apple iPhone 制造的 8 层 flash die stack：芯片厚度约 `55-70 μm`，采用外围 wire bonding；封装含基板厚度约 `0.93 mm`，芯片堆叠高度约 `670 μm`（p.344，Fig. 7.6）。
2. Samsung `Portable SSD T3 2 TB`：每个封装容纳 16 颗 48-layer V-NAND die，单颗 die 厚度约 `40 μm`，通过 wire bonding 堆叠在 coreless organic substrate 上（pp.344、349）。

### 1.2 Face-to-face / back-to-back 芯片堆叠并由封装级引出

这一类拓扑的共同特征是：芯片之间存在 face-to-face 或 back-to-back 的垂直堆叠界面，但最终仍通过 wire bond、solder ball、C4 bump、TGV / TPV 或 fan-out RDL 引出到下一级互连。

```txt
塑封料
→ 上层 die
→ face-to-face solder bumps / hybrid-bond interface
  或 back-to-back die attach interface
→ 下层 die
→ package-level escape：wire bond / solder balls / C4 bumps / TGV / TPV / fan-out RDL
→ package substrate / glass carrier / fan-out carrier
→ BGA solder balls
→ PCB
```

#### 1.2.1 Face-to-face 并通过引线或焊球引出

```txt
塑封料 / heat spreader
→ 上层 die，有源面朝下
→ microbumps / hybrid-bond interface
→ 下层 die，有源面朝上，外围焊盘或 RDL 保持可引出
→ die attach，或下层 die 的 fan-out / TGV / TPV 结构
→ wire bond / solder balls / C4 bumps
→ package substrate
```

![Sony 面对面堆叠并通过引线引出](/images/3D/面对面-引线.png)

图片来源：`[PDF]` p.350，Fig. 7.9。

![面对面键合并通过焊球连接基板](/images/3D/面对面-焊球.png)

图片来源：`[PDF]` p.351，Fig. 7.12。

商业例子 / PDF 收录方案：

1. Sony PlayStation `CXD53135GG`：5-chip stack；DDR2、spacer 和 DDR2 采用 wire bond 堆叠，wide-I/O SDRAM 与 processor 采用 face-to-face solder-bumped flip chip，再由 processor wire bond 引出（pp.344-350）。
2. Sony backside-illuminated CMOS image sensor（BI-CIS）：BI-CIS 与 processor face-to-face hybrid bonding，processor 再通过 wire bond 引出（pp.345、350）。
3. IME `memory-on-logic`：memory 通过 C2 bump face-to-face 连接 logic，logic 再通过 SnAgCu solder ball 接到刚性或柔性基板（pp.346、351）。
4. Georgia Tech `router + TGV glass`：多颗芯片 face-to-face 连接 router，信号经 fan-out RDL 和 through-glass via 引出（pp.347、352）。
5. Fraunhofer IZM `MEMS + ASIC`：MEMS 与 ASIC face-to-face 连接，ASIC 侧可通过 solder ball 或 wire bond 引出（pp.347、352）。
6. ASIC-on-FPGA：ASIC 以 `40 μm` pitch microbump face-to-face 连接 FPGA，FPGA 再以 C4 bumps 连接封装基板（pp.347、353）。
7. Amkor `Double-POSSUM`：daughter dies → mother die → grandma die 的两级嵌套堆叠，层间分别使用 C2 / C4 bumps（pp.347-353）。
8. 3D embedded MEMS/controller：MEMS 与 controller 近 face-to-face 连接，使用 fan-out RDL、TPV 和 solder balls 引出（pp.348、354）。

#### 1.2.2 Back-to-back 并通过引线引出

```txt
塑封料
→ 上层 die，有源面朝上；顶面焊盘通过 wire bond 接基板
→ die attach，形成 back-to-back 界面
→ 下层 die，有源面朝下
→ flip-chip bumps + underfill
→ package substrate
→ BGA solder balls
→ PCB
```

![Intel PMB9955 背对背堆叠](/images/3D/背对背-引线.png)

图片来源：`[PDF]` p.351，Fig. 7.11。

商业例子：

1. Intel `PMB9955` modem chipset（用于 iPhone XR）：baseband AP 倒装在 3-layer ETS 上，DRAM 贴在 AP 背面并 wire bond 到 ETS（pp.346、351）。

### 1.3 Face-to-back fan-out 堆叠

这一类拓扑的共同特征是：上层芯片连接到下层 fan-out package 的背面，垂直通路由 TMV / TPV 与上下 RDL 完成。

```txt
塑封料
→ 顶层 die，有源面朝下
→ microbumps
→ 下层 fan-out package 的背面 RDL
→ TMV / TPV，穿过下层 EMC
→ 下层一颗或多颗 face-down die + EMC
→ 下层 fan-out RDL
→ C4 bumps + underfill
→ package substrate
```

![面对背 fan-out 堆叠](/images/3D/面对背.png)

图片来源：`[PDF]` p.354，Fig. 7.18。

商业方案 / PDF 收录方案：

1. 3D fan-out face-to-back：上层 Chip 3 倒装到下层 fan-out package 背面，使用 TMV、上下 RDL 和 solder balls 完成垂直互连（pp.352-355）。
2. SPIL `face-to-back 3D package`：顶层芯片经 microbump、fan-out RDL 和 TMV 连接下层芯片，底部以 C4 bumps 连接 package substrate（p.355，Fig. 7.19）。

### 1.4 SiP 中的嵌入式芯片（face-to-face）

这一类拓扑的共同特征是：芯片嵌入 flexible / organic SiP substrate 的腔体中，并与上方器件形成 face-to-face 功能界面。

```txt
塑封料
→ 表面安装的 sensor / IC / passive components
→ 焊点或细间距互连
→ flexible / organic SiP substrate
→ 嵌入基板腔体中的 silicon die，其有源面朝向上方器件，形成 face-to-face 功能界面
→ 基板底部外部焊盘 / BGA solder balls
→ PCB
```

![Fujikura WABE 嵌入式芯片 SiP](/images/3D/嵌入式芯片.png)

图片来源：`[PDF]` p.356，Fig. 7.20。

商业方案：

1. Fujikura `WABE`（wafer and board level embedded package）：将 U1 嵌入柔性基板，与上方 sensor face-to-face；封装由 `3.5 mm × 3.5 mm` 缩至 `2.5 mm × 2.5 mm`（pp.355-356）。

### 1.5 Package-on-Package（PoP）

PoP 的共同特征是：顶部封装通常承载 memory stack，底部封装承载 application processor / chiplets / PMIC，两个封装通过焊球、Cu-core balls、TIV / TMV 或中介层连接。

![PoP 总括拓扑](/images/3D/PoP总括拓扑-Fig7.2.png)

图片来源：`[PDF]` p.345，Fig. 7.2。

#### 1.5.1 基于倒装芯片底部封装的 PoP

```txt
塑封料
→ 顶部 memory die stack，通常正面朝上并以 wire bond 连接
→ top-package coreless substrate
→ PoP solder balls / Cu-core balls / TSV-less interposer
→ application processor，正面朝下
→ C4 / C2 bumps + underfill
→ bottom-package build-up substrate / ETS
→ BGA solder balls
→ PCB
```

![Apple A9 倒装芯片 PoP](/images/3D/PoP-倒装.png)

图片来源：`[PDF]` p.357，Fig. 7.21。

商业例子 / PDF 收录方案：

1. Apple `A9 + LPDDR4` PoP：A9 倒装在 `2-2-2` build-up substrate，上层为 wire-bonded LPDDR4；PDF 原文将其写作 iPhone 6 Plus 截面（pp.356-357）。
2. Qualcomm `Snapdragon 805` + Samsung Galaxy：C2 bump + TC-NCP 连接 Shinko `MCeP` 基板，上层封装通过 Cu-core balls 连接（pp.356、358）。
3. NXP `3D PoP`：底部 4-layer ETS 承载 processor，上层承载 memory，封装间使用双层 solder balls 与 TSV-less interposer（pp.356、358）。
4. Shinko `Cu-core-ball PoP`：底部 memory、顶部 ASIC，层间采用 Cu-core solder balls（pp.356、359）。

#### 1.5.2 基于扇出底部封装的 PoP

```txt
塑封料
→ 顶部 memory package / HBM package
→ top-package substrate / laminated TSV-less interposer(有机层压转接板)
→ PoP solder balls，或 TIV / TMV 穿过底部 EMC
→ 底部封装中的 application processor / chiplets / PMIC，嵌入 EMC
→ fan-out RDL / RDL-first substrate
→ BGA solder balls
→ PCB
```

![Apple TSMC InFO PoP](/images/3D/PoP-扇出.png)

图片来源：`[PDF]` p.360，Fig. 7.26。

商业例子 / PDF 收录方案：

1. STATS ChipPAC `3D fan-out PoP`：底部为约 `450 μm` 厚 AP eWLB，顶部为 wire-bonded memory package（pp.357、359）。
2. Apple / TSMC `InFO-WLP PoP`：PDF 列出 A10、A11、A12、A13、A14 共用相近平台；A12 采用 7 nm、3 层 RDL，并在底部集成 flip-chip IPD（pp.357-360）。
3. TSMC `fan-out chiplet + memory/HBM PoP`：底部为 4-6 层 RDL-first chiplet package，顶部 memory/HBM 通过 laminated TSV-less interposer 连接（pp.358、360）。
4. Samsung smartwatch `ePoP`：上层含 2 DRAM、2 NAND、1 controller；下层 AP 与 PMIC 并排采用 fan-out panel-level packaging（pp.358-361）。
5. IME `RDL-first fan-out PoP`：processor 通过 microbump 连接预制 RDL substrate，顶部 DRAM 直接连接底部封装背面 RDL（pp.359-361）。

## 2. 3D IC Integration：TSV 或混合键合高密度堆叠

3D IC Integration 的共同特征是：垂直堆叠是通过 TSV、microbump 或 hybrid bonding 形成高密度的 chip-to-chip 互连。书中把 3D IC Integration 概括成三种基本结构：HBM memory stack、memory-on-logic with TSV，以及 bumpless hybrid bonding with TSV。

![3D IC Integration 总括拓扑](/images/3D/3DIC集成总括拓扑-Fig7.30.png)

图片来源：`[PDF]` p.362，Fig. 7.30。

### 2.1 HBM memory cube

HBM 的共同特征是：多层 DRAM 通过 TSV 与 C2 microbumps 垂直堆叠在 logic base die 上，形成高带宽存储器堆叠；随后 HBM stack 再连接到 2.5D interposer 或其他高密度载体。

```txt
mold / 可选 heat spreader
→ 多层薄化 DRAM die
→ 每层之间：TSV + C2 microbumps + NCF（非导电胶膜，兼作 underfill）
→ die，含 TSV 与底部 RDL
→ microbumps
→ passive silicon interposer，或其他下一级高密度载体
→ C4 bumps + build-up package substrate
→ BGA solder balls
→ PCB
```

![HBM HBM2 HBM2E 规格与结构](/images/3D/HBM规格.png)

图片来源：`[PDF]` p.363，Fig. 7.31。图中的 HBM3 数值是该书 2021 年出版时的预期值，仅作为现行标准参考。

![HBM TCB-NCF 组装](/images/3D/HBM组装.png)

图片来源：`[PDF]` p.364，Fig. 7.33。

商业例子 / PDF 收录方案：

1. SK hynix `HBM`：PDF 记载首个 HBM memory cube 于 2013 年由 Hynix 制造（pp.363-364）。
2. Samsung 与 SK hynix `HBM / HBM2 / HBM2E`：PDF 称两家公司当时是 HBM 模组的 HVM 供应商；Micron 当时处于进入意愿阶段（pp.362-364）。
3. Samsung / SK hynix `TCB-NCF HBM assembly`：C2 bumped DRAM 逐颗热压键合，NCF 同时承担预置底填材料功能；单颗芯片键合约需 `10 s`，吞吐量是主要挑战（pp.364-365）。
4. Toray `collective bonding`：先快速预键合，再一次完成多层堆叠后键合，以缩短 4-die stack 的组装时间（pp.365-366）。

### 2.2 TSV microbump CoC / memory-on-logic / active base die

这一类拓扑的共同特征是：上层 chip / memory / chiplet 通过 microbumps 连接到含 TSV 的下层 logic die 或 active base die；下层 TSV 再把信号、电源和地引到背面 RDL 或封装基板。

```txt
mold / 可选 heat spreader
→ 顶层 chip / chiplet / memory，有源面朝下
→ microbumps + underfill
→ 底层 logic die / active base die / active TSV interposer（含 CMOS devices 与 TSV）
→ C4 bumps
→ package substrate
→ BGA solder balls
→ PCB
```

多层 CoC 时重复“薄化芯片 → microbumps → TSV”单元。

![Intel Foveros 基于 TSV 的 CoC](/images/3D/CoC-TSV-Foveros.png)

图片来源：`[PDF]` p.370，Figs. 7.39-7.40。

商业例子 / PDF 收录方案：

1. Sony `ISX014` stacked camera sensor：BI-CIS 位于 processor 上方，边缘 TSV 将信号引至 processor，再由 wire bond 引出（pp.365-367）。
2. AMD / UCSB active-interposer concept：CPU chiplet、多个 GPU chiplet 与 HBM 集成在带 CMOS 的 active TSV interposer 上（pp.366、368）。
3. Samsung `X-Cube`：2020 年发布，memory 位于带 TSV 的 logic / active TSV interposer 上方，层间采用 C2 microbump（pp.366、369）。
4. Intel `Foveros`：chiplets / SoC face-to-face 连接 22FFL active base die；PDF 还收录 `ODI Type 1/2/3` 与 `MDIO` die-to-die interface（pp.366-370）。
5. Intel `Lakefield` mobile processor：2020 年出货，10 nm compute die 堆叠在 22FFL TSV base die 上，是 PDF 给出的 Foveros 具体量产型号（pp.367、370）。
6. IME `memory + logic CoC test vehicle`：两颗带 TSV 的芯片通过 `25 μm` pitch microbumps 连接；TSV 直径约 `15 μm`、深度约 `200 μm`（pp.367、371-372）。

### 2.3 带 TSV 的 bumpless hybrid bonding CoC

这一类拓扑与第 2.2 节相同，但芯片间界面从 `microbumps + underfill` 替换为无凸点混合键合。它的目标是进一步缩小互连 pitch、降低堆叠高度，并消除传统微凸点界面的部分寄生和可靠性限制。

```txt
mold / 可选 heat spreader
→ 顶层 chip / chiplet / memory，有源面朝下
→ Cu-Cu + dielectric-dielectric hybrid-bond interface
→ 底层 logic die / base die，含 TSV
→ 背面 RDL 
→ BGA solder balls
→ PCB
```

![TSMC SoIC 带 TSV 混合键合](/images/3D/混合键合-带TSV-SoIC.png)

图片来源：`[PDF]` p.373，Fig. 7.44。

商业方案 / PDF 收录方案：

1. Intel `Foveros Hybrid Bonding`：以 Cu-Cu hybrid bonding 取代 Foveros 的 microbump 界面；PDF 收录的是 2020 年公布的技术路线（pp.368、372）。
2. TSMC `3DFabric / SoIC`：frontend SoIC 以 bumpless hybrid bonding 将上层 chip 连接到带 TSV 的下层 chip；backend 可组合 `SoIC + InFO` 或 `SoIC + CoWoS`（pp.368、373）。
3. TSMC `bumpless HBM stacking`：PDF 展示 4-Hi、8-Hi、12-Hi 等 SoIC / hybrid-bonded memory stack 方案（pp.368、373）。
4. Arm `face-to-face / face-to-back hybrid bonding`：带 TSV 芯片的两类无凸点堆叠及其热分析验证（pp.368-369、374）。

### 2.4 不带 TSV 的 bumpless hybrid bonding CoC（特殊案例）

这一类不满足本书开头对 3D IC Integration 的严格 TSV 定义，但书中仍把它放在 3D IC Integration 章节下讨论。判断时应把它看作“无 TSV、但 chip-to-chip hybrid bonding 密度已经接近 IC 级垂直互连”的边界案例。

```txt
mold / 可选 heat spreader
→ 顶层 die，有源面朝下
→ Cu-Cu + dielectric-dielectric hybrid-bond interface
→ 较大的底层 processor / logic die，有源面朝上且不使用 TSV
→ 底层 die 外围焊盘，通过 wire bond 或封装 RDL 引出
→ package substrate 
→ BGA solder balls
→ PCB
```

![Sony IMX260 无 TSV 混合键合](/images/3D/混合键合-无TSV-Sony.png)

图片来源：`[PDF]` p.374，Fig. 7.47。

商业例子：

1. Sony `IMX260` backside-illuminated CMOS image sensor：无 TSV 的 BI-CIS 与 ISP 通过 Cu-Cu + SiO2-SiO2 hybrid bonding 连接；用于 Samsung Galaxy S7，2016 年出货。PDF 将其列为当时已 HVM 的 bumpless hybrid-bonded 产品（pp.369-371、374）。

## 3. 拓扑提取结论

书中 pp.343-374 已经能直接提取典型 3D 拓扑，不需要完全依赖厂商路线反推结构：

1. 3D IC Packaging 的拓扑分歧主要来自封装级引出方式：wire bond、solder bump、PoP solder balls。
2. 3D IC Integration 的拓扑分歧主要来自芯片间界面：`TSV + microbumps + underfill` 或 `TSV + bumpless hybrid bonding`。

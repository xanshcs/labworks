# Builds — office kit, 4 workplaces

Common to all four: desktop PC on Intel LGA1700 with DDR4, Windows 11 Pro
(retail licence), at least 16 GB RAM, 1 TB NVMe SSD, monitor, keyboard and
mouse. All prices are from Shop.kz, taken on 2026-11-15 (see budget.csv).

**Why one platform, four configurations.** The director's instinct to
standardise is right for support, spare parts and imaging, but wrong for the
configuration: each role runs out of a different resource first. So the
platform is shared and the money is moved between roles.
**Platform trade-off.** LGA1700 with DDR4 is the end of a platform line
(newer Intel boards use DDR5), but board and memory are cheaper, and LGA1700
accepts 12th–14th generation CPUs, so a CPU upgrade stays possible.

## Build 1 — accountant
**Load:** 1C, large Excel workbooks, bank client, a few browser tabs.
**Bottleneck:** disk latency and single-core CPU speed; 1C file mode mostly
uses one core, so more cores do not help.
**Trade-off:** no discrete GPU (integrated graphics are enough), 16 GB RAM
(the hard minimum) with one free memory slot, money goes into a strong
single-thread CPU and a fast SSD.

| Part | Model | KZT |
|---|---|---|
| CPU | Intel Core i5-12400 LGA1700 OEM | 87,500 |
| Cooler | ID-Cooling DK-03 (OEM CPU has no cooler) | 3,200 |
| Motherboard | Gigabyte H610M H DDR4 | 46,690 |
| RAM | 16 GB DDR4 3200 Hiksemi Hiker | 63,990 |
| SSD | MSI Spatium M470 Pro 1 TB | 96,990 |
| PSU | MSI MAG A500N-H 500 W | 14,590 |
| Case | DeepCool CC560 WH V2 | 27,990 |
| Monitor | iiyama ProLite XU2493HSU-B7 24" IPS | 65,990 |
| OS | Windows 11 Professional retail | 123,990 |
| Keyboard + mouse | TODO | TODO |

**Total:** 530,930 KZT before keyboard and mouse (budget.csv).
**Note:** the PCIe 4.0 SSD is faster than this role needs; a cheaper 1 TB
SSD would free money for other machines. TODO: price one and decide.

## Build 2 — sales manager
**Load:** browser CRM with many tabs, Excel, messengers, hours of video calls,
often all at once.
**Bottleneck:** memory.
**Trade-off:** same CPU and platform as the accountant (the CPU idles in this
role); the saving goes into 32 GB (2 × 16 GB, dual channel) and a 27"
monitor for side-by-side windows.
**Parts to price:** as Build 1, plus a second 16 GB stick and a 27" IPS monitor.
**Target:** about 520,000 KZT hardware and monitor, excluding Windows and
peripherals. **Total:** TODO (budget.csv rows TODO)

## Build 3 — web developer
**Load:** IDE, several browser windows with devtools, Docker and virtual
machines, local database, builds and tests.
**Bottleneck:** RAM first, then core count.
**Trade-off:** more cores (Core i5-12600 or i7-12700) and 32 GB on a board
with four memory slots, so 64 GB is possible later; integrated graphics
(no GPU needed); a good monitor, since text is read all day.
**Parts to price:** CPU 12600 or 12700, B660 DDR4 board with 4 slots,
2 × 16 GB, 1 TB SSD, cooler, PSU, case, 24" or 27" monitor.
**Target:** about 640,000 KZT. **Total:** TODO (budget.csv rows TODO)

## Build 4 — designer
**Load:** Photoshop, Illustrator, Figma, large layered files, possibly light
video or 3D, colour-critical work.
**Bottleneck:** GPU and RAM, and the monitor: a screen with poor colour
makes the rest of the machine irrelevant.
**Trade-off:** mid-range discrete GPU, 32 GB RAM, a mid-range CPU (F-series,
no integrated graphics, because a GPU is installed) and the largest share of
the budget on an IPS monitor with stated sRGB coverage.
**Parts to price:** Core i5-12400F, B660 DDR4 board, 2 × 16 GB, 1 TB SSD,
GPU (RTX 3050 or 4060 class), a PSU sized for the GPU, case, 27" IPS monitor
with sRGB coverage in the specification.
**Target:** about 750,000 KZT. **Total:** TODO (budget.csv rows TODO)

## Budget check
Budget 3,000,000 KZT. Reserve ~5% (150,000) → 2,850,000. Four Windows
licences: 4 × 123,990 = 495,960 (16.5% of the budget). Left for hardware,
monitors and peripherals: 2,354,040. The targets above are planning figures,
not prices; the real totals come from budget.csv.
**Grand total:** TODO KZT of 3,000,000.

## Why not four identical machines
TODO: one paragraph with real numbers: what four copies of the designer build
would cost against the budget, and what the accountant would be paying for
and never use.

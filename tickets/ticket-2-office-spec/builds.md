# Builds — office kit, 4 workplaces

Common to all four: desktop PC on Intel LGA1700 with DDR4, Windows 11 Pro
(retail licence), at least 16 GB RAM, 1 TB NVMe SSD, monitor. Prices are
from Shop.kz, taken on 2026-11-15 (see budget.csv). Keyboards and mice are
not priced; they are covered by the 5% reserve.

**Why one platform, four configurations.** Standardising is right for
support and spare parts, wrong for the configuration: each role runs out of
a different resource first. So the platform is shared and the money moves
between roles.
**Platform trade-off.** LGA1700 with DDR4 is the end of a platform line
(newer boards use DDR5), but board and memory are cheaper and LGA1700 still
allows a CPU upgrade.

## Build 1 — accountant
**Load:** 1C, large Excel workbooks, bank client, a few browser tabs.
**Bottleneck:** disk latency and single-core CPU speed; 1C file mode mostly
uses one core, so more cores do not help.
**Trade-off:** no discrete GPU (integrated graphics are enough), 16 GB RAM
(the hard minimum) with one free memory slot; the money goes into a strong
single-thread CPU and a fast SSD. The PCIe 4.0 SSD is faster than this role
needs, so a cheaper 1 TB SSD would be the first saving if the budget tightens.
**Total:** 530,930 KZT (budget.csv, rows with role Accountant)

## Build 2 — sales manager
**Load:** browser CRM with many tabs, Excel, messengers, hours of video calls,
often all at once.
**Bottleneck:** memory.
**Trade-off:** same CPU and platform as the accountant, because the CPU
idles in this role; the saving goes into 32 GB (2 × 16 GB, dual channel).
I kept the 24" monitor; a 27" would be more comfortable for side-by-side
windows but was not priced.
**Total:** 594,920 KZT (budget.csv, rows with role Sales)

## Build 3 — web developer (specified, not priced)
**Load:** IDE, several browser windows with devtools, Docker and virtual
machines, local database, builds and tests.
**Bottleneck:** RAM first, then core count.
**Trade-off:** more cores (Core i5-12600 or i7-12700 class) and 32 GB on a
board with four memory slots so 64 GB is possible later; integrated graphics.
**Planning target:** about 640,000 KZT.

## Build 4 — designer (specified, not priced)
**Load:** Photoshop, Illustrator, Figma, large layered files, colour-critical
work.
**Bottleneck:** GPU and RAM, and the monitor: a screen with poor colour
makes the rest of the machine irrelevant.
**Trade-off:** mid-range discrete GPU, 32 GB RAM, F-series CPU (no integrated
graphics, since a GPU is installed), and the largest share of the budget on
an IPS monitor with stated sRGB coverage.
**Planning target:** about 750,000 KZT.

## Budget check
Budget 3,000,000 KZT. The two priced builds total 1,125,850 KZT, leaving
1,874,150 KZT for the other two and a 5% reserve (150,000). The targets for
builds 3 and 4 above total 1,390,000, which fits, but they are planning
figures, not prices. Four Windows licences cost 4 × 123,990 = 495,960 KZT,
about 16.5% of the budget.

## Why not four identical machines
Four copies of the sales build would cost 4 × 594,920 = 2,379,680 KZT and
leave the designer without a GPU and the developer without 32 GB and
extra cores, while the accountant would pay for a second memory stick and
a monitor upgrade he never uses.

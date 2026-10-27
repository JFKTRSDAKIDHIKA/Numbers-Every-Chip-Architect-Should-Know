# Numbers Every Chip Architect Should Know

A running collection of the numbers that matter when designing chips —
the ones you should be able to recall from memory, similar in spirit to
"Latency Numbers Every Programmer Should Know", but for the hardware world.

## The Numbers

| # | Number | Value | Notes |
|---|--------|-------|-------|
| 1 | DUV reticle limit | 26 mm × 33 mm (858 mm²) | Maximum exposure field of an ArF immersion (DUV) scanner. Any die larger than this must be stitched or built as a multi-die package. |
| 2 | TSMC 7nm HD 6T SRAM bitcell area | 0.027 µm² / bit | High-density (HD) 6-transistor bitcell of TSMC N7. Sets the floor for on-chip SRAM density at that node. |
| 3 | Intel 18A logic HP (5T) density | 169.9 MTr/mm² (measured) vs 163.7 MTr/mm² (PDK) | 5-track HP library, 177 nm cell height × 49 nm CGP. Measured density runs ~3.8% above PDK. Full pitch/material/PDK comparison below. |

## 1. DUV Reticle Limit — 26 × 33 mm²

The stepper/scanner exposes one reticle field at a time, and the field size is
bounded by the reticle itself: a 6" × 6" mask with a 4× reduction ratio yields
a maximum field of **26 mm × 33 mm (858 mm²)** on the wafer.

Practical implications:

- The largest single die printed in one shot — and therefore the practical
  upper bound on monolithic chip area — is roughly **26 mm × 33 mm ≈ 858 mm²**.
- Dies beyond that size require **reticle stitching** (multiple exposures per
  die) or splitting the product into chiplets on an interposer/substrate.
- Smaller process nodes do not change this limit; it is set by lithography
  optics and mask size, not by the transistor density.

## 2. TSMC 7nm HD 6T SRAM Bitcell — 0.027 µm² / bit

The high-density (HD) 6-transistor SRAM bitcell in TSMC's N7 (7nm) process
occupies **0.027 µm² per bit**.

Practical implications:

- This is the *bitcell* area only. Real macros add sense amps, decoders, wordline
  drivers, I/O and wiring overhead — expect roughly **1.5×–2×** the pure bitcell
  area for a complete SRAM macro, depending on aspect ratio and column muxing.
- Density rules of thumb: **1 Mbit ≈ 0.027 mm²** of bitcell area
  (≈ 0.04–0.05 mm² of actual macro), and **1 mm² of SRAM ≈ 37 Mbit** of raw bitcell.
- Compare across nodes by bitcell area, not by node name: it is the number that
  actually drives area budgets in a cache/memory hierarchy.

## 3. Intel 18A — Pitches, Materials, Density

Transcribed from provided figures; abbreviations and table headers follow the
original images.

### 3.1 Minimum measured pitch — BM layers

| BM layer | Minimum measured pitch |
|----------|------------------------|
| BM0 | 176 nm |
| BM1 | 291 nm |
| BM2 | 477 nm |
| BM3 | 2890 nm |
| BM4 | 2950 nm |
| BM5 | 5840 nm |

### 3.2 Minimum measured pitch — metal M0–M14

| Layer | Pitch | Layer | Pitch | Layer | Pitch |
|-------|-------|-------|-------|-------|-------|
| M0 | 36 nm | M5 | 78 nm | M10 | 80 nm |
| M1 | 49 nm | M6 | 79 nm | M11 | 116 nm |
| M2 | 36 nm | M7 | 77 nm | M12 | 117 nm |
| M3 | 40 nm | M8 | 78 nm | M13 | 311 nm |
| M4 | 40 nm | M9 | 78 nm | M14 | 155 nm |

### 3.3 Contact level materials

| Contact | Liner | Fill |
|---------|-------|------|
| S/D contact | Ti/Mo | W |
| Gate contact | Mo | W |
| Contact to M0 | Mo | W |
| Nano-TSV contact | Mo | W |

### 3.4 Metal layer materials — Intel 18A vs SF2

| Layer | Liner 18A | Liner SF2 | Fill 18A | Fill SF2 | Top ES 18A | Top ES SF2 |
|-------|-----------|-----------|----------|----------|------------|------------|
| M9 | Nb-based | TaN / Co | Cu | Cu | - | - |
| M8 | Nb-based | TaN / Co | Cu | Cu | - | - |
| M7 | Nb-based | TaN / Co | Cu | Cu | - | - |
| M6 | Nb-based | TaN / Co | Cu | Cu | - | - |
| M5 | Nb-based | TaN / Co | Cu | Cu | - | Al-based ES |
| M4 | Co | TaN / Co | Cu | Cu | Al-based ES | Al-based ES |
| M3 | Co | TaN / Co | Cu | Cu | Al-based ES | Al-based ES |
| M2 | Co | TaN / Co | Cu | Cu | Al-based ES | Al-based ES |
| M1 | Co / Ru | TaN / Co | Cu | Cu | Al-based ES | Al-based ES |
| M0 | Co / Ru | TaN / Co | Cu | Cu | Al-based ES | Al-based ES |

### 3.5 PTL-U / Intel 18A measurements vs PDK

A. **Logic: HP — Cougar Cove (P)**

| Metric | Measured | PDK |
|--------|----------|-----|
| Cell Height | 177 nm | 180 nm |
| Gate Pitch | 49 nm | 50 nm |
| M0 Height | 35 nm | - |
| M0 Top CD | 25 nm | - |
| M0 Bottom CD | 20 nm | - |
| M0 Pitch | 37 nm | 36* nm |

B. **Logic: HP — Darkmont (LP-E)**

| Metric | Measured | PDK |
|--------|----------|-----|
| Cell Height | 177 nm | 180 nm |
| Gate Pitch | 49 nm | 50 nm |
| M0 Height | 34 nm | - |
| M0 Top CD | 24 nm | - |
| M0 Bottom CD | 18 nm | - |
| M0 Pitch | 35 nm | 36* nm |

C. **SRAM: 1:2:2 HCC — Cougar Cove (P) L2**

| Metric | Measured | PDK |
|--------|----------|-----|
| Cell Height | 230 nm | 230 nm |
| Gate Pitch | 49 nm | 50 nm |

D. **SRAM: 1:2:2 HCC — Cougar Cove (P) L3**

| Metric | Measured | PDK |
|--------|----------|-----|
| Cell Height | 230 nm | 230 nm |
| Gate Pitch | 50 nm | 50 nm |

E. **I/O (Logic: HP) — (LP)DDR5 PHY**

| Metric | Measured | PDK |
|--------|----------|-----|
| Cell Height | 184 nm | 180 nm |
| Gate Pitch | "NO XTEM" | 50 nm |
| M0 Height | 36 nm | - |
| M0 Top CD | 38 nm | - |
| M0 Bottom CD | 29 nm | - |
| M0 Pitch | 76 nm | "2× relaxed" |

### 3.6 Logic density — Logic HP (5T)

| Metric | Measured | PDK |
|--------|----------|-----|
| Cell Height (CH) | 177 nm | 180 nm |
| Contacted Gate Pitch (CGP) | 49 nm | 50 nm |
| Tracks | 5 | 5.00 |
| NAND2 area | 0.0260 µm² | 0.0270 µm² |
| NAND2 density | 153.7 MTr/mm² | 148.1 MTr/mm² |
| SFF area | 0.1648 µm² | 0.1710 µm² |
| SFF density | 194.2 MTr/mm² | 187.1 MTr/mm² |
| Bohr density | 169.9 MTr/mm² | 163.7 MTr/mm² |

Notes:

- CH = Cell Height; CGP = Contacted Gate Pitch; CD = Critical Dimension;
  ES = Etch Stop.
- "\*" (in "36\*") and "2× relaxed" are kept as in the original figure.
- In the source figure, Top ES 18A is "-" for M7–M9 and Top ES SF2 is "-" for M6.
- Data transcribed by hand from images; some abbreviations and header wording
  follow the original figures.

## Contributing

Add a new section with the number, its value, and a one-line "why it matters".

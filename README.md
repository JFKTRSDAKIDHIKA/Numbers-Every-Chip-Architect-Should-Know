# Numbers Every Chip Architect Should Know

A running collection of the numbers that matter when designing chips —
the ones you should be able to recall from memory, similar in spirit to
"Latency Numbers Every Programmer Should Know", but for the hardware world.

## The Numbers

| # | Number | Value | Notes |
|---|--------|-------|-------|
| 1 | DUV reticle limit | 26 mm × 33 mm (858 mm²) | Maximum exposure field of an ArF immersion (DUV) scanner. Any die larger than this must be stitched or built as a multi-die package. |

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

## Contributing

Add a new section with the number, its value, and a one-line "why it matters".

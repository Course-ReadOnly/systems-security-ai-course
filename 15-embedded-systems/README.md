> **Generated ahead of schedule** (2026-07-27, per learner request). Revisit
> when actually reached.

# Stage 15 — Embedded Systems

**Time budget:** 4–6 weeks part-time / 2 weeks full-time

## Objectives

Optional branch (per ROADMAP.md's timeline notes) — real hardware,
constrained resources, no OS underneath you. Worth doing if
embedded/firmware/IoT security interests you; skippable if your goal is
purely software/AI/security track work, per the roadmap's own framing.

## Topics & resources

| # | Topic | Free Resource |
|---|---|---|
| 01 | ARM embedded fundamentals | [ARM Developer docs](https://developer.arm.com/documentation) |
| 02 | Practical embedded community | [embedded.fm](https://embedded.fm/) |
| 03 | STM32 ecosystem (free toolchain) | [STM32CubeIDE](https://www.st.com/en/development-tools/stm32cubeide.html) |

**Topics:** ARM, UART, SPI, I2C, DMA.

## Projects

| # | Project | Folder |
|---|---|---|
| 15.1 | Bootloader | `projects/15.1-bootloader/` |
| 15.2 | Small firmware project | `projects/15.2-firmware-project/` |
| 15.3 | UART driver | `projects/15.3-uart-driver/` |

**Note:** this stage requires actual hardware (an STM32 dev board or
similar) — specs assume you have one; if not, note that in STATUS.md
when you reach here rather than silently skipping.

# Changelog

All notable changes to the **4D_7S Library** will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

### [Unreleased]
* (Place your planned improvements here as you code them)
* Planned: Improve and integrate usage with SPI expanders like 74HC595
* Planned: Support for 1-digit 7-segment display will be added also.
* Planned: Full Arduino Support will be added also.
* Planned: Support for Common Anode displays via a configuration macro.

### Fixed
* (List bugs you've fixed since the 1.0.0 release)

## [1.0.0] - 2026-04-08

This is the **initial stable release** of the library, providing high-performance, bare-metal multiplexing for AVR-based systems.

### Added
* **Core Multiplexing Engine**: Implemented flicker-free 4-digit multiplexing using Timer 2 Interrupt Service Routine (ISR).
* **Architecture Support**: Added register-level compatibility for both modern AVRs (ATmega328P, 168, 2560) and legacy MCUs (ATmega8, 16, 32).
* **Zero-Delay Display Logic**: Integrated background refreshing, allowing for $O(1)$ constant-time performance without blocking the main loop.
* **Decimal Point (DP) Management**: Created a `dp_mask` system to allow individual control of decimal points across any of the four digits.
* **Integer Parsing**: Added automatic extraction of individual digits from 16-bit integers (0-9999).
* **Port Flexibility**: Introduced pointer-based port initialization to allow the use of any 8-bit GPIO port for segments and ground control.
* **Hardware Efficiency**: Leveraged direct SFR (Special Function Register) manipulation to bypass high-latency abstraction layers.
* **Safety Measure**: Added thread-safe (atomic) number extraction to prevent data corruption during high-frequency interrupts.
* **Documentation**: Initial release of the `README.md` including API references and hardware mapping.
* **Licensing**: Project released under the MIT License.

---

### [Internal Technical Notes]
* **Timer Frequency**: Pre-scaled to 1024 with a calculated OCR2A/OCR2 value based on `F_CPU` to maintain a consistent refresh rate.
* **Memory Footprint**: Optimized to utilize minimal SRAM by using `volatile uint8_t` pointers for port addresses.
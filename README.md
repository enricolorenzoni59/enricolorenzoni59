# Enrico Lorenzoni

**Engineering Tech Lead @ Cisco (London, UK) | C/C++ | Linux | Performance Engineering | DSP**

I'm a software engineer passionate about high-performance systems, low-level programming, software-defined radio, and real-time signal processing.

I enjoy solving problems at the intersection of hardware and software, optimizing critical paths, investigating subtle correctness issues, and building reliable systems.

## Selected Open Source Contributions

### [stream1090](https://github.com/mgrone/stream1090) — ADS-B / Mode S decoder

**48 merged pull requests** spanning DSP, CPU optimization, demodulation, error correction, concurrency, and cross-platform support.

Highlights:

- [Reduced DSP and demodulation CPU usage by 24% on Raspberry Pi 4 and 15% on Pi 5](https://github.com/mgrone/stream1090/pull/38), backed by reproducible benchmarks.
- [Implemented confidence-based error correction for Mode S messages](https://github.com/mgrone/stream1090/pull/24).
- [Made the multicore processing pipeline deterministic](https://github.com/mgrone/stream1090/pull/30).
- [Added macOS CI with Apple Clang and strict compiler warnings](https://github.com/mgrone/stream1090/pull/62).

### [libiio](https://github.com/analogdevicesinc/libiio) — Analog Devices IIO library

Contributions to command-line reliability, portability, and automated testing.

- [Fixed argument truncation and incomplete attribute writes](https://github.com/analogdevicesinc/libiio/pull/1596).
- [Restored CI formatting checks and error propagation](https://github.com/analogdevicesinc/libiio/pull/1599).
- [Fixed API test builds and added macOS emulator testing](https://github.com/analogdevicesinc/libiio/pull/1600).

### [readsb](https://github.com/wiedehopf/readsb) — ADS-B decoder

- [Fixed Clang compatibility issues and two latent bugs](https://github.com/wiedehopf/readsb/pull/141).
- [Restored the benchmark build targets](https://github.com/wiedehopf/readsb/pull/142).

### [Tvheadend](https://github.com/tvheadend/tvheadend) — TV streaming server

- [Fixed a locking issue on failed UUID assignment](https://github.com/tvheadend/tvheadend/pull/2083).
- [Fixed handling of relative IPTV encryption-key URLs](https://github.com/tvheadend/tvheadend/pull/1748).

### Other merged contributions

- **[dtv-scan-tables](https://github.com/tvheadend/dtv-scan-tables)** — [Updated Italian DVB-T frequency tables](https://github.com/tvheadend/dtv-scan-tables/pull/173).
- **[label-maker](https://github.com/burnmark-io/label-maker)** — [Updated dependencies for DYMO 11354 support](https://github.com/burnmark-io/label-maker/pull/1).

## Contributions Under Review

- **[Wavelog](https://github.com/wavelog/wavelog/pull/3990)** — Corrected DXCC award progress calculations, with an isolated container-based reproduction, synthetic fixtures, and regression testing.
- **[RTL-SDR Blog](https://github.com/rtlsdrblog/rtl-sdr-blog/pull/79)** — Per-stage gain control for R82xx tuners.
- **[RTL-SDR Blog](https://github.com/rtlsdrblog/rtl-sdr-blog/pull/83)** — Robust asynchronous handling of USB device disconnection.
- **[ANTSDR E200](https://github.com/MicroPhase/antsdr-fw-patch/pull/40)** — Dual-core CPU configuration.
- **[Airspy host tools](https://github.com/airspy/airspyone_host/pull/107)** — Improved USB device initialization.

## Earlier Technical Investigations

Some earlier contributions were submitted from my previous GitHub account, [enrico-samknows](https://github.com/enrico-samknows).

**[Boost.JSON — AddressSanitizer memory-boundary investigation](https://github.com/boostorg/json/pull/663)**

Investigated invalid pointer-pair handling during JSON serialization using Clang AddressSanitizer. The upstream discussion led to follow-up investigation and fixes by the maintainers. The original pull request was closed without merging.

## Technical Interests

`C` · `C++` · `Linux` · `Rust` · `Python` · `DSP` · `Concurrency` · `Low-level Debugging` · `Performance Optimization` · `SDR` · `Embedded Systems`

---

[GitHub Profile](https://github.com/enricolorenzoni59)

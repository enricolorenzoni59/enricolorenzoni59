# Enrico Lorenzoni

**Engineering Tech Lead @ Cisco (London, UK) | C/C++ | Linux | DSP | Performance Engineering**

I'm a software engineer interested in high-performance systems, real-time signal processing, software-defined radio, and low-level programming.

I enjoy understanding systems end-to-end, from hardware interfaces and signal processing to software architecture, performance optimization, testing, and reliability.

## Open Source Contributions

### [stream1090](https://github.com/mgrone/stream1090) — ADS-B / Mode S decoder

**48 merged pull requests** covering DSP, demodulation, CPU optimization, error correction, concurrency, and cross-platform support.

Selected contributions:

- [Reduced CPU usage by 24% on Raspberry Pi 4 and 15% on Pi 5](https://github.com/mgrone/stream1090/pull/38) through measured DSP and demodulator optimizations.
- [Implemented confidence-based error correction](https://github.com/mgrone/stream1090/pull/24) for Mode S extended squitter messages.
- [Made the multicore processing pipeline deterministic](https://github.com/mgrone/stream1090/pull/30).
- [Added macOS CI with Apple Clang and strict compiler warnings](https://github.com/mgrone/stream1090/pull/62).

### [libiio](https://github.com/analogdevicesinc/libiio) — Analog Devices IIO library

Contributions to reliability, cross-platform testing, and command-line tooling.

- [Fixed truncated CLI arguments and incomplete attribute writes](https://github.com/analogdevicesinc/libiio/pull/1596).
- [Restored CI formatting checks](https://github.com/analogdevicesinc/libiio/pull/1599).
- [Fixed API test builds and added macOS emulator tests](https://github.com/analogdevicesinc/libiio/pull/1600).

### [readsb](https://github.com/wiedehopf/readsb) — ADS-B decoder

- [Fixed Clang compatibility and uncovered two latent bugs](https://github.com/wiedehopf/readsb/pull/141).
- [Restored the benchmark build targets](https://github.com/wiedehopf/readsb/pull/142).

### [Tvheadend](https://github.com/tvheadend/tvheadend) — TV streaming server

- [Fixed an IPTV relative encryption-key URL issue](https://github.com/tvheadend/tvheadend/pull/1748).
- [Fixed locking on a failed UUID operation](https://github.com/tvheadend/tvheadend/pull/2083).

### Other merged contributions

- **[dtv-scan-tables](https://github.com/tvheadend/dtv-scan-tables)** — [Updated the Italian DVB-T frequency table](https://github.com/tvheadend/dtv-scan-tables/pull/173) to reflect the current spectrum plan.
- **[label-maker](https://github.com/burnmark-io/label-maker)** — [Updated dependencies](https://github.com/burnmark-io/label-maker/pull/1) for DYMO label support.

## Ongoing Upstream Contributions

Additional pull requests currently under review:

- **[RTL-SDR Blog](https://github.com/rtlsdrblog/rtl-sdr-blog)** — [Per-stage R82xx tuner gain control](https://github.com/rtlsdrblog/rtl-sdr-blog/pull/79) and [USB disconnect handling](https://github.com/rtlsdrblog/rtl-sdr-blog/pull/83).
- **[ANTSDR E200 firmware](https://github.com/MicroPhase/antsdr-fw-patch)** — [Dual-core CPU support](https://github.com/MicroPhase/antsdr-fw-patch/pull/40) and [reproducible SD image generation](https://github.com/MicroPhase/antsdr-fw-patch/pull/41).
- **[Airspy host tools](https://github.com/airspy/airspyone_host)** — [USB device initialization improvements](https://github.com/airspy/airspyone_host/pull/107).

## Technical Interests

`C` · `C++` · `Rust` · `Python` · `Linux` · `DSP` · `SDR` · `RF` · `Concurrency` · `Performance Optimization` · `Embedded Systems`

---

[View all my GitHub activity](https://github.com/enricolorenzoni59)

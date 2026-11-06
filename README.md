# Enrico Lorenzoni

**Engineering Tech Lead @ Cisco (London, UK) · C / C++ · Linux · Systems & Performance Engineering · DSP / SDR**

I work on the parts of a system where correctness is hard to see: memory lifetimes across threads, untrusted input parsers, undefined behaviour that only one compiler exposes, and hot paths where a few instructions per message add up. I like to find a bug, prove it with a minimal reproduction, fix it with the smallest change that is clearly correct, and leave behind the evidence a maintainer needs to merge it quickly.

**In open source:** 100 merged upstream pull requests across 9 projects, plus 6 firmware patches adopted by a hardware vendor. Most of them are in two real-time ADS-B / Mode S decoders, [readsb](https://github.com/wiedehopf/readsb) (C) and [stream1090](https://github.com/mgrone/stream1090) (C++).

---

## Flagship: [readsb](https://github.com/wiedehopf/readsb): hardening a production ADS-B decoder

readsb is the multi-threaded C decoder behind a large part of the community ADS-B feeder ecosystem. It is widely used by community feeders and aggregators, runs 24/7 and accepts network input in several protocols (Beast, AVR, SBS, ASTERIX, HTTP API).

**40 merged pull requests.** I audited it systematically with ASan, UBSan, TSan, Valgrind/Callgrind, a libFuzzer harness for the network input parsers and clang on macOS. Every PR comes with a reproduction, the impact, the fix and a before/after verification. The maintainer also made three more fixes that credit me as reporter: [a startup race](https://github.com/wiedehopf/readsb/commit/92ef55564aaaf893a9bb7c8f39a6fe83a13e78da), [a NULL-dereference race](https://github.com/wiedehopf/readsb/commit/975cd84f8dcbf1ef4d0ce89843d4baefbde0aa1e) and [malformed UUID handling](https://github.com/wiedehopf/readsb/commit/571b334367e9cf0f79af54640e337d479be669a7).

| Area | Representative fixes |
|---|---|
| **Memory safety on network-facing input** | [Out-of-bounds read and write in the HTTP API query parser](https://github.com/wiedehopf/readsb/pull/165) · [Stack buffer overflow from `?circle=1,2,3,4`](https://github.com/wiedehopf/readsb/pull/166) · [Stack overflow when a bind address resolves to more than 16 addresses](https://github.com/wiedehopf/readsb/pull/199) · [ASTERIX records reading into the next record and creating phantom aircraft](https://github.com/wiedehopf/readsb/pull/174) |
| **Concurrency and object lifetime** | [Use-after-free race between the JSON writer and client teardown](https://github.com/wiedehopf/readsb/pull/167), with a [TSan follow-up](https://github.com/wiedehopf/readsb/pull/167#issuecomment-6416473033) that led to maintainer fixes · [Use-after-free after a serial Beast device disconnects](https://github.com/wiedehopf/readsb/pull/177) · [Startup SIGSEGV race between upkeep and decode threads](https://github.com/wiedehopf/readsb/pull/178) (fixed upstream, credited) · [Double `close()` that can close a descriptor reused by another thread](https://github.com/wiedehopf/readsb/pull/171) |
| **Protocol correctness** | [ASTERIX high-precision time up to 1 s off, so valid positions were discarded](https://github.com/wiedehopf/readsb/pull/164) · [I021/220 compound item misaligning every later field](https://github.com/wiedehopf/readsb/pull/194) · [SBS emergency and ident flags read from the wrong field](https://github.com/wiedehopf/readsb/pull/175) · [One address-less record dropping a whole ASTERIX feed](https://github.com/wiedehopf/readsb/pull/186) · [Impossible block lengths silently desynchronising a stream](https://github.com/wiedehopf/readsb/pull/187) |
| **Performance (measured)** | [Beast frame delimiter fast path: −3% total instructions, `memchr` removed from the profile](https://github.com/wiedehopf/readsb/pull/181) · [Beast timestamp and payload decode without per-byte loops: −30% in `decodeBinMessage()`, −2.1% overall](https://github.com/wiedehopf/readsb/pull/184). Both were measured with Callgrind instruction counts, so the numbers do not depend on machine noise. |
| **Portability and toolchains** | [Clang build fix that uncovered a C11 atomics misuse and a function returning failure on success](https://github.com/wiedehopf/readsb/pull/141) · [macOS epoll→kqueue shim leaving stale filters and spinning a thread at 100%](https://github.com/wiedehopf/readsb/pull/202) · [Misaligned 64-bit loads in the hash function on every API refresh](https://github.com/wiedehopf/readsb/pull/180) |
| **Defence in depth** | [Command socket never got its intended 0600 mode](https://github.com/wiedehopf/readsb/pull/189) · [JSON injection through the PROXY protocol header](https://github.com/wiedehopf/readsb/pull/198) · [Non-finite values reaching `aircraft.json` and breaking every consumer](https://github.com/wiedehopf/readsb/pull/185) · [A series of signed-shift and float→int UB fixes](https://github.com/wiedehopf/readsb/pulls?q=is%3Apr+author%3Aenricolorenzoni59+is%3Amerged) that make full sanitizer builds of the decoder possible |

---

## [stream1090](https://github.com/mgrone/stream1090): C++ ADS-B / Mode S demodulator

*Collaborator (write access)* · **50 merged pull requests** across DSP, demodulation, error correction, concurrency, SDR back-ends and CI.

- **Performance:** [cut demodulator and DSP CPU by 24% on a Raspberry Pi 4 and 15% on a Pi 5](https://github.com/mgrone/stream1090/pull/38), with reproducible benchmarks. Also a [branchless CRC update](https://github.com/mgrone/stream1090/pull/27) and [CRC error-table lookups answered from an occupancy bitmap](https://github.com/mgrone/stream1090/pull/45).
- **Error correction:** [repair extended squitters by solving for the least confident bits](https://github.com/mgrone/stream1090/pull/24), and [fixed collisions in the DF17 error table](https://github.com/mgrone/stream1090/pull/7).
- **False-positive control:** [a deterministic white-noise test](https://github.com/mgrone/stream1090/pull/65), with address-parity frames trusted [only on repetition](https://github.com/mgrone/stream1090/pull/67), so noise cannot create aircraft.
- **Concurrency:** [made the multicore staged pipeline deterministic](https://github.com/mgrone/stream1090/pull/30), and [made USB/FIFO sample loss visible and bounded](https://github.com/mgrone/stream1090/pull/74).
- **DSP:** [fixed the 2.56 → 8 MHz interpolation](https://github.com/mgrone/stream1090/pull/32), [kept the FIR shape when taps do not fit Q15](https://github.com/mgrone/stream1090/pull/86), and [improved the 10 → 24 MHz filtering](https://github.com/mgrone/stream1090/pull/40).
- **Engineering hygiene:** [macOS CI with Apple Clang and fatal warnings](https://github.com/mgrone/stream1090/pull/62), and [per-backend translation units for preset dispatch](https://github.com/mgrone/stream1090/pull/77).

---

## SDR hardware and driver stack

- **[libiio](https://github.com/analogdevicesinc/libiio)** (Analog Devices): [fixed CLI argument truncation and silently incomplete attribute writes](https://github.com/analogdevicesinc/libiio/pull/1596), [restored the CI formatting checks and their failure propagation](https://github.com/analogdevicesinc/libiio/pull/1599), and [fixed the API test builds and added macOS emulator testing](https://github.com/analogdevicesinc/libiio/pull/1600).
- **[ANTSDR E200 firmware](https://github.com/MicroPhase/antsdr-fw-patch)** (MicroPhase): the vendor adopted 6 patches into a [dedicated consolidation branch](https://github.com/MicroPhase/antsdr-fw-patch/tree/merge/enrico-prs). They cover build preflight checks, a Kconfig fix, enabling the second CPU core and documented FPGA limitations. I also maintain [antsdr-e200-fw](https://github.com/enricolorenzoni59/antsdr-e200-fw), which migrates the firmware runtime to native libiio 1.0 with ABI validation and Linux CI.
- **[RTL-SDR Blog](https://github.com/rtlsdrblog/rtl-sdr-blog)** (under review): [per-stage gain control for R82xx tuners](https://github.com/rtlsdrblog/rtl-sdr-blog/pull/79), and [ending `rtlsdr_read_async()` cleanly when the device is unplugged](https://github.com/rtlsdrblog/rtl-sdr-blog/pull/83).
- **[Airspy host tools](https://github.com/airspy/airspyone_host/pull/107)** (under review): avoid redundant USB configuration changes during device open.

## Other merged contributions

- **[Tvheadend](https://github.com/tvheadend/tvheadend)**: [fixed a lock leak on a failed UUID assignment](https://github.com/tvheadend/tvheadend/pull/2083) and [handling of relative IPTV key URLs](https://github.com/tvheadend/tvheadend/pull/1748).
- **[MeshCore](https://github.com/meshcore-dev/MeshCore/pull/1871)** (firmware): fixed the `gps sync` reply buffer.
- **[MeshMonitor](https://github.com/Yeraze/meshmonitor/pull/6122)**: stopped a server crash, a regression that lost every room post from serial and TCP radios.
- **[Wavelog](https://github.com/wavelog/wavelog/pull/3990)**: corrected the DXCC award progress calculation, with a container-based reproduction and regression fixtures.
- **[dtv-scan-tables](https://github.com/tvheadend/dtv-scan-tables/pull/173)**: updated the Italian DVB-T frequency tables.
- **[label-maker](https://github.com/burnmark-io/label-maker/pull/1)**: dependency update adding DYMO 11354 support.

## How I work

- **Reproduce first.** A bug report is a sanitizer trace, a failing input or a measurement, not an opinion.
- **Small, reviewable changes.** One concern per PR, with independent commits, so a maintainer can take part of it and drop the rest.
- **Measure what you claim.** For performance, I use instruction counts or controlled benchmarks rather than noisy wall-clock time.
- **Respect the codebase's trade-offs.** When a maintainer prefers a different fix, such as keeping the forwarding path lock-free, I adapt to that design and follow up with data.

## Earlier work

Some earlier contributions were submitted from my previous account, [enrico-samknows](https://github.com/enrico-samknows). One example is a [Boost.JSON AddressSanitizer investigation](https://github.com/boostorg/json/pull/663) into invalid pointer-pair handling during serialization. The PR was closed, but the maintainers investigated further and fixed the issue.

## Technical interests

`C` · `C++` · `Linux` · `Concurrency` · `Sanitizers & fuzzing` · `Performance engineering` · `DSP` · `SDR` · `Embedded Linux` · `Rust` · `Python`

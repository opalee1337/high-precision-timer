# Precision Timer

A lightweight high-precision timer utility for Windows, built on top of `QueryPerformanceCounter` (QPC).
Designed for low-latency timing and more accurate sleep behavior than standard `sleep_for`.

---

## Features

- High-resolution timing (~100ns precision via QPC)
- Calibrated sleep to compensate for OS scheduling overhead
- Hybrid sleep strategy:
  - coarse sleep (`sleep_for`)
  - yield phase (`std::this_thread::yield`)
  - spin-wait using `_mm_pause`
- Cached frequency for minimal overhead
- Simple static API (no instantiation required)

---

## Usage

```cpp
#include "timer.h"

using pane::common::Timer;

int main() {
    Timer::Init(); // optional: pre-calibrate sleep overhead

    double start = Timer::GetTime();

    Timer::PrecisionSleep(10.0); // sleep ~10 ms

    double end = Timer::GetTime();
}

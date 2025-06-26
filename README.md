# Ghidra aarch64 Native Binaries (Development Build)

![Ghidra Version](https://img.shields.io/badge/Ghidra-11.4_DEV-blueviolet)
![Architecture](https://img.shields.io/badge/Architecture-aarch64-informational)
![License](https://img.shields.io/badge/License-Apache_2.0-blue)

This repository provides unofficial, pre-compiled native binaries (including the decompiler) for running the Ghidra Software Reverse Engineering (SRE) suite on `aarch64` (ARM64) Linux systems, such as Chromebooks with ARM processors.

The official Ghidra releases do not always include these binaries for development versions, which prevents the decompiler from working out-of-the-box on this architecture. These files were built from the official source code to solve that problem.

---

> ## ⚠️ Disclaimer
>
> This is an **unofficial community build** and is not affiliated with, or endorsed by, the National Security Agency or the Ghidra project. This build is based on a **development version** of Ghidra and may be less stable than official public releases. Use at your own risk. For maximum security, you should build from source yourself (see instructions below).

---

## Compatibility

These binaries were built for a specific development version of Ghidra and a specific environment. Using them with other versions will likely not work.

| Component           | Version / Details            |
| ------------------- | ---------------------------- |
| **Ghidra Version** | `11.4_DEV`                   |
| **Target Arch** | `aarch64` / `ARM64`          |
| **Build OS** | `Debian 12 (Bookworm)`       |
| **Build JDK** | `OpenJDK 21`                 |

---

## Installation Instructions

To use these binaries, you will need to first build the corresponding `11.4_DEV` version of Ghidra from source, and then overlay these files if your own build fails to produce the native components.

1.  **Build Ghidra:** Follow the official instructions to build the `11.4_DEV` version from the Ghidra source code. The final output of the build process is a `.zip` file (e.g., `ghidra_11.4_DEV_....zip`).

2.  **Download Native Binaries:** Go to this repository's **[Releases Page](https://github.com/bolo73/ghidra-aarch64-natives/releases)** and download the `ghidra_11.4_DEV_aarch64_natives.tar.gz` asset.

3.  **Unzip Your Ghidra Build:** In your terminal, unzip your build package. This will create a directory like `ghidra_11.4_DEV`.
    ```bash
    unzip ghidra_11.4_DEV_*.zip
    ```

4.  **Extract Native Binaries:** Extract the `aarch64` binaries you downloaded from this repository directly into the Ghidra directory you just unzipped. The `-C` flag in the command is important as it tells `tar` where to place the files.
    ```bash
    tar -xzf ghidra_11.4_DEV_aarch64_natives.tar.gz -C ghidra_11.4_DEV/
    ```
    This command will correctly place the `decompile` executable and other native libraries into their required subdirectories (e.g., `Ghidra/Features/Decompiler/os/linux_aarch64/`).

5.  **Launch Ghidra:** Run Ghidra as you normally would. The decompiler should now be fully functional!
    ```bash
    cd ghidra_11.4_DEV/
    ./ghidraRun
    ```

<br/>

<details>
<summary>💻 **How These Binaries Were Built**</summary>

For transparency, these binaries were created on a Debian 12 system by following these key steps after many rounds of troubleshooting:

1.  Installed necessary build tools (`build-essential`, `make`, etc.).
2.  Manually installed `OpenJDK 21` and configured it to be the system default.
3.  Cloned the Ghidra `master` branch and ran the build.
4.  Ran the bootstrap script to fetch all third-party dependencies: `./gradlew -I gradle/support/fetchDependencies.gradle`
5.  Ran the main build command: `./gradlew buildGhidra`

</details>

---

## License

The Ghidra SRE suite is licensed under the Apache License, Version 2.0. A copy of the license from the official Ghidra repository is included in this project. All acknowledgements and credits go to the developers and contributors of the Ghidra project.

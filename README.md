# IE-Engine-Bridge 

IE-Engine-Bridge is a lightweight Windows utility written in C that restores access to the Internet Explorer (Trident) rendering engine. In modern Windows (10/11), while the `iexplore.exe` entry point is disabled or redirected to Microsoft Edge, the underlying engine remains available via HTML Applications (HTA). 

This tool automates the process of creating a temporary HTA environment to browse legacy websites that require IE compatibility.

## Features
- Bypass Redirection: Directly invokes the Trident engine without triggering Microsoft Edge.
- Portable: Single executable with no installation required.
- Stealthy: Automatically cleans up or overwrites its footprint in the system `%TEMP%` folder.
- Custom UI: Features a minimalist navigation bar built with HTML/CSS.

## How it Works
1. The C program retrieves the system's temporary directory path.
2. It dynamically generates a `.hta` file containing a custom-designed browser shell.
3. It executes the HTA using the system's built-in `mshta.exe`.
4. The HTA runs as a standalone window, providing an isolated IE-engine environment.

## Installation & Building

### Prerequisites
- A C compiler (e.g., GCC/MinGW, MSVC, or Clang)
- Windows OS (10 or 11 recommended)

### Compiling with GCC (MinGW)
```bash
gcc -o IE-Engine-Bridge.exe main.c -mwindows
```

### Compiling with Visual Studio (cl.exe)
```cmd
cl main.c /link shell32.lib user32.lib /subsystem:windows
```

## GitHub Actions 自动编译与发布

仓库包含 `/.github/workflows/build-release.yml` 工作流：

- 推送 `v*` 标签时会自动在 `windows-latest` 上编译 `IE-Engine-Bridge.exe`。
- 编译产物会作为 Actions Artifact 保存。
- 同时会自动创建/更新同名 GitHub Release，并上传 `IE-Engine-Bridge.exe` 到该 Release。

你也可以在 Actions 页使用 **Run workflow** 手动触发，并填写要发布的标签（例如 `v1.0.0`）。

## Usage
1. Run `IE-Engine-Bridge.exe`.
2. A window will appear using the legacy Internet Explorer engine.
3. Enter the URL in the address bar (including `http://` or `https://`) and click GO.

## Preview
The interface includes:
- A navigation bar with URL input.
- A "Go" button for navigation.
- A full-screen iframe powered by the Trident engine.

## Security Warning
Internet Explorer and the Trident engine are deprecated. 
- Do not use this tool for daily browsing or entering sensitive credentials on the public web.
- Only use this for accessing trusted legacy internal systems or specialized hardware interfaces that strictly require IE.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---
*Disclaimer: This project is intended for legacy compatibility and educational purposes only. Microsoft, Internet Explorer, and Windows are trademarks of Microsoft Corporation.*

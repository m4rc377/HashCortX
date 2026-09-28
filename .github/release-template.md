**HashCortx is a desktop AI workspace that runs on your own machine.** Chat with eleven providers or your own local models, run an autonomous coding agent, read your own documents, analyse financial statements, design 3D parts, and put a team of agents on one brief. No backend, no account, no telemetry. Free and MIT-licensed.

**This release runs on Linux, Windows, and macOS.** Until now the prebuilt downloads only targeted Apple Silicon macOS and Windows x64. This release carries prebuilt packages for Debian/Ubuntu, universal Linux (AppImage), Windows (both portable and installer), and macOS (both Apple Silicon and Intel).

---

## What else is in 2.6.0

112 commits since v2.5.0. The largest part of it is **3D Forge**, which went from a demo to something that produces a file a printer or a CAD program will accept:

- **Models have a real size, in millimetres**, written into every file they export.
- **Solid geometry.** Parts are fused into one solid, a design can cut a hole through it, and a model can be hollowed to a real wall thickness.
- **Our own STL, OBJ, 3MF and STEP writers**, rather than relying on a library to describe what the numbers mean. Writing them ourselves uncovered that every mirrored part had been exported inside out.
- **A printability report**, in millimetres, saying whether the thing could actually be made.
- **A build order you can rearrange**, part dimensions you can type, and holes you can cut by hand.
- **A design can do arithmetic**, so a part that repeats is written once instead of twenty-four times.

Elsewhere:

- **A model that fails no longer falls back to a worse one than it should.** Candidates were ranked by family name before variant, so a failover reached for the small cheap model ahead of a genuinely large one.
- **Money is read correctly.** A bracketed debit was being counted as money coming in.
- **Generated dates were a day early** everywhere east of Greenwich.
- **Every export writes a file.** Seventeen save buttons and the Python sandbox's own output wrote nothing at all, silently.

The full list, including what is still open, is in the [changelog](https://github.com/REPO_PLACEHOLDER/blob/main/CHANGELOG.md).

---

## Linux

Download the package matching your distribution below:

- **Debian, Ubuntu, Linux Mint, Pop!_OS:** Download the `.deb` package and install it:
  ```bash
  sudo apt install ./hashcortx_VERSION_PLACEHOLDER_amd64.deb
  ```
- **Universal Linux (Arch, Fedora, openSUSE, etc.):** Download the `.AppImage`, make it executable, and run it directly:
  ```bash
  chmod +x hashcortx_VERSION_PLACEHOLDER_amd64.AppImage
  ./hashcortx_VERSION_PLACEHOLDER_amd64.AppImage
  ```

---

## Windows

Choose between the standalone portable program or the full setup installer:

- **Portable (No install needed, starts on any 64-bit PC):**  
  Download **HashCortx_VERSION_PLACEHOLDER_x64_no-embeddings.exe** below and run it. There is nothing to install — it is the program itself, not an installer.  
  
  This is the build made without local embeddings, and that is deliberate. The standard build links a prebuilt ONNX Runtime compiled for processors with AVX2 — Intel from 2013, AMD from 2015 — and it is linked in such a way that its start-up code runs before the app's own. On an older processor the app cannot start at all: no window, no error, nothing on screen. The build published here has none of that code in it and starts on any 64-bit PC.

  What you give up is search by meaning: the knowledge base matches on keywords instead, and the app reports that it is doing so rather than quietly returning weaker results. Everything else — the chat, the coding agent, the swarm, the file work, 3D Forge — is the same app.

- **Installer (Standard setup with Start Menu integration):**  
  Download **HashCortx_VERSION_PLACEHOLDER_x64-setup.exe** (or `.msi`) below and run the installation wizard.

**Windows will show a blue "Windows protected your PC" box.** That happens for any program without a paid signing certificate. Click **More info**, then **Run anyway**. If the window opens white and empty, install the [WebView2 runtime](https://developer.microsoft.com/microsoft-edge/webview2/).

---

## macOS

Download the image matching your Mac processor, open it, and drag HashCortx to Applications:

- **Apple Silicon (M1/M2/M3/M4):** Download `HashCortx_VERSION_PLACEHOLDER_aarch64.dmg`
- **Intel Mac:** Download `HashCortx_VERSION_PLACEHOLDER_x64.dmg`

macOS will refuse it the first time. The app is not signed by Apple and not notarised, because that needs a paid developer account, and macOS treats everything unsigned the same way. It is not damaged. Open Terminal and run this once:

```bash
xattr -cr /Applications/HashCortx.app
```

Then open it normally. You never have to do this again.

---

## Check the download is the one that was published

Optional, and worth doing if you care where your software came from. Run this in the folder you downloaded to; if it matches, your copy is byte-for-byte the file uploaded here.

Linux:

```bash
sha256sum hashcortx_VERSION_PLACEHOLDER_amd64.deb
```

```text
__DEB_HASH__
```

```bash
sha256sum hashcortx_VERSION_PLACEHOLDER_amd64.AppImage
```

```text
__APPIMAGE_HASH__
```

Windows (PowerShell):

```powershell
Get-FileHash HashCortx_VERSION_PLACEHOLDER_x64_no-embeddings.exe -Algorithm SHA256
```

```text
__WIN_PORTABLE_HASH__
```

```powershell
Get-FileHash HashCortx_VERSION_PLACEHOLDER_x64-setup.exe -Algorithm SHA256
```

```text
__WIN_SETUP_HASH__
```

macOS:

```bash
shasum -a 256 HashCortx_VERSION_PLACEHOLDER_aarch64.dmg
```

```text
__MAC_ARM_HASH__
```

```bash
shasum -a 256 HashCortx_VERSION_PLACEHOLDER_x64.dmg
```

```text
__MAC_INTEL_HASH__
```

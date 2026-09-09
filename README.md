# EurKEY 1.3r with Slovak `ĺ`

This fork makes one small change to [rpnfan's modern EurKEY 1.3r Windows rebuild](https://github.com/rpnfan/EurKey-fork-for-Windows):

- acute + `l` produces Slovak `ĺ` (`U+013A`) instead of Polish `ł` (`U+0142`)
- acute + `L` produces Slovak `Ĺ` (`U+0139`) instead of Polish `Ł` (`U+0141`)

The existing caron combinations are unchanged, so caron + `l`/`L` still produces `ľ`/`Ľ`.

The project has a unique name and ID so it can coexist with stock EurKEY and
older custom builds. The MSKLC package supports x86 and x64 Windows, not ARM64.

## installing

1. Download the latest installer archive from this fork's [Releases](../../releases).
2. Extract it.
3. Run `setup.exe`.
4. Sign out and back in, or restart Windows.
5. Select **EurKEY 1.3r - Slovak l-acute** using `Win+Space`.

Test both sequences:

- `AltGr + '`, then `l` should type `ĺ`
- `Shift + AltGr + 6`, then `l` should type `ľ`

Run `setup.exe` again and choose the removal option to uninstall it.

## modifying and building the layout

- x64 Windows 11
- [.NET Framework 3.5](https://learn.microsoft.com/en-us/dotnet/framework/install/dotnet-35-windows), enabled through **Turn Windows features on or off**
- [Microsoft Keyboard Layout Creator 1.4](https://www.microsoft.com/en-us/download/details.aspx?id=102134)

`eursk13.klc` is based on the source shipped in upstream's EurKEY 1.3r release.
Its only keymap change is in the acute-accent dead-key table:

```text
006c    013a    // l -> ĺ
004c    0139    // L -> Ĺ
```

Leave the caron table unchanged; it already contains `ľ` and `Ľ`.

1. Start **Microsoft Keyboard Layout Creator 1.4** and load `eursk13.klc`.
2. Select **Project > Build DLL and Setup Package**.
3. Accept the inherited `ß`/`ẞ` casing warning; there should be no errors.
4. Choose an output directory outside the repository, such as `Documents\eursk13`.

The output contains `setup.exe`, architecture-specific MSI packages and DLL directories. These are generated release artifacts: keep them out of Git and attach a ZIP containing the complete output directory to a GitHub release instead.

Keep generated DLLs, MSIs and `setup.exe` out of Git. Zip the complete build
directory and attach it to a GitHub release.

---

## Original README

<img width="1448" height="518" alt="image" src="https://github.com/user-attachments/assets/202d748e-9d21-4202-8143-b22be31783b0" />

# EurKey (Windows Installer Rebuild)

**Unofficial rebuild of [EurKEY v1.3](https://eurkey.steffen.bruentjen.eu/)
by Steffen Brüntjen: same layout, fixed Windows installer.**

This is **not** a modified layout. The keymap is identical to the
official EurKEY v1.3. The only difference is the build pipeline used
to create the Windows installer.

## Why this exists

The official Windows installer had several issues reported:

- Problems with keyboard shortcuts not working
- May not register correctly in the Windows language bar
- Math symbols from beta 1.3 not working
- Fails to install on ARM64 Windows
- Keymaps could not be loaded directly into [KbdEdit](http://kbdedit.com/)

## What I did

1. Exported the layout to an MSKLC source file
2. Imported this into KbdEdit
3. Added the math symbols. These were missing from the MSKLC import.
4. Added a handful of extra math symbols such as: ⋙ ⋘ ≟ ⊾ ≉  and a real minus character. See the PDF for the shortcuts.
5. Built a new installer package from KbdEdit directly

This installer works correctly on the systems I tested, including ARM64.

## Installation/Uninstall

 1. Download the installer from [Releases](../../releases)
 2. Run the installer
 3. Reboot or log out and log in again to Windows.

 4. Uninstall: Run the installer again and choose the uninstall option.

## Security / Virus Check

This repository provides a compiled Windows installer (`.exe`). If you want to verify it before running it, upload it to **[VirusTotal.com](https://www.virustotal.com/)** — it will be scanned by about 60+ antivirus engines simultaneously.

When I last checked, 68 of 69 engines reported the file as clean. The single flag came from Trapmine, which uses machine-learning heuristics and is [well known for false positives on legitimate installers](https://www.google.com/search?q=Trapmine+Malicious.moderate.ml.score+false+positive). No major antivirus vendor flagged it.

If you are not comfortable running the installer regardless, the KbdEdit source `.kbe` is also in this repo which you can use and build the installer with kbdedit yourself.

## Credit & License

The EurKEY layout is © Steffen Brüntjen, licensed under
[GPLv3](LICENSE). This repository redistributes it unmodified under the
same license, with a different installer build. All credit for the
layout design goes to the original author. Please check out the
[official site](https://eurkey.steffen.bruentjen.eu/) and consider
supporting it there.

This is an independent, unofficial project, not affiliated with or
endorsed by the original author.

## Future plans

I'm also working on a separate, modified layout inspired by EurKEY's
AltGr/diacritic approach which will live in its own repo under a
different name once it is ready.

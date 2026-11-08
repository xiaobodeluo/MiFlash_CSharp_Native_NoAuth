# No-admin MiFlash patch for Xiaomi 9 SE (`grus`)

This fork carries a minimal portability patch for the native C# NoAuth MiFlash
client. It was validated against a Qualcomm SDM710 device in 9008 mode.

## Changes

1. `src/app.manifest`
   - Requested execution level changed from `requireAdministrator` to
     `asInvoker`.
2. `src/XiaoMiFlash.code.Utility/IniFile.cs`
   - `MiFlashvcom.ini` now lives beside `MiFlash.exe`.
   - The upstream code attempted to create `C:\MiFlashvcom.ini`, which fails
     for a non-elevated process on a normal Windows installation.

No changes were made to the EDL/Firehose command sequence.

## Verified device and firmware

- Device: Xiaomi 9 SE (`grus`), SDM710, bootloader locked
- EDL transport: `Qualcomm HS-USB QDLoader 9008 (COM5)`
- Firmware:
  `grus_images_9.4.18_20190418.0000.00_9.0_cn_22e903424a.tgz`
- Firmware SHA-256:
  `9C90BC3BDFB90C8D2C211018B551131A62BB740B8FC03A9E496CF835CE0781F4`
- Firehose:
  `prog_ufs_firehose_sdm710_ddr.elf`
- Flash mode: clean all / all delete

## Verification result

- GUI result: `100% / flash done / success`
- Elapsed time: 164 seconds
- `rawprogram0.xml` through `rawprogram5.xml`: completed
- GPT images and `patch0.xml` through `patch5.xml`: completed with ACK
- Final command: `power reset`
- Log scan: zero matches for `ERROR`, `failed`, `exception`, and
  `authentication failed`
- After reset, 9008 disappeared and the device booted after a manual power-on.

## How to use the release bundle

1. Extract `MiFlash_NoAuth_grus.zip`.
2. Start `MiFlash.exe`.
3. Select the firmware root containing `images` and `rawprogram0.xml` through
   `rawprogram5.xml`.
4. Select the 9008 COM port and click `start flash`.
5. The first configure request enters the delayed auth-bypass path. The tool
   sends the fallback `sig` request after roughly 20 seconds and continues when
   the target returns `Authenticated==, TRUE`.

The release bundle is intended to make this exact tested build reproducible.
Build from source when integrating the patch elsewhere.

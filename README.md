# MiFlash CSharp Native NoAuth
For educational purposes. Learn how Xiaomi Flash work on Qualcomm EDL Protocol with C# code...

[![Preview](https://i.ibb.co/XZCyLFx4/image.png)](https://ibb.co/VWqH9MYN)

## No-admin patch

This fork includes a small portability patch for running MiFlash from a regular
user account:

- `app.manifest` uses `asInvoker` instead of `requireAdministrator`.
- `MiFlashvcom.ini` is created beside the application instead of in `C:\`.

The patched build was tested on a Xiaomi 9 SE (`grus`, SDM710) with the complete
MIUI 9.4.18 UFS package. The full flash completed in 164 seconds with zero
`ERROR`, `failed`, `exception`, or authentication failures in the EDL log.

See [docs/NOADMIN-GRUS.md](docs/NOADMIN-GRUS.md) for the exact test result,
hashes, and usage notes. Download the tested runnable bundle from the
[latest release](../../releases/latest).

## Supported devices (upstream list)

Auth Bypass work on Xiaomi 
- SD 636
- SD 680
- SD 845
- SD 855
- SD 860
- SD 870

Depend on supported firehose file loader or eng firehose loader.

Video test on Redmi 7
https://youtu.be/r4RJSzSzOg0

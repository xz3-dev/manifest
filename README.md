# manifest

Local manifest for a LineageOS 22.2 build for the Sony Xperia XZ3 **801SO**
(`akatsuki`).

```sh
repo init -u https://github.com/LineageOS/android.git -b lineage-22.2 --git-lfs
git clone -b lineage-22.2 https://github.com/xz3-dev/manifest .repo/local_manifests
repo sync -c --no-tags
export GH_TOKEN=...                     # read access to xz3-dev/xz3-gcam
vendor/sony/xz3/scripts/fetch-prebuilts.sh
source build/envsetup.sh
breakfast akatsuki
m target-files-package otatools-package
```

## Projects

| Path | Repository | Revision |
|---|---|---|
| `device/sony/akatsuki` | xz3-dev/android_device_sony_akatsuki | `lineage-22.2-xz3` |
| `device/sony/tama-common` | xz3-dev/android_device_sony_tama-common | `lineage-22.2-xz3` |
| `kernel/sony/sdm845` | xz3-dev/android_kernel_sony_sdm845 | `lineage-22.2-xz3` |
| `hardware/sony/SonyOpenTelephony` | LineageOS/android_hardware_sony_SonyOpenTelephony | `lineage-22.2` |
| `vendor/sony/akatsuki` | TheMuppets/proprietary_vendor_sony_akatsuki | `lineage-22.2` |
| `vendor/sony/tama-common` | TheMuppets/proprietary_vendor_sony_tama-common | `lineage-22.2` |
| `vendor/sony/xz3` | xz3-dev/proprietary_vendor_sony_xz3 (private) | `lineage-22.2` |

Removed: `packages/apps/Aperture` (GCam is the camera app).

KernelSU-Next is vendored in the kernel (`drivers/kernelsu`) and needs no
project. The camera bridge library and the patched camera provider are
committed to `vendor/sony/xz3`; GCam is downloaded from the xz3-gcam CI by
`vendor/sony/xz3/scripts/fetch-prebuilts.sh`, so neither xz3-camera-bridge nor
xz3-gcam is synced.

Tested revisions of TheMuppets: akatsuki `d1dafaa568a2`, tama-common
`e4046a9cc96b`.

## Private repositories

`vendor/sony/xz3` and the GCam download need a GitHub token with read access.
For `repo sync` over HTTPS, for example:

```sh
git config --global url."https://x-access-token:${GH_TOKEN}@github.com/xz3-dev/".insteadOf \
    "https://github.com/xz3-dev/"
```

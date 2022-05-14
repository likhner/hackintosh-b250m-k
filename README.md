# Hackintosh B250M-K

## Hardware

| Type         | Model                                                                                                                                                 |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| Motherboard  | [ASUS PRIME B250M-K](https://www.asus.com/Motherboards-Components/Motherboards/PRIME/PRIME-B250M-K/techspec/)                                         |
| CPU          | [Intel Core i5-7400](https://ark.intel.com/content/www/us/en/ark/products/97147/intel-core-i57400-processor-6m-cache-up-to-3-50-ghz.html) (Kaby Lake) |
| Video card   | NVIDIA GeForce GTX 1050                                                                                                                               |
| iGPU*        | Intel HD Graphics 630                                                                                                                                 |
| Network card | Realtek RTL8111H                                                                                                                                      |
| Sound card   | Realtek ALC887                                                                                                                                        |

*iGPU is used for IQSV

## Issues

| Issue                                             | Fixable? | Reason                                                 | Fix |
|---------------------------------------------------|----------|--------------------------------------------------------|-----|
| No sound adjustment of the video card             | ❌        | Not supported by macOS                                 | ❌   |
| Unable to assign all USB ports to the map         | ❌        | The macOS limit of 15 USB ports                        | ❌   |
| The latest supported version is macOS High Sierra | ❌        | NVIDIA graphics cards are no longer supported by macOS | ❌   |
| HDMI audio does not work when using AppleALC      | ❌        | 🤷‍♂️                                                     | ❌   |

## OpenCore

### Drivers

| Name                                                                                   | Description                     |
|----------------------------------------------------------------------------------------|---------------------------------|
| [HfsPlus](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi) | Required to display HFS volumes |
| [OpenRuntime](https://github.com/acidanthera/OpenCorePkg/releases/latest)              | Required for NVRAM support      |

### SSDTs

| Name                                      | Description                                                 |
|-------------------------------------------|-------------------------------------------------------------|
| [SSDT-EC-USBX](SSDT/SSDT-EC-USBX.dsl)     | Fixes both the embedded controller and the USB power supply |
| [SSDT-PLUG](SSDT/SSDT-PLUG.dsl)           | Fixes CPU power management                                  |
| [SSDT-SBUS-MCHC](SSDT/SSDT-SBUS-MCHC.dsl) | Fixes SMBus support                                         |

### Kexts

| Name                                                                                                                  | Description             |
|-----------------------------------------------------------------------------------------------------------------------|-------------------------|
| [Lilu](https://github.com/acidanthera/Lilu/releases)                                                                  | Universal patcher       |
| [RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X/releases/download/v2.2.2/RealtekRTL8111-V2.2.2.zip) | Kext for network card   |
| [USBMap](EFI/OC/Kexts/)                                                                                               | USB port map            |
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases/latest) (_SMCProcessor, SMCSuperIO_)                  | Apple SMC Emulator      |
| [VoodooHDA](https://sourceforge.net/projects/voodoohda/files/latest/download)                                         | Kext for sound card     |
| [WhateverGreen](https://github.com/acidanthera/whatevergreen/releases/latest)                                         | Video card patcher      |
| [NVIDIA Web](https://gfe.nvidia.com/mac-update)                                                                       | Kext for the video card |
| [NVIDIA CUDA](https://www.nvidia.com/en-us/drivers/cuda/mac-driver-archive/)                                          | Kext for CUDA           |

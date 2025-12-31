# RadioMaster MT12 Build Workflow

This GitHub Actions workflow automatically builds the latest Multiprotocol firmware for the RadioMaster MT12 transmitter.

## How It Works

The workflow is triggered on every push to the `master` branch that modifies:
- The workflow file itself (`.github/workflows/build-mt12.yml`)
- Build scripts (`buildroot/bin/**`)
- Multiprotocol firmware source code (`Multiprotocol/**`)

## What Gets Built

The workflow builds the STM32F103 128KB 4-in-1 firmware variants suitable for the RadioMaster MT12:
- Serial mode builds with different channel orders (AETR, TAER, RETA)
- Air mode, Surface mode, and EU/LBT variants
- PPM mode builds with different channel orders

All built firmware files are uploaded as GitHub Actions artifacts and retained for 90 days.

## Manual Trigger

You can also manually trigger the build from the GitHub Actions tab:
1. Go to the "Actions" tab in your repository
2. Click on "Build RadioMaster MT12 Firmware" workflow
3. Click "Run workflow" button
4. Select the branch and click "Run workflow"

## Downloading Built Firmware

After a successful build:
1. Go to the Actions tab
2. Click on the completed workflow run
3. Scroll down to the "Artifacts" section
4. Download the `radiomaster-mt12-firmware` artifact
5. Extract the ZIP file to access the firmware binaries

## Firmware Files

The firmware binaries will be named like:
- `mm-stm-serial-aetr-air-v{VERSION}.bin` - Serial mode, AETR channel order, Air
- `mm-stm-serial-taer-air-v{VERSION}.bin` - Serial mode, TAER channel order, Air
- `mm-stm-serial-reta-air-v{VERSION}.bin` - Serial mode, RETA channel order, Air
- Similar variants for surface (`sfc`) and EU/LBT (`lbt`) modes
- `mm-stm-ppm-{order}-v{VERSION}.bin` - PPM mode variants

Choose the appropriate firmware based on:
- Your preferred channel order (AETR is standard for FlySky/DEVO, TAER for JR/Spektrum)
- Your region (Air for US/Asia, LBT for EU)
- Your use case (Air for aircraft/drones, Surface for cars/boats)

## Technical Details

- **Board:** STM32F103CB (128KB flash)
- **Module Type:** 4-in-1 (supports A7105, CYRF6936, CC2500, NRF24L01)
- **Build System:** Arduino CLI 0.32.2
- **Core:** multi4in1:STM32F1

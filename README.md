# ti-cc-tool
Docker image for [JelmerT/cc2538-bsl](https://github.com/JelmerT/cc2538-bsl)

* This project allows to flash a TI SoC with a single line of code.
* Firmware files are supported as URL or local file, in native (bin/hex) and zipped format.

## Usage
### Docker
#### Example: download firmware and flash to SONOFF Dongle Plus
```sh
$ docker run --rm --device /dev/ttyUSB0:/dev/ttyUSB0 -e FIRMWARE_URL=https://github.com/Koenkk/Z-Stack-firmware/raw/master/coordinator/Z-Stack_3.x.0/bin/CC1352P2_CC2652P_launchpad_coordinator_20211217.zip ckware/ti-cc-tool -ewv -p /dev/ttyUSB0 --bootloader-sonoff-usb
```

#### Example: flash local firmware file to SONOFF Dongle Plus
* This example expects the file `CC1352P2_CC2652P_launchpad_coordinator_20211217.zip` in the local directory
* ```sh
  $ docker run --rm --device /dev/ttyUSB0:/dev/ttyUSB0 -e FIRMWARE_FILE=CC1352P2_CC2652P_launchpad_coordinator_20211217.zip ckware/ti-cc-tool -ewv -p /dev/ttyUSB0 --bootloader-sonoff-usb
  ```

### docker-compose
1. Create a `docker-compose.yml` for your environment
1. Run `docker-compose run --rm ckware/ti-cc-tool`

#### Example: download firmware and flash to SONOFF Dongle Plus
```yaml
---
services:
  ti-cc-tool:
    image: "ckware/ti-cc-tool"
    environment:
      FIRMWARE_URL: "https://github.com/Koenkk/Z-Stack-firmware/raw/master/coordinator/Z-Stack_3.x.0/bin/CC1352P2_CC2652P_launchpad_coordinator_20211217.zip"
    devices:
      "/dev/ttyUSB0:/dev/ttyUSB0"
    command: [ "-ewv", "-p", "/dev/ttyUSB0", "--bootloader-sonoff-usb" ]
```

#### Example: flash local firmware file to SONOFF Dongle Plus
```yaml
---
services:
  ti-cc-tool:
    image: "ckware/ti-cc-tool"
    devices:
      "/dev/ttyUSB0:/dev/ttyUSB0"
    environment:
      FIRMWARE_FILE: "/firmware.zip"
    volumes:
      - "./CC1352P2_CC2652P_launchpad_coordinator_20211217.zip:/firmware.zip"
    command: [ "-ewv", "-p", "/dev/ttyUSB0", "--bootloader-sonoff-usb" ]

```

## Requirements
### Software
* Required: Docker
* Optional: Docker Compose

The Docker Compose [documentation](https://docs.docker.com/compose/install/)
contains a comprehensive guide explaining several install options. On recent debian-based systems, Docker Compose may be installed by calling
  ```sh
  $ sudo apt install docker-compose
  ```

## References
* This project is an integration of
  * [JelmerT/cc2538-bsl](https://github.com/JelmerT/cc2538-bsl)
  * [Docker](https://www.docker.com)

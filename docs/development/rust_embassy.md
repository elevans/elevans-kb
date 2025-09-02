# Embassy

## Setup `probe-rs`

Embassay uses `probe-rs` to write and debug embedded devices. Follow the steps
below to create your own debugging probe for an RP2040 (needs one RP2040 as the
probe).

1. Selected an RP2040 device as your debugging probe.
2. Download the latest release of the `debugprobe` from the
   [official repository](https://github.com/raspberrypi/debugprobe/releases/tag/debugprobe-v2.2.3).
3. Put your RP2040 device into BOOTSEL mode and copy the .`uf2` debug file onto
   the mounted volume.   

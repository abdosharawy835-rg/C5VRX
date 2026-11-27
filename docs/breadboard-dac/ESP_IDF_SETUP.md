# Development environment — upstream C5VRX

The current upstream README specifies **ESP-IDF 6.0.2** for the verified PHY
filter/DC-correction path. Other ESP-IDF versions may build with those features
disabled and a warning; use 6.0.2 for a faithful baseline.

## Recommended environment

- OS: Ubuntu 22.04/24.04 (native or VM)
- Git
- ESP-IDF v6.0.2 and its ESP32-C5 toolchain
- USB-C data cable
- Python environment managed by ESP-IDF

## Setup outline (Ubuntu)

```bash
sudo apt update
sudo apt install -y git wget flex bison gperf python3 python3-venv \
  cmake ninja-build ccache libffi-dev libssl-dev dfu-util \
  libusb-1.0-0

mkdir -p ~/esp
cd ~/esp
git clone -b v6.0.2 --recursive https://github.com/espressif/esp-idf.git
cd esp-idf
./install.sh esp32c5
. ./export.sh
```

Open a new terminal for future sessions and source the environment:

```bash
. "$HOME/esp/esp-idf/export.sh"
idf.py --version
```

## Get the C5VRX source

```bash
cd ~/esp
git clone --recursive https://github.com/Twotoz/C5VRX.git
cd C5VRX
```

If already cloned:

```bash
cd ~/esp/C5VRX
git pull --ff-only
git submodule update --init --recursive
```

## Build

```bash
. "$HOME/esp/esp-idf/export.sh"
idf.py set-target esp32c5
idf.py build
```

The upstream README warns that `idf.py flash` can trigger a USB line-reset
problem on a running receiver. Follow the current upstream flashing procedure
and use its `tools/flash.py` helper as documented there, rather than assuming
a generic flash command is safe.

Example (replace `COM6` with the actual port):

```bash
python tools/flash.py COM6
```

## GitHub workflow for this supplementary package

Keep this package in a separate repository or add its `hardware/` and
`environment/` directories to your own fork as documentation. Do not overwrite
upstream firmware files just to add the breadboard notes.

```bash
git init
git add README.md hardware/ environment/
git commit -m "Add C5VRX breadboard DAC build documentation"
git branch -M main
git remote add origin https://github.com/USERNAME/REPOSITORY.git
git push -u origin main
```

Replace `USERNAME/REPOSITORY` with your own GitHub repository URL.

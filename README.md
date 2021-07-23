# Bypass utility
Small utility to disable bootrom protection (SLA and DA).

## Usage:
```
python main.py [-h] [-c CONFIG] [-t] [-w WATCHDOG] [-u UART] [-v VAR_1] [-a PAYLOAD_ADDRESS] [-p PAYLOAD] [-s SERIAL_PORT] [-f] [-n] [-m CRASH_METHOD]

optional arguments:
  -h, --help              show this help message and exit
  -c CONFIG, --config CONFIG
                          Device configuration file (default is default_config.json5)
  -t, --test              Test mode: tests whether the exploit will or will not work.
  -w WATCHDOG, --watchdog WATCHDOG
                          Watchdog address(in hex)
  -u UART, --uart UART    UART base address(in hex)
  -v VAR_1, --var_1 VAR_1
                          var_1 value(in hex)
  -a PAYLOAD_ADDRESS, --payload_address PAYLOAD_ADDRESS
                          payload_address value(in hex)
  -p PAYLOAD, --payload PAYLOAD
                          Payload to use
  -s SERIAL_PORT, --serial_port SERIAL_PORT
                          Connect to existing serial port
  -f, --force             Force exploit on insecure device
  -n, --no_handshake      Skip handshake
  -m CRASH_METHOD, --crash_method CRASH_METHOD
                          Method to use for crashing preloader (0, 1, 2)
```

## Installation
Note: I don't plan on widely supporting Windows-specific instructions. Using powershell the same commands with basic syntax changes like / to \ should work just fine. Feel free to make a pull request that details it further.

Grab the repository:
```
git clone https://github.com/haise0/bypass_utility
```

The script's default path variables have been changed for the configuration file and payloads folder, so it now works as soon as you have the exploits collection cloned under the main directory. Clone the repository under the mtk_bypass folder:
```
cd bypass_utility
git clone https://github.com/MTK-bypass/exploits_collection 
```

If you've already done the setup steps, you're good to go and can run the python script.

If you haven't, move on to the following steps to finish the steps for setting up depending, on your operating system.

## Setup on Windows
Skip steps 1-5 are only required for first usage.

1. Install [python](https://www.python.org/downloads) and make sure to select "Add Python X.X to PATH."
2. Install [libusb-win32](https://sourceforge.net/projects/libusb-win32/files/libusb-win32-releases/1.2.6.0/libusb-win32-devel-filter-1.2.6.0.exe/download)
3. Launch the filter wizard and click next to install a device driver filter.
4. Connect powered off phone with volume+ button, you should see new serial device in the list. Select and install its filter. On LGE devices, at least the Stylo 6, it will only show for about one second before disappearing again, so you will have to be relatively fast.
5. Install python dependencies:
```
sudo pip install -r requirements.txt
```
6. After that, without disconnecting phone, run SP Flash Tool


## Usage on Linux
Steps 1-2 are only required for first usage.
To use this you need [FireISO](https://github.com/amonet-kamakiri/fireiso/releases) or [this patch](https://github.com/amonet-kamakiri/kamakiri/blob/master/kernel.patch) for your kernel

Prebuilt kernels for various distros are available [here](https://github.com/amonet-kamakiri/prebuilt-kernels). You can install your corresponding kernels directly via `sudo apt install ./<file>` or `dpkg -i <file>` and then `sudo update-grub` to add them to your boot entries (assuming you use grub). Booting with the Kamakiri kernel will be under advanced options by default. Install the headers first, and then the image, and then libc.

1. Install python (version 3. Double check with `python --version`. If it comes up as version 2.x, on most debian-based systems and some others you can install `python-is-python3` or simply use `python3` to execute it. You should also ensure that pip is version 3 as well, with `pip --version`.)
```
sudo apt install python python3-pip python-is-python3
```
3. Install python dependencies:
```
sudo pip install -r requirements.txt
```
3. Run this command as root or with sudo, and connect your powered off phone with volume+ button:
```
./main.py
```
4. After that, without disconnecting phone, run SP Flash Tool in UART Connection mode

## Credits
- [@chaosmaster](https://github.com/chaosmaster)
- [@xyzz](https://github.com/xyzz)
- [@mtkbypass](https://github.com/MTK-bypass/)

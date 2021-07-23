# Bypass utility
Small utility to disable bootrom protection(sla and daa)

## Payloads from the Original Branch:
https://github.com/MTK-bypass/exploits_collection

## Usage on Windows
Skip steps 1-5 after first usage

1. Install [python](https://www.python.org/downloads) and make sure to select "Add Python X.X to PATH."
2. Install [libusb-win32](https://sourceforge.net/projects/libusb-win32/files/libusb-win32-releases/1.2.6.0/libusb-win32-devel-filter-1.2.6.0.exe/download)
3. Launch filter wizard, click next
4. Connect powered off phone with volume+ button, you should see new serial device in the list. Select and install its filter. On LGE devices, at least the Stylo 6, it will only show for about one second before disappearing again, so you will have to be relatively fast.
6. Install python dependencies:
```
sudo pip install -r requirements.txt
```
6. Run this command and connect your powered off phone with volume+ button, you should get "Protection disabled" at the end
```
python main.py
```
7. After that, without disconnecting phone, run SP Flash Tool


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

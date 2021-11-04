``` bash
sudo-apt-get install qemu-system
```

## Requires
- Qemu Kernel
- VM Image Here:
	- [Prebuilt](https://blahcat.github.io/2017/25/qemu-images-to-play-with/)
	- [Raspberyy PI](http://downloads.raspberrypi.org/raspbian/images/rapbian-2017=04-10/)

## Qemu-System (Manual)
### ARM
```bash
qemu-system-arm -kernel <KERNEL> -cpu <CPU> -m <RAM-MB> -M versatilepb -serial stdio -append "root=/dev/sda2 roofstype=ext4 rw" -hda <IMAGE0> -hdb <IMAGE1> -nic user,hostfwd=tcp::5022-:22 -no-reboot
```

## Assigning Ports
``` bash
sudo apt-get install uml-utilities net-tools
sudo tunctl -t tap0 -u <UID>
sudo ifconfig tap0 172.16.0.1/24
```

### Qemu
```bash
qemu-system-arm -kernel <KERNEL> -cpu <CPU> -m <RAM-MB> -M versatilepb -serial stdio -append "root=/dev/sda2 roofstype=ext4 rw" -hda <IMAGE> -net nic -net tap,ifname=tap0,script=no,downscript=no -no-reboot
```

### Static IP
```bash
sudo ifconfig eth0 172.16.0.2/24
```
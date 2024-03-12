# build手順

## Build linux

```
cd packages/linux-kernel
git clone -b v5.4.268 https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git
./build-kernel.sh
```

## Build linux-firmware

```
cd packages/linux-kernel
git clone https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git
./build-linux-firmware.sh
```

## Build wireguard

```
cd packages/linux-kernel
git clone https://salsa.debian.org/debian/wireguard-linux-compat.git
cd packages/linux-kernel/wireguard-linux-compat
git checkout debian/1.0.20201112-1_bpo10+1
cd packages/linux-kernel
./build-wireguard-modules.sh
```

## Copy build-modules

```
cd packages/linux-kernel
cp *.deb ../
```

## Build iso image

```
cd ./
./configure --architecture amd64 --build-by "github.com/irumaru"
sudo make iso
```

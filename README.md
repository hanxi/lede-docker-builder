# lede 的 docker 编译环境

### clone docker and build image

```
git clone https://github.com/hanxi/lede-docker-builder.git
cd lede-docker-builder
docker build -t lede .
```

### run container and clone lede code

```
docker run --rm -it -v $(pwd)/data:/root lede
git clone --depth 1 https://github.com/coolsnowwolf/lede -b master openwrt

cd openwrt
../diy-part1.sh
./scripts/feeds update -a 
./scripts/feeds install -a
../diy-part2.sh

cp ../.config .
make menuconfig 

#Download package
make defconfig
make download -j8
find dl -size -1024c -exec ls -l {} \;
find dl -size -1024c -exec rm -f {} \;

# First Compile the firmware
make -j1 V=s

# Second Compile the firmware
make -j$(($(nproc) + 1))
```


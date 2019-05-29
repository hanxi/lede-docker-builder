# lede 的 docker 编译环境

### clone docker and build image

```
git clone https://github.com/hanxi/lede-docker-builder.git
cd lede-docker-builder
docker build -t lede - < Dockerfile
```

### run container and clone lede code

```
docker run --rm -it -v $(pwd)/data:/root lede
git clone https://github.com/coolsnowwolf/lede
cd lede
./scripts/feeds update -a 
./scripts/feeds install -a
make menuconfig 
```


## Start

```bash
docker build -t han3zeng/d2l .
```

```bash
docker run --rm -it \
    -p 8888:8888 \
    -v "$PWD/src":/usr/local/app/src \
    han3zeng/d2l
```
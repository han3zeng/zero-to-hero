# Zero to Hero
The repos is implementation and course note from the repo [zero-to-hero](https://github.com/karpathy/makemore?tab=readme-ov-file)


## Start

```bash
docker build -t han3zeng/zth .
```

```bash
docker run --rm -it \
    -p 8888:8888 \
    -v "$PWD/src":/usr/local/app/src \
    han3zeng/zth
```
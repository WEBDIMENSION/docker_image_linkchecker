# Linkchecker

## Usage

### Example Docker-compose

#### Docker-compose Structure

```bash
├── docker-compose.yml
├── output
│   └── report
└── src
    └── linkchecker.sh
```

#### .env

```env
DIR_PATH=.
PROJECT_NAME=linkchecker # As you like
TARGET_URL=<<TARGET_URL>>
```

#### docker-compose.yml

```yml
version: "3"
services:
  linkchecker:
    image: ghcr.io/webdimension/linkchecker:latest
    container_name: ${PROJECT_NAME}_linkchecker
    volumes:
      - ${DIR_PATH}/docker/output:/workspace/output
      - ${DIR_PATH}/docker/src:/workspace/src
    environment:
      - TARGET_URL=${TARGET_URL}
    working_dir: /workspace/src
    entrypoint: "/bin/sh -c './linkchecker.sh'"
```

#### src/linkchecker.sh

```sh
linkchecker -o text -Fhtml//workspace/output/report/linkchecker.report.html "$TARGET_URL"
```

#### docker-compose 実行

```bash
docker-compose run --rm linkchecker
```

### Example Docker

### Docker Structure

```bash
├── output
│   └── report
└── src
    └── linkchecker.sh
```

### Docker-compose `src/linkchecker.sh`

```sh
linkchecker -o text -Fhtml//workspace/output/report/linkchecker.report.html <<TargenURL>>
# Example
# linkchecker -o text -Fhtml//workspace/output/report/linkchecker.report.html http://localhost:9000
```

### docker 実行

```bash
# Image pull
docker pull ghcr.io/webdimension/linkchecker:1.0.0

# Exec
docker run --rm \
-v /Users/garaccii/CloudStation/workspace/projects/GitHub/linkchecker/src:/workspace/src \
-v /Users/garaccii/CloudStation/workspace/projects/GitHub/linkchecker/output:/workspace/output \
--workdir="/workspace/src" \
--entrypoint "./linkchecker.sh" \
--name linkchecker ghcr.io/webdimension/linkchecker:latest
```

## 解析ファイル

`output/repo/xxxx` にファイルが生成される

## linkchecker usage

`Over Write src/linkchecker`

```bash
# Format html
linkchecker -o text -Fhtml/report/linkchecker.report.html http://localhost
```

```bash
# create sitemap
linkchecker -o text -Fsitemap/report/linkchecker.report.sitemap http://localhost
```

```bash
# Format CSV
linkchecker --no-status -v  -o text -Fcsv/report/linkchecker.report.csv http://localhost
```

```bash
# Format SQL
linkchecker -o text -Fsql/report/linkchecker.report.sql http://loalhost
```

```bash
# Format dotL
linkchecker -o text -Fdot/report/linkchecker.report.dot http://loalhost
```

```bash
# Format failures
linkchecker -o text -Ffailures/report/linkchecker.report.failures http://loalhost
```

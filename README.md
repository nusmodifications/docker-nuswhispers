# Docker Images for NUSWhispers

> Run NUSWhispers web stack using Docker.

## Containers
- nginx
- php-fpm
- MariaDB
- Redis
- Workspace (for running `composer`, `npm` operations)
- Data (for databases' persistence)
- Application (mapped to NUSWhispers source code)

## Requirements
- Docker for Mac / Windows

## Setup
Assuming your work directory is `~/Projects/`:

1) Checkout NUSWhispers source code:
```
cd ~/Projects
git clone https://github.com/nusmodifications/nuswhispers.git
```

2) Checkout this repository; it should be on the same folder as `nuswhispers`:
```
cd ~/Projects
git clone https://github.com/nusmodifications/docker-nuswhispers.git
```

3) Setup for the first time:
```
cd docker-nuswhispers
docker-compose up
```

## Usage

**Example:** Running all containers in the background:
```
docker-compose up -d
```

**Example:** Destroying all containers:
```
docker-compose down
```

**Example:** Run bash in workspace container:
```
docker exec -it {workspace-container-name} bash
```

## Credits
- [Laradock](https://github.com/LaraDock/)

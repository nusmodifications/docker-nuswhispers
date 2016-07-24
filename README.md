# Docker Images for NUSWhispers

> Run NUSWhispers web stack using (Native) Docker.

## Containers
- nginx
- hhvm
- MariaDB
- Redis
- Workspace (for running `composer`, `bower`, `npm`, and `gulp` operations)
- Data (for databases' persistence)
- Application (mapped to NUSWhispers source code)

## Requirements
- Docker for Mac / Windows

## Setup
Assuming your work directory is `~/Projects/`:

1) Checkout NUSWhispers source code (this assumes `remove-vagrant` branch is merged into master):
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

_TODO_

## Known Issues

_TODO_

## Credits
- [Laradock](https://github.com/LaraDock/)

# One Piece Deploy

- One piece deploy method, you can find data-only which only includes datatbase, RMQ, KAFKA, Cache or other stuffs but not including services and app layer.
  But services deploy includes above all plus services and app layer. We use makefile to execute script to make our life easier.

## Prerequisite

- Here are some essential tools that you need to have to running project properly, and some optional tools if you want to change the repository.
And please feel free to make any changes that suit your interest.

- [docker](https://www.docker.com/)
- [make](https://www.gnu.org/software/make/)

### Get Started

- If you are not going to make any changes, the only two things you need is inside `docker-compose.yaml` and `Makefile`. To execute and running the application.
You can start with `make help` to see what kinds of commands you can use. That's get started.

#### Helper command

- list all commands available for make

```bash
make help
```

#### Build command

** Additional info `${c}` can be replace with any `container_name` which you wanted to spin up a specific container wich command **

- build the image from Dockerfile. In our applications we have a server build on top of Nestjs framework, and Vue Typescript frontend binding with Nginx.

```bash
make build                          # building all containers
make build c=onepiece-gateway-redis # building gateway redis only
```

#### Up command

- Stopping and recreating the containers

```bash
make up                          # Up all containers
make up c=onepiece-gateway-redis # Up gateway redis only
```

#### Start command

- Is used to start the containers. To start only one container for example if I only want to start db container run `make start c=database`

```bash
make start                          # start all containers
make start c=onepiece-gateway-redis # start gateway redis only
```

#### Down command

- Is used to stop and remove containers. To delete specific container use for example if I only want to delete db container run `make down c=database`

```bash
make down                          # down all containers
make down c=onepiece-gateway-redis # down gateway redis only
```

#### Restart command

- Is used to restart containers. To restart specific container use for example if I only want to restart db container run `make down c=database`

```bash
make down                          # down all containers
make down c=onepiece-gateway-redis # down gateway redis only
```

#### Logs command

- Is used to see the log of the containers. To log specific container use for example if I only want to log db container run `make log c=database`

```bash
make log                          # log all containers
make log c=onepiece-gateway-redis # log gateway redis only
```

#### Sh command

- Is used to see sh into containers. To sh specific container use for example if I only want to sh server container run `make sh c=movies-server`

```bash
make sh c=onepiece-gateway-redis # sh gateway redis only
```

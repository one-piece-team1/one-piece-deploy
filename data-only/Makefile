# --------------------------------------------------------------------
# Copyright (c) 2021 AHOY!APP, The Taiwans. All Rights Reserved.
# Author(s): libtery
# 
# This software may be modified and distributed under the terms of the
# MIT license. See the LICENSE file for details.
# --------------------------------------------------------------------

PWD ?= pwd_unknown
PROJECT_NAME = $(notdir $(PWD))
SERVICE_TARGET := master

# if vars not set specifially: try default to environment, else fixed value.
# strip to ensure spaces are removed in future editorial mistakes.
# tested to work consistently on popular Linux flavors and Mac.
ifeq ($(user),)
# USER retrieved from env, UID from shell.
HOST_USER ?= $(strip $(if $(USER),$(USER),nodummy))
HOST_UID ?= $(strip $(if $(shell id -u),$(shell id -u),4000))
else
# allow override by adding user= and/ or uid=  (lowercase!).
# uid= defaults to 0 if user= set (i.e. root).
HOST_USER = $(user)
HOST_UID = $(strip $(if $(uid),$(uid),0))
endif

THIS_FILE := $(lastword $(MAKEFILE_LIST))
CMD_ARGUMENTS ?= $(cmd)

check:
				@echo $(THIS_FILE)
				@echo $(CMD_ARGUMENTS)
help: ## list all commands available for make
				@IFS=$$'\n' ; \
				help_lines=(`fgrep -h "##" $(MAKEFILE_LIST) | fgrep -v fgrep | sed -e 's/\\$$//'`); \
				for help_line in $${help_lines[@]}; do \
								IFS=$$'#' ; \
								help_split=($$help_line) ; \
								help_command=`echo $${help_split[0]} | sed -e 's/^ *//' -e 's/ *$$//'` ; \
								help_info=`echo $${help_split[2]} | sed -e 's/^ *//' -e 's/ *$$//'` ; \
								printf "%-30s %s\n" $$help_command $$help_info ; \
				done
build: ## build the image from Dockerfile. In our applications we have a server build on top of Nestjs framework, and Vue Typescript frontend binding with Nginx
				docker-compose -f docker-compose.yaml build $(c)
up: ## Stopping and recreating the containers
				docker-compose -f docker-compose.yaml up -d $(c)
start: ## Is used to start the containers. To start only one container for example if I only want to start db container run `make start c=database`
				docker-compose -f docker-compose.yaml start $(c)
down: ## Is used to stop and shutdown containers. To shutdown specific container use for example if I only want to shutdown db container run `make down c=database`
				docker-compose -f docker-compose.yaml down $(c)
destroy: ## Is used to destroy containers. To destroy specific container use for example if I only want to destroy db container run `make destroy c=database` 
				docker-compose -f docker-compose.yaml down -v $(c)
stop: ## Is used to stop containers. To stop specific container use for example if I only want to stop db container run `make destroy c=database` 
				docker-compose -f docker-compose.yaml stop $(c)
restart: ## Is used to restart containers. To restart specific container use for example if I only want to restart db container run `make down c=database`
				docker-compose -f docker-compose.yaml stop $(c)
				docker-compose -f docker-compose.yaml up -d $(c)
logs:	## Is used to see the log of the containers. To log specific container use for example if I only want to log db container run `make log c=database`
				docker-compose -f docker-compose.yaml logs --tail=100 -f $(c)
ps: ## Is used to list the containers. To list specific container use for example if I only want to list db container run `make log c=database`
				docker-compose -f docker-compose.yaml ps $(c)
sh: ## Is used to see sh into containers. To sh specific container use for example if I only want to sh server container run `make sh c=movies-server`
				docker exec -it $(c) sh
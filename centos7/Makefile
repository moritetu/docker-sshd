NAME   ?= centos7-sshd
TAG    ?= latest
IMAGE  ?= $(NAME):$(TAG)
PORT   ?= 10022
HOST   ?= localhost
ARGS   ?=
CMD    ?=

all: build

build:
	docker build . -t $(IMAGE) $(ARGS)

run: build
	docker run -d -p $(PORT):22 --name $(NAME) $(ARGS) $(IMAGE) $(CMD)
	@echo "ssh login: ssh -p $(PORT) root@$(HOST)"

runp: build
	docker run -d -p $(PORT):22 --name $(NAME) $(ARGS) --privileged $(IMAGE) /sbin/init
	@echo "ssh login: ssh -p $(PORT) root@$(HOST)"

start:
	docker container start $(NAME)

stop:
	docker container stop $(NAME)

login:
	$(eval _PORT := $(shell docker inspect $(NAME) -f '{{(index (index .NetworkSettings.Ports "22/tcp") 0).HostPort }}'))
	ssh -p $(_PORT) root@$(HOST)

update-key:
	ssh-keygen -R "[$(HOST)]:$(PORT)"

clean: stop
	docker container rm -f $(NAME)
	docker image rm $(IMAGE)

help:
	@echo "usage: make [TARGET]"
	@echo ""
	@echo "build        Build container image."
	@echo "run          Run container."
	@echo "runp         Run container with priviledged mode. systemd service is running in the container"
	@echo "start        Start container."
	@echo "stop         Stop container."
	@echo "login        Login container."
	@echo "update-key   Updating host keys."
	@echo "clean        Stop container and remove image."
	@echo ""

.PHONY: all build run stop clean update-key help

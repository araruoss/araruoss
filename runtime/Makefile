SHELL := /bin/sh
COMPOSE := docker compose --env-file .env -f docker-compose.yml

.DEFAULT_GOAL := help

.PHONY: help setup build rebuild up start stop down restart update logs status ps health config clean admin-password admin-password-force

help:
	@echo "Araru runtime"
	@echo "  make setup    cria .env a partir do exemplo"
	@echo "  make build    build Server and Web"
	@echo "  make rebuild  rebuild without cache and start the stack"
	@echo "  make up       build and start the stack"
	@echo "  make start    inicia containers existentes"
	@echo "  make stop     para sem remover containers"
	@echo "  make down     remove containers e rede"
	@echo "  make restart  reinicia o stack"
	@echo "  make update   update databases and rebuild"
	@echo "  make logs     acompanha logs"
	@echo "  make status   mostra containers e health"
	@echo "  make admin-password       show the pending temporary password"
	@echo "  make admin-password-force force admin password rotation"
	@echo "  make config   validate the configuration"
	@echo "  make clean    remove local containers and images; preserve data"

setup:
	@test -f .env || cp .env.example .env
	@echo "Revise runtime/.env antes de executar make up."

build:
	$(COMPOSE) build

rebuild:
	$(COMPOSE) build --pull --no-cache
	$(COMPOSE) up -d --wait

up:
	$(COMPOSE) up -d --build --wait

start:
	$(COMPOSE) start

stop:
	$(COMPOSE) stop

down:
	$(COMPOSE) down

restart: down up

update:
	$(COMPOSE) pull postgres redis
	$(COMPOSE) build --pull
	$(COMPOSE) up -d --wait

logs:
	$(COMPOSE) logs -f --tail=200

ps status:
	$(COMPOSE) ps

health:
	@server_port=`$(COMPOSE) port server 3001 | sed 's/.*://'`; curl -fsS "http://localhost:$$server_port/ready" && echo
	@web_port=`$(COMPOSE) port web 80 | sed 's/.*://'`; curl -fsS "http://localhost:$$web_port/healthz" && echo

admin-password:
	@$(COMPOSE) up -d --build --wait postgres redis server
	@$(COMPOSE) exec -T server npm run admin:reset-password

admin-password-force:
	@$(COMPOSE) up -d --build --wait postgres redis server
	@$(COMPOSE) exec -T server npm run admin:reset-password -- --force

config:
	$(COMPOSE) config -q

clean:
	$(COMPOSE) down --rmi local

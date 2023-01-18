# Makefile commands for Hugo

unit-tests: ## Tests code
	@go test -v -short -coverprofile=coverage-units.out

lint: ## Catches errors
	@golangci-lint run ./*.go

build: lint ## Generates website
	@hugo
	@go build -o awesome-api ./*.go

run: ## Runs programs in background
	@./awesome-api >./awesome.log 2>&1 &

stop: ## Stops Programs
	@pkill awesome-api

clean: stop ## Cleans files
	@rm -Rf dist/*
	@rm -f awesome-api awesome.log || true

test: ## Tests website
	@echo "# Test 1:"
	@if curl http://localhost:9999; then \
		echo "TESTOK" ;\
	else \
		echo "TESTFAILED" ;\
	fi
	@echo "# Test 2:"
	@if curl http://localhost:9999/health; then \
		echo ""; \
		echo "TESTOK" ;\
	else \
		echo ""; \
		echo "TESTFAILED"; \
	fi

post: ## Posts content to hugo website
	@rm -Rf content/posts/$(POST_NAME).md
	@hugo new posts/$(POST_NAME).md
	@sed -i 's/title:.*/title: $(POST_TITLE)/' content/posts/$(POST_NAME).md
	@sed -i 's/draft:.*/draft: "false"/' content/posts/$(POST_NAME).md

.SILENT:
help: ## Makefile commands
	@echo "Usage: make <command>"
	@echo "-----"	
	@cat Makefile | grep "^\w*:.*##.*" | sed 's/## //'

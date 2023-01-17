lint:
	@golangci-lint run ./*.go

build:
	@hugo
	@go build -o awesome-api ./*.go

run:
	@./awesome-api >./awesome.log 2>&1 &

stop:
	@pkill awesome-api

clean:
	@rm -Rf dist/*
	@rm -f awesome-api awesome.log || true

test:
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

post:
	@rm -Rf content/posts/$(POST_NAME).md
	@hugo new posts/$(POST_NAME).md
	@sed -i 's/title:.*/title: $(POST_TITLE)/' content/posts/$(POST_NAME).md
	@sed -i 's/draft:.*/draft: "false"/' content/posts/$(POST_NAME).md

.SILENT:
help:
	@echo "Usage: make <command>"
	@echo "-----"	
	@cat Makefile | grep "^\w*:.*##.*" | sed 's/## //'

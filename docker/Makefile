.PHONY: pull build run clean push

pull:
	docker pull tomaslaz/gem5-aladdin-boat:dev

build:
	docker build . -f Dockerfile -t tomaslaz/gem5-aladdin-boat:dev

run:
	docker run -it --rm \
		--mount source=gem5-aladdin-boat-workspace,target=/workspace \
		tomaslaz/gem5-aladdin-boat:dev

clean:
	docker volume rm gem5-aladdin-boat-workspace && docker image rm tomaslaz/gem5-aladdin-boat:dev

push:
	docker push tomaslaz/gem5-aladdin-boat:dev
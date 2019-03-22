.PHONY: pull build run clean push

ifndef branch
n_branch = develop
else
n_branch = $(branch)
endif

pull:
	docker pull turingboat/gem5-aladdin-boat:$(n_branch)

build:
	docker build . -f Dockerfile -t turingboat/gem5-aladdin-boat:$(n_branch)

run:
	docker run -it --rm \
		--mount source=gem5-aladdin-boat-workspace,target=/workspace \
		turingboat/gem5-aladdin-boat:$(n_branch)

clean:
	docker volume rm gem5-aladdin-boat-workspace && docker image rm turingboat/gem5-aladdin-boat:$(n_branch)

push:
	docker push turingboat/gem5-aladdin-boat:$(n_branch)
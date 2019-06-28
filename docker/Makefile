.PHONY: clean basebuild basepush basepull build push pull run

ifndef branch
n_branch = develop
else
n_branch = $(branch)
endif

clean:
	docker volume rm gem5-aladdin-boat-workspace && docker image rm turingboat/gem5-aladdin-boat:$(n_branch)

basebuild:
	docker build . -f Dockerfile.base -t turingboat/gem5-aladdin-boat_base:latest
	
basepush:
	docker push turingboat/gem5-aladdin-boat_base:latest

basepull:
	docker pull turingboat/gem5-aladdin-boat_base:latest

build:
	docker build . -f Dockerfile -t turingboat/gem5-aladdin-boat:$(n_branch)

push:
	docker push turingboat/gem5-aladdin-boat:$(n_branch)
	
pull:
	docker pull turingboat/gem5-aladdin-boat:$(n_branch)

run:
	docker run -it --rm \
		--mount source=gem5-aladdin-boat-workspace,target=/workspace \
		turingboat/gem5-aladdin-boat:$(n_branch)

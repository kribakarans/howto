# How to build the Multi-Architecture images

## Method 1:
### Build an image for each architecture
	docker build -t kribakarans/ubuntu:amd64 .
	docker build -t kribakarans/ubuntu:arm64 .

### Push all images to docker hub repository
	docker push kribakarans/ubuntu:amd64
	docker push kribakarans/ubuntu:arm64

### Create a multi-architecture image
	docker manifest create kribakarans/ubuntu:latest kribakarans/ubuntu:amd64 kribakarans/ubuntu:arm64

### Push the multi-architecture image
	docker manifest push kribakarans/ubuntu:latest

### The image is now ready to be pulled regardless of architecture
	docker pull kribakarans/ubuntu:latest

### Login to the Ubuntu shell
	docker run -it kribakarans/ubuntu:latest bash

## Method 2: With Buildx tool
	docker buildx build --push \
	                    --platform linux/amd64,linux/arm64 \
	                    --tag kribakarans/ubuntu:latest

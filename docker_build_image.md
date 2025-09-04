# Instructions when building Docker container images on MacOS Arm64 CPU

An issue with the newer MacOS hardware is that by default Docker container images will be downloaded and run with Arm64 operating system images.

When you intend to make the image portable you will need to build container images for other platforms (e.g. AMD64, X86_64).

Below is the process:

1. Ensure Docker is running.

2. Run the following command to verify your MacOS has the ability to build images other than arm64

```
docker buildx ls
```

Your output should be similar to below in the column titled PLATFORMS

"linux/amd64 (+2), linux/arm64, linux/arm (+2), linux/ppc64le, (3 more)"

3. Download the desired continer images (or build from source).

```
docker pull <insert image name>
```

4. Create a folder for each container image and setup your Dockerfile to build your container(s).

```
mkdir <folder_name>
```

```
cd <folder_name>
```

```
vim Dockerfile
```

5. Run the container image(s) to make sure everything works as expected.

6. After verifying everything works, it is time to build a container for platforms other than what your MacOS is operating on.

```
docker buildx build --platform=linux/amd64 -t <image-name> .
```

7. Switch to the keycloak directory, modify the Dockerfile, save your changes  and run the command below

```
docker buildx build . --platform=linux/amd64 -t keycloak-demo --load
```
8. Switch to the postgresql directory, modify the Dockerfile, save your changes  and run the command below

```
docker buildx build . --platform=linux/amd64 -t postgres-demo --load
```

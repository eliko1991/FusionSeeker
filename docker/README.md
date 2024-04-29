# Build Container

cd into this folder and run:
```
docker build -t fusionseeker .
```

# SSH into container
```
docker run -it fusionseeker


```
# Run container
Note, you'll need to mount a volume (-v local_path:container_path) from your machine to the container in order for the container to see your files, and output results from the container.
```
docker run -it fusionseeker bash -c "fusionseeker {PARAMETERS}"
```

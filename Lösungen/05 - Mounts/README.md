# Bind mounts

```sh
# Variablen
MOUNT_PATH="/tmp/mydata"   
CONTAINER_NAME="my_container"  
IMAGE_NAME="alpine"

docker run -d --name $CONTAINER_NAME -v $MOUNT_PATH:/data $IMAGE_NAME tail -f /dev/null

docker exec -it $CONTAINER_NAME sh -c "echo 'Hello, World!' > /data/myfile.txt"

docker stop $CONTAINER_NAME
docker rm $CONTAINER_NAME

docker run -d --name $CONTAINER_NAME -v $MOUNT_PATH:/data $IMAGE_NAME tail -f /dev/null

if docker exec $CONTAINER_NAME sh -c "test -f /data/myfile.txt"; then
    echo "Die Datei myfile.txt ist noch vorhanden."
else
    echo "Die Datei myfile.txt ist nicht vorhanden."
fi

docker stop $CONTAINER_NAME
docker rm $CONTAINER_NAME

```

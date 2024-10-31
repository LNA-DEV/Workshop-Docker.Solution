# Volumes

- Erstellen sie ein Volume
- Erstellen sie einen Container und binden das Volume ein
- Verbinden sie sich mithilfe des exec Befehls in den Container
- Erstellen sie im Container und Volume Pfad eine Datei
- Löschen sie den Container
- Binden sie das Volume in einen neuen Container ein und überprüfen sie ob die erstellte Datei noch vorhanden ist
- Löschen sie das Volume

```sh
VOLUME_NAME="mein_volume"
CONTAINER_NAME="mein_container"
FILE_PATH="/data/testdatei.txt"

# 1. Erstellen eines Volumes
echo "Erstelle ein Docker Volume..."
docker volume create $VOLUME_NAME

# 2. Erstellen eines Containers und Einbinden des Volumes
echo "Starte Container und binde Volume ein..."
docker run -d --name $CONTAINER_NAME -v $VOLUME_NAME:/data alpine sleep infinity

# 3. Verbinden mit dem Container
echo "Verbinde mich mit dem Container und erstelle eine Datei im Volume-Pfad..."
docker exec $CONTAINER_NAME sh -c "echo 'Hallo, Welt!' > $FILE_PATH"

# Überprüfen, ob die Datei erfolgreich erstellt wurde
echo "Überprüfe, ob die Datei erstellt wurde..."
docker exec $CONTAINER_NAME ls -l $FILE_PATH

# 4. Löschen des Containers
echo "Lösche den Container..."
docker rm -f $CONTAINER_NAME

# 5. Einbinden des Volumes in einen neuen Container und Überprüfung der Datei
echo "Starte neuen Container und binde Volume ein..."
docker run --rm --name neuer_container -v $VOLUME_NAME:/data alpine sh -c "cat $FILE_PATH"

# 6. Löschen des Volumes
echo "Lösche das Volume..."
docker volume rm $VOLUME_NAME
```

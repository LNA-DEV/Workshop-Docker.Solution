# Networks

- Erstellen sie ein Docker Netzwerk (Bridge)
- Füge sie mehrere Container dem Netzwerk hinzu
- Verbinden sie sich auf einen der Container und versuchen sie den anderen zu erreichen
- Erstellen sie ein weiteres Netzwerk (Host)
- Testen sie die Unterschiede zwischen dem Host und Bridge Netzwerk

```sh
# Docker Netzwerk erstellen (Bridge)
echo "Erstelle ein Docker Netzwerk (Bridge)..."
docker network create --driver bridge my_bridge_network

# Mehrere Container im Bridge-Netzwerk starten
echo "Starte zwei Container und füge sie dem Bridge-Netzwerk hinzu..."
docker run -d --name container1 --network my_bridge_network alpine sleep 3600
docker run -d --name container2 --network my_bridge_network alpine sleep 3600

# Teste die Verbindung zwischen den Containern im Bridge-Netzwerk
echo "Verbinde zu 'container1' und pinge 'container2' im Bridge-Netzwerk..."
docker exec container1 ping -c 4 container2

# Ein weiteres Netzwerk erstellen (Host)
echo "Erstelle ein weiteres Netzwerk (Host)..."
docker network create --driver host my_host_network

# Container im Host-Netzwerk starten
echo "Starte zwei Container und füge sie dem Host-Netzwerk hinzu..."
docker run -d --name container3 --network host alpine sleep 3600
docker run -d --name container4 --network host alpine sleep 3600

# Teste den Unterschied zwischen Host- und Bridge-Netzwerk
echo "Teste die Verbindung im Host-Netzwerk..."
docker exec container3 ping -c 4 127.0.0.1

# Zusammenfassung
echo "Zusammenfassung der Ergebnisse:"
echo "1. Im Bridge-Netzwerk können sich die Container über ihre Namen erreichen."
echo "2. Im Host-Netzwerk teilen sich die Container den gleichen Netzwerk-Stack wie der Host selbst."
echo "   Hier ist die direkte Kommunikation zwischen Containern eher eingeschränkt und funktioniert anders als im Bridge-Netzwerk."

# Cleanup
read -p "Möchten Sie die erstellten Container und Netzwerke löschen? (y/n): " cleanup
if [ "$cleanup" == "y" ]; then
    echo "Entferne Container und Netzwerke..."
    docker rm -f container1 container2 container3 container4
    docker network rm my_bridge_network
    # Host-Netzwerk wird nicht entfernt, da es sich um das Standard-Netzwerk handelt
else
    echo "Cleanup übersprungen."
fi
```

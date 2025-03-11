# ROS 2 Paketlisten-Dokumentation

Dieses Repository enthält verschiedene Textdateien, die Informationen über installierte ROS 2 Pakete und Abhängigkeiten speichern. Die Dateien wurden mit den folgenden Befehlen generiert.

---

## Generierung der Dateien

### 1. Installierte ROS 2 Python-Pakete (über `pip`)
```bash
pip freeze | grep ros > installed_ros_python_packages.txt
```
Diese Datei listet alle ROS 2 Python-Pakete auf, die mit pip installiert wurden.

**Warum pip freeze statt pip list?**
- pip freeze gibt exakte Versionsspezifikationen aus, sodass die Ausgabe direkt für eine requirements.txt verwendet werden kann.
- pip list zeigt die installierten Pakete an, aber ohne eine Formatierung, die für eine spätere Installation nützlich ist.

### 2. Installierte ROS 2 Pakete (über `apt`)
```bash
dpkg -l | grep ros-iron > installed_ros_packages.txt
```
Hier werden alle ROS 2 Pakete aufgelistet, die über apt installiert wurden und zum ROS 2 Iron Release gehören.

**Alternative**
- Der Befehl `dpkg --get-selections > installed_packages.txt` listet alle installierten Pakete auf, nicht nur ROS 2.
- Falls nur ROS 2 Pakete von Interesse sind, reicht `dpkg -l | grep ros-iron` aus.

### 3. Alle aktuell erkannten ROS 2 Pakete im System
```bash
ros2 pkg list > ros2_detected_packages.txt
```
Dieser Befehl gibt eine Liste aller ROS 2 Pakete aus, die vom aktiven ROS 2 Setup erkannt werden. Dazu gehören:
- ROS 2 Pakete, die über apt installiert wurden
- Pakete aus dem Workspace, falls `source install/setup.bash` oder `source devel/setup.bash` ausgeführt wurde

**Hinweis**: Falls der ROS 2 Workspace nicht gesourct wurde, erscheinen hier nur die systemweit installierten Pakete.

### 4. Eigene ROS 2 Pakete im Workspace
```bash
ls -1 ~/my_ros_workspace/src > my_ros_workspace_packages.txt
```
Hier werden alle ROS 2 Pakete aufgelistet, die sich direkt im src/-Verzeichnis des angegebenen Workspaces befinden.
Dies hilft, eine Übersicht über selbst entwickelte oder aus dem Source-Code kompilierte Pakete zu behalten.

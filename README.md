# Automatic Skeleton Marker Relation

### Luke Mikat, Abraham Neme Alvarez, Valdone Zabutkaite

## Problemstellung

Beim markerbasierten Motion Capturing (MoCap) werden Marker auf den Körper platziert. Es ist jedoch nicht immer möglich, alle Marker genau dort zu platzieren, wo sie idealerweise hingehören. Dadurch fehlt die Relation zwischen den Markern und dem Skelett, was bedeutet, dass man nicht mehr von den Markern auf das Skelett zurückschließen kann.

## Lösungsansatz

Um die Relation zwischen den MoCap-Markern und dem Skelett zu verbessern, wird vorgeschlagen, auf bestehende Forschungsarbeiten zurückzugreifen, die parametrische Menschenmodelle wie SMPL (Skinned Multi-Person Linear Model) verwenden. Diese Modelle können in Tiefenaufnahmen von RGBD-Kameras, beispielsweise der Kinect, eingebettet werden. 

Die Hauptidee besteht darin, zunächst das SMPL-Modell auf die Tiefenaufnahmen zu fitten und in einem zweiten Schritt die MoCap-Marker zu erkennen und deren Relation zum SMPL-Modell herzustellen. Durch die Verwendung des SMPL-Modells könnte man eine präzisere Positionierung der Marker erreichen, da das Modell detaillierte Informationen über die Körperform und -struktur liefert. Sobald das Modell angepasst ist, könnte die Position der Marker relativ zum Modell berechnet werden. Das würde eine genaue Relation zwischen den Markern und dem Skelett ermöglichen.

## Vorgehensweise

1. **Untersuchung bestehender Ansätze:**
   - Avatar Project - Anpassung von 3D-Modellen an reale Personen
   - RVH Mesh Registration - Registrierung von 3D-Meshes auf reale Personen

2. **Nutzung und Testen eines SMPL-Renderers:**
   - Die vorhandenen Ansätze zum Rendern von SMPL 3D-Modellen sollen zum Laufen gebracht und mittels Tiefenaufnahmen von RGBD-Kameras getestet werden.

3. **Markererkennung und Zuordnung:**
   - Im nächsten Schritt wird die Erkennung der MoCap-Marker in den Tiefenaufnahmen vorgenommen. Diese Marker werden dann dem SMPL-Modell zugeordnet, um deren genaue Position relativ zum Skelett zu bestimmen.

4. **Evaluierung des SMPL-Modells:**
   - Nach der erfolgreichen Implementierung des SMPL-Modells wird dessen Performance in Bezug auf das Fitting in Kinect-Videos evaluiert. Dabei wird darauf geachtet, wie gut das Modell die Bewegungen der erfassten Person nachbilden kann und wie genau das resultierende Skelett ist.

## Dependencies

- **[Boost 1.58](https://sourceforge.net/projects/boost/files/boost/1.58.0/):** [Boost](https://www.boost.org) ist eine Sammlung von hochqualitativen, plattformübergreifenden C++ Bibliotheken, die oft als Erweiterungen der Standardbibliothek dienen. Sie bietet Lösungen für eine Vielzahl von Programmieraufgaben, darunter Datenstrukturen, Algorithmen, Multithreading, und vieles mehr. Boost wird häufig als Grundlage für die Entwicklung von C++ Projekten verwendet und ist bekannt für seine robuste und gut getestete Implementierung.

- **[OpenCV 3.3+](https://sourceforge.net/projects/opencvlibrary/files/) (OpenCV 4 wird nicht unterstützt):** [OpenCV](https://opencv.org) ist eine umfangreiche Open-Source-Bibliothek, die für Echtzeit-Computer-Vision-Anwendungen entwickelt wurde. Sie bietet eine Vielzahl von Algorithmen und Funktionen zur Bildverarbeitung, Objekt- und Gesichtserkennung, Bewegungsverfolgung und vielem mehr.

- **[Eigen 3.3.4](https://community.chocolatey.org/packages/eigen/3.3.4):** Eine vielseitige, plattformübergreifende C++ Bibliothek für lineare Algebra, die sich auf Matrizen- und Vektorenoperationen spezialisiert. [Eigen](https://eigen.tuxfamily.org/index.php?title=Main_Page) bietet leistungsstarke und flexible Tools für numerische Berechnungen, darunter Eigenwertprobleme und lineare Gleichungssysteme. Andere Download-Möglichkeit: [Gitlab](https://gitlab.com/libeigen/eigen/-/releases/3.3.4).

- **[Ceres Solver 1.14](https://github.com/ceres-solver/ceres-solver/tree/1.14.x) (Ceres 2 wird nicht unterstützt):** Eine leistungsstarke C++ Bibliothek zur Lösung von nichtlinearen Optimierungsproblemen. Sie wird oft in Bereichen wie Computer Vision und Robotik eingesetzt, um Probleme wie Kamerakalibrierung und 3D-Rekonstruktion zu lösen. Ceres Solver unterstützt verschiedene Optimierungsalgorithmen und bietet die Möglichkeit, mit großen und komplexen Datensätzen effizient umzugehen, insbesondere wenn sie mit LAPACK und OpenMP kompiliert wird. Weiteres über diese Bibliothek und ihre Installation: [Ceres Solver](http://ceres-solver.org).

- **[zlib](https://www.zlib.net/zlib131.zip):** [Zlib](https://www.zlib.net) ist eine weit verbreitete, plattformübergreifende C-Bibliothek zur Datenkompression. Sie bietet Funktionen zur schnellen und effizienten Komprimierung und Dekomprimierung von Daten, die in vielen Anwendungen und Dateiformaten verwendet werden, einschließlich PNG-Bilddateien und HTTP-Kommunikation. zlib ist bekannt für seine hohe Performance und geringe Speicheranforderungen, was es ideal für ressourcenbeschränkte Umgebungen macht.

   Eine der folgenden (erforderlich für Live-Demo):
- **[K4A](https://github.com/microsoft/Azure-Kinect-Sensor-SDK/blob/develop/docs/usage.md):** [Azure Kinect SDK](https://learn.microsoft.com/de-de/azure/kinect-dk/sensor-sdk-download) ist eine Software-Entwicklungsplattform von Microsoft, die zur Nutzung und Steuerung der Azure Kinect Development Kit Hardware dient. Sie bietet APIs für den Zugriff auf die Tiefenkamera, die RGB-Kamera, den IMU-Sensor und das Mikrofonarray der Azure Kinect. Extra-Dependency: [Depth Engine](https://github.com/microsoft/Azure-Kinect-Sensor-SDK/blob/develop/docs/depthengine.md).

- **libfreenect2:** Eine Open-Source-Bibliothek zur Ansteuerung und Nutzung der Kinect for Windows v2 (Kinect v2) Sensorhardware. Sie bietet Treiber und APIs, um auf die Tiefen-, Infrarot- und RGB-Kameradaten des Kinect v2 Sensors zuzugreifen.

   Optional:
- **PCL 1.8+:** Point Cloud Library ist eine Open-Source-Bibliothek für die Verarbeitung und Analyse von Punktwolken. Sie bietet zahlreiche Algorithmen für Aufgaben wie Filterung, Merkmalsextraktion, Registrierung, Segmentierung und Visualisierung von 3D-Punktwolken. PCL wird häufig in der Robotik, Automatisierung und Computer Vision eingesetzt, um präzise 3D-Modelle und Umgebungswahrnehmung zu ermöglichen.

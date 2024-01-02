# Praxiserfahrung

## Effect of Algorithms and Hyperparameters on Sim2Real Transfer (Masterarbeit)
- Schwerpunkte: Roboter-Aufgben, Training und Inferenz von RL Modelle, Sim2Real Transfer, Visualisierung der Ergebnisse.
- Details:
1. Definieren der erforderlichen Roboter-Aufgaben: Reach, Push, PnP. Finden eines RLPakets (SB3) sowie der zu evaluierenden Algos und HPs.
2. Finden und Anpassen einer geeigneten Simulationsumgebung (myGym) für das Training der RL-Agenten.
3. Probe-Training in der Simulationsumgebung mit Algorithmen aus dem RL-Paket unter Verwendung der Standard-Hyperparameter.
4. Analyse des Trainingsprozesses (mit Weight & Bias), Festlegung von Reward-Funktionen für verschiedene Roboter-Aufgaben und der erforderlichen Trainingszeit.
5. Training mehrerer RL-Modelle mit verschiedenen Hyperparametern und Algorithmen auf einem Cloud-Server, jeweils angepasst an unterschiedliche Roboter-Aufgaben.
6. Implementierung der Modelle in einer realen Umgebung (Niryo Robot), Evaluation und Visualisierung (mit autorl-landscape) der Leistungsunterschiede aller Modelle.
7. Zusammenfassung der Erkenntnisse über den Einfluss von Hyperparametern und Algorithmen auf den Sim2Real-Transfer.
- Fazit:
  Bei der SAC-Training für die Reach-Aufgaben der Roboter führte die Verwendung einer mittleren learning-rate und niedrigerer discount-factor schnell zu einer verbesserten Leistung des Trainingsmodells in der realen Umgebung, um die Lücke beim Sim2Real-Transfer zu verringern. Diese Studie ist jedoch nicht ausgereift, da aufgrund von Zeitbeschränkungen nicht viele Hyperparameter-Kombinationen und Seed-Gruppen gewählt wurden, was zu weniger glatten Ergebnissen und erhöhter Zufälligkeit führte. Die Verallgemeinerung der Trainingszeit führte dazu, dass einige Hyperparameter-Kombinationen im Trainingsumfeld nicht erfolgreich trainiert wurden, was die Aussagekraft für den Sim2Real-Transfer reduzierte.
![image](https://github.com/engineerkong/Learning_Notes/assets/89781823/133bc288-7434-4ce3-b782-0e7ff6f3b43c)
![image](https://github.com/engineerkong/Learning_Notes/assets/89781823/fb065914-6584-447a-8064-cc022dcaed1c)

## Technical Support (Praktikum)
- Schwerpunkte: KI Anwendung, IoT, Kundensupport
- Details:
1. Hikvision-Kameras und andere intelligente Geräte bieten viele KI-Anwendungen, wie Gesichtserkennung, Bewegungserkennung usw. Als Technical Support verstand ich zuerst alle diese Funktionen und ihre Anwendungsmethoden vollständig. Außerdem beherrschte ich die Verbindung zwischen intelligenten Geräten, was Kenntnisse im Bereich des Internet of Thing umfasst. Dies sind die grundlegenden Kenntnisse, um die Produkte zu testen.
2. Ich war häufig in Kontakt mit Firmenkunden, um ihnen neue Produkte und Funktionen von Hikvision in Form von Präsentationen vorzustellen. Ich sammlte auch deren Vorschläge und Ideen und leitete sie nach einer Auswahl an die Entwicklungsabteilung weiter, um die Produkte zu optimieren. Neben Firmenkunden haben auch Einzelhandelskunden oft Fragen zur Anwendung und Qualität der Produkte, die ich ebenfalls beantwortete.

## Software Entwickler (HiWi)
- Schwerpunkte: Entwicklung von Asynchronisierung und GUI durch Workflow
- Details:
  Ich entwickelte eine Software namens TEQO im Rahmen der Teamarbeit. TEQO ist eine physikalische Messsoftware, die auf Plexy als Baseline basiert und speziell für einige physikalische Messgeräte in unserem Forschungsinstitut konzipiert ist. Diese Software ermöglicht es, Geräte zu steuern und zu konfigurieren und physikalische Ergebnisse als Feedback zu erhalten. Der Einsatzprozess ist jedoch nicht parallel. Zudem wird die Bedienung über eine grafische Benutzeroberfläche (GUI) realisiert. Nach meiner Entwicklung konnten einige physikalische Messgeräte sowie die GUI im Simulationsmessprozess teilweise parallel betrieben werden. Der von mir entwickelte Code wurde nach den CI/CD-Tests automatisiert entwickelt, getestet und ausgeliefert.

## Simultane Form- und Posen-Rekonstruktion von Verkehrsteilnehmern für Überwachungskameras und LiDAR-Punktwolken (Studienarbeit)
- Schwerpunkte: Training und Inferenz von DL Modelle, LiDAR Punktwolke, 3D Rekonstruktion
- Details:
1. Finden und Anpassen von zwei DL-Modellen, eines zur Erkennung von Autos (GSNet) und eines zur Erkennung von Fußgängern (Alphapose).
2. Trainieren der DL-Modelle mit beschrifteten Daten.
3. Einsatz der beiden trainierten DL-Modelle zur Vorhersage in Versuchsvideos, um die 2D-Position und -Haltung von Autos und Fußgängern in jeder Bildsequenz zu erkennen.
4. Anwendung der ICP-Methode zur Umwandlung dieser 2D-Informationen in 3D-Informationen, einschließlich der Transformation zwischen Welt-, Objekt-, Kamera- und Bildkoordinatensystemen.
5. Entfernung von Punkten auf der Ebene und Ausreißern aus den Ergebnissen und Abgleich mit der LiDAR-Punktwolke der entsprechenden Versuchsdaten mittels KD-Baum-Methode zur Gewinnung von 3D-Positionsdaten. Anwendung der PCA-Methode zur Bestimmung der 3D-Haltungsinformationen.
- Fazit:
  Die Kombination von Kameras und LiDAR kann genaue 3D-Informationen über Verkehrsteilnehmer liefern, was eine höhere Genauigkeit als die direkte Vorhersage von 3D-Informationen durch DL in Kameras bietet. Allerdings werden nur einige Verkehrsteilnehmer erkannt, und die 3D-Haltungsinformationen können die Ausrichtung der Fahrzeuge nicht genau darstellen. Diese Aspekte bedürfen weiterer Forschung und Verbesserung.
![image](https://github.com/engineerkong/Learning_Notes/assets/89781823/5155909d-08f9-46bc-9bbe-1b23cb709afd)

## Entwurf und Simulation flexibler Manipulatoren (Bachelorarbeit)

- Details:
  Dies ist ein Artikel über mechanisches Design. Er beschreibt eine einzigartige Art von flexibler Roboterhand, die sich von traditionellen Zwei-Klauen-Roboterhänden unterscheidet. Das Design dieser flexiblen Roboterhand basiert auf der Methode, Gas in einen abgeschlossenen Silikonkörper zu injizieren und es wieder abzulassen. Wenn das Gas voll ist, sind die Finger in einer aufrechten Position; wenn das Gas abnimmt, biegen sich die Finger aufgrund der Form des internen Stützelements. Ich habe das Design dieser Roboterhand mit der UG-Software abgeschlossen und die Belastungssituation beim Greifen von Objekten mit der ANSYS-Software analysiert.
![image](https://github.com/engineerkong/Learning_Notes/assets/89781823/efcf403f-f69c-49aa-8293-5ba83985dfb9)

## Robomaster Designer (Wettbewerb)
- Details:
  Dies ist die Beschreibung des Roboter-Kampfwettbewerbs, veranstaltet von DJI. In diesem Wettbewerb gewinnen die Roboter, indem sie feindliche Roboter beschießen und deren Lebenspunkte verringern. Der Autor nahm an diesem Wettbewerb teil und war verantwortlich für das Design und die Herstellung der Roboterstruktur sowie für Teile der Bewegungs- und Sehalgorithmen des Roboters. Der Hauptfokus des Autors lag auf einem Roboter, der bewegliche Objekte auf dem Spielfeld greift, um dem eigenen Roboter einen Vorteil (Buff) zu verschaffen. Zuerst entwarf er mit der UG-Software die dreidimensionalen Zeichnungen des Roboters, dann fertigte er mit 3D-Druck, Laserschneiden und CNC-Maschinen die einzelnen Komponenten an, montierte sie und fügte Antriebselemente wie Zylinder und Elektroschocker hinzu. Anschließend entwickelte der Autor den Sehalgorithmus des Roboters, damit dieser mit Unterstützung von Computer Vision die Greifaufgaben ausführen konnte. Am Ende erreichte das Roboterteam seiner Schule einen der Top 32 Plätze in ganz China.
![image](https://github.com/engineerkong/Learning_Notes/assets/89781823/365121d5-7e51-4e1f-a6e6-33a43031cc67)
![Weixin Image_20240102144801](https://github.com/engineerkong/Learning_Notes/assets/89781823/2b677426-7ffc-4c4e-a188-8d59d6aaf4a7)
![Weixin Image_20240102144039](https://github.com/engineerkong/Learning_Notes/assets/89781823/4a99c62e-761f-4850-81b9-72211687815f)

# Kurse

## Zertifikate
### Microsoft AI
- Details:
  Microsoft Azure beinhaltet verschiedenen Dienste einschließlich Storage, Database, Computing, Analytics, DevOps, Network sowie andere Dienste, die für die Datenspeicherung, -verarbeitung und -anwendung verwendet werden. Im AZ-900 Zertifikat habe ich hauptsächlich einen Überblick über Azure und diese Dienste erlangt. Im AI-900 Zertifikat habe ich spezifisch ML Studio angewendet, einschließlich der Nutzung von Computer Vision, Custom Vision, Language Service, Speech Service, Document Intelligence und Azure ML Studio. Im DP-900 Zertifikat habe ich ein tieferes Verständnis von Daten, wie sie von Azure definiert werden, erlangt. Ich habe auch gelernt, wie man in Azure verschiedene Daten speichert und verarbeitet, und Daten mit den umfangreichen Azure Data Analytics Werkzeuge analysiert.
## Master
### Machine Learning
- Hier habe ich das Wissen über die Grundlagen von Machine Learning erlernt. Von Einzelnen Neuronen bis zur tiefen Netzstruktur, vom Feed-forward bis zur Backpropagation. Im Kurs wurden auch Supervised, Semi-Supervised, Unsupervised sowie Reinforcement Learning studiert und angewendet, was auch in den zuvor erwähnten praktischen Erfahrungen berücksichtigt wurde. Darüber hinaus habe ich auch die Evaluierungsmethoden für Modelle gelernt, wie Precision, Recall, F1-Score, Confusion matrix usw.
### Computer Vision
- Computer Vision beinhaltet grundlegender Bildkonzepte (Pixel, Farben) und Bildverarbeitungstechniken (Filtern, Kantenentdeckung, Bildverbesserung). Ich habe gelernt, Schlüsselmerkmale in Bildern zu erkennen und zu extrahieren sowie Merkmale abzugleichen. Außerdem habe ich auch gelernt, durch die Analyse von Bildern mehrerer Kameras die 3D-Struktur einer Szene zu verstehen und Bewegungsabschätzungen durchzuführen. Darüber hinaus habe ich gelernt, Machine Learning Algorithmen, insbesondere mit Convolutional Neural Networks, für Bilderkennung, Klassifizierung und Detektion anzuwenden. Schließlich habe ich mich mit fortgeschrittenen Techniken wie Szenenverständnis, semantischer Segmentierung und Gesichtserkennung auf Basis von Bildern vertraut gemacht.
### Robotik
- Designs von Robotern (mechanische Struktur und Antriebssystem), des Studiums der Kinematik und Dynamik sowie der Kontrollmethoden, Sensoren und Aktuatoren. Die mechanische Struktur besteht aus Gliedern (Teilen) und Gelenken (Gelenken), und das Verständnis der Bewegungs- und Kraftbeziehungen in Mehrfachgelenkstrukturen ist für das Antreiben von Robotern sehr wichtig. Ich habe auch die praktische Erfahrung mit der Programmierung von Robotern in Python, die bereits bei der Praxiserfahrungen erwähnt wurde.
### Mechatronik
- Mechatronik integriert vielfältiges Wissen von Mechanik, Machinenbau, Maschinenkonstruktion und Elektronik. Die habe ich schon seit Bachelorstudium studiert.
## Bachelor
### Mechanik
-  Mechanik (einschließlich Statik, Dynamik, Festigkeitslehre, Fluidmechanik), Materialwissenschaft (inklusive verschiedener Metalle und Verbundmaterialien, deren Härte, Festigkeit, Steifigkeit usw., sowie Wärmebehandlungsverfahren wie Abschrecken).
### Machinenbau
- Maschinenbau (mit verschiedenen Fertigungstechniken wie Gießen, Schweißen, mechanische Bearbeitung, Wärmebehandlung wie Abschrecken und 3D-Druck)
### Maschinenkonstruktion
- Maschinenkonstruktion (einschließlich der Gestaltung von Wellen, Zahnrädern, Lagern, Federn und der Fähigkeit, 2D- und 3D-Maschinenzeichnungen zu erstellen).
### Elektronik
- Im elektronischen Bereich umfasst das Studium elektronische Steuerungssysteme, Bauteile wie Trigger, Sensoren, Motoren und zudem die Signalverarbeitung als wichtigen Teil des elektronischen Systems.

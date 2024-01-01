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

## Robomaster Designer (Wettbewerb)

# Kurse

## Zertifikate
### Microsoft AI

## Machine Learning

## Computer Vision

## Robotik

## Mechatronik

## Mechanische Konstruktion

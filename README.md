# Car-Parking-Simulator-V2
Our groupproject about the second implementation of the game "Car-Parking Simulator".

# Lern-Bericht
Car-Parking Simulator V2 - Julian Hartmann (https://github.com/JHartmann-ims), Benjamin Peterhans

## Einleitung

Zu Beginn des Projektes haben Julian Hartmann und ich uns die Aufgabe gestellt, unser unvollständiges "Car-Parking Simulator" zu erweitern. Durch das Wissen aus dem letzten Projekt sollten wir besser und auch effizienter mit Unity Editor und Blender umgehen können. Da das Projekt von der Zeit her kleiner ist, sollten keine schwierigen oder zeitaufwändigen Funktionen in das Spiel eingebaut werden. In diesem Projekt soll es lediglich um das Verbessern und Hinzufügen der zuletzt nicht erledigten Funktionen gehen.

## Ziele

Meine Ziele:

Z1: Ich kann das Spiel funktionsfähig implementieren.

Z2: Ich kann mit Unity Editor umgehen.

Z3: Ich weiss, wie man Methoden aus anderen Skripts einbinden, bzw. verwenden kann.

## Beschreibung

In diesem Spiel geht es hauptsächlich darum, ein Auto auf einen Parkplatz zu parkieren. Mit anderen Autos, die auf dem Parkareal herumstehen, wird das Parkieren erschwert. Insgesamt gibt es in diesem Spiel momentan fünf individuelle Levels. Drei davon muss man vorwärts parkieren, die anderen zwei rückwärts.
Das Auto wird mit vier Pfeiltasten gesteuert, und zwar vorwärts, rückwärts, links und rechts. Die Bremse wird automatisch betätigt, sobald das Auto nicht mehr vor- oder rückwärts fährt.
Ausserdem wurde ein Punktesystem implementiert: Am Anfang des Spiels hat man fünf Sterne, die bei Kollisionen mit Hindernissen um je einen Stern abgezogen werden. Das Spiel ist beendet, wenn der Spieler sich in einem Parkplatz befindet oder eben alle Sterne verloren hat.

Natürlich gibt es für ein Handyspiel ein GUI, beziehungsweise ein Menü, in dem man herum navigieren kann. Im Spiel selbst kann man das Menü betätigen und einige Funktionen auswählen, wie zum Beispiel das Neustarten des Spiels, das Auswählen der Levels, das Beenden des Spiels etc.

## Demo

[![IMAGE ALT TEXT](http://img.youtube.com/vi/TUgpCnKCQtE/0.jpg)](http://www.youtube.com/watch?v=TUgpCnKCQtE "Car-Parking Simulator V2")

## Codeausschnitt

```cs
using carControl;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

namespace car
{
    public class Car : MonoBehaviour
    {
        private List<GameObject> starImagesGame = new List<GameObject>();
        private List<GameObject> starImages = new List<GameObject>();

        private int stars = 5;

        private CarControl car;

        private GameObject canvas;
        private GameObject canvasEnd;

        void Start()
        {
            car = GetComponent<CarControl>();

            canvasEnd = GameObject.Find("Menu2");
            canvas = GameObject.Find("Ingame");

            for(int i = 1; i <= 5; i++)
            {
                starImages.Add(GameObject.Find("Star" + i));
                starImagesGame.Add(GameObject.Find("GameStar" + i));
            }
            canvasEnd.SetActive(false);
        }

        void Update(){...}
        void OnCollisionEnter(){...}
        private IEnumerator waitThreeSeconds(){...}

        public void setEndMenu()
        {
            car.setHandleCarFalse();
            car.brakeCar();
            canvas.SetActive(false);
            StartCoroutine(waitThreeSeconds());
        }

        private void setStars(){...}
    }
}
```

# Download

Downloadlink: https://drive.google.com/drive/folders/13KrgwP2oIneNCi-nKU3Zcv6l52Nd1M2M?usp=sharing

## Verifikation

Z1: Das Ziel wird mit der Demonstration oben validiert.

Z2: Wird mit dem Skript unter "ILA_1306_Car-Parking\Assets\Scripts\Detector.cs" von Zeile 27 bis 48 validiert (Die Methoden wurden in den Skripts "Car.cs" und "CarControl.cs" verwendet).

Z3: Das Ziel wird mit dem Skript unter "ILA_1306_Car-Parking\Assets\Scripts\Car.cs" validiert (siehe Zeilen 1, 15, 22, 76 und 77).

# Reflektion zum Arbeitsprozess

##### IPERKA

I: Da wir schon beim letzten Projekt an diesem Spiel gearbeitet haben, mussten wir anfangs keine Informationen suchen gehen, oder allgemein uns über das Projekt informieren. Da das Spiel im Grunde genommen gleich ist, habe ich das Use-Case-Diagramm vom letzten Projekt übernommen. Ich konnte somit direkt mit den Testfällen beginnen, die auch wieder von den letzten abgeleitet wurden.

P: Das Planen hat dieses Mal Julian Hartmann übernommen.

E: Schon relativ am Anfang haben wir uns entschieden, die durchgefallenen Testfälle vom letzten Projekt zu implementieren, und allgemein das Spiel zu erweitern.

R: Während der Implementation gab es ein nennenswertes Problem. Hauptsächlich habe ich bei der Verbesserung der Detectors, beim Design in Unity und beim Creditmenü gearbeitet. Die meiste Zeit sass ich bei den Detectors, da dort viele Verbesserungen durchgeführt wurden. Das Creditmenü konnte in kurzer Zeit fertigstellen.

Beim Design in Unity musste ich einige Probleme mit den Colliders und den Rigidbodies beheben. Bei der Implementation der zwei zusätzlichen Levels, hatte ich die Idee, dass man bei diesen zwei rückwärts parkieren muss. Die Umsetzung war nicht wirklich kompliziert, da ich die Detectors (die im Spiel eingebaut sind) lediglich um 180 Grad rotieren muss. Ausserdem wurde die Präzision für das Parkieren durch die neue Anordnung der Detectors verbessert, sodass man nicht komplett schief parkieren kann. Ansonsten wurde das Menü noch überarbeitet und der Code vereinfacht, bzw. auch verbessert.

Zum Problem: Bei der Datei "Detector.cs" wollte ich das Skript "Car.cs" einbinden, sodass ich Methoden von "Car" benutzen kann. Das Einbinden war noch das Einfache, jedoch konnte ich irgendwie nicht auf das Skript zugreifen, da dieser einen Null-Wert hatte. Mit dem Debugging-Tool habe ich nach einer Lösung gesucht, jedoch vergeblich. Somit habe ich dann im Internet nachgeschaut und so die Lösung für das Problem gefunden (siehe unten "Link 1").
Da das Skript "Detector.cs" an das Objekt mit den Detectors gebunden war, und nicht an das Gesamtobjekt des Autos, konnte ich nicht auf "Car" zugreifen. Somit habe ich dann das Detector-Skript an das Auto gebunden, worauf dann das Problem gelöst wurde.

K: Das Testprotokoll wurde schlussendlich von Julian Hartmann durchgeführt. Alle Testfälle haben dieses Mal bestanden, was heisst, dass das Programm einwandfrei läuft. Das Programm ist spielbar und auch offen für Erweiterungen.

A: Wir konnten hierbei Vergleiche mit dem letzten Projekt herstellen. Wir kamen zum Schluss, dass dieses Projekt, auch wenn dies um einiges kleiner war, gut gelaufen ist. Das Hauptspiel wurde erreicht, weshalb wir nur noch einige Verbesserungen durchgeführt haben und auch neue Funktionen, die wir im letzten Projekt wegen der Zeit nicht implementieren konnten, hinzufügen konnten. Oben unter "Code" kann man die Verwendung des Skripts "Car.cs" sehen, die in "Detector.cs" angewendet wurde.

## Links

Link 1: https://stackoverflow.com/questions/49827358/getcomponent-function-returning-null

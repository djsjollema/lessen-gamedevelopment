# M4.6 My Clock


## Doelstelling
Leren werken met Euler-hoeken in graden
 
## De opdracht
Maak met behulp van deze assets

<img src="images/myClockAssets.png" alt="clock assets" width="50%"/>

Een werkende analoge klok

<img src="images/myClock.gif" alt="myClock" width="50%"/>

Je mag natuurlijk ook zelf andere assets zoeken, maken en/of ontwerpen voor jouw eigen ontwerp klok


## Hints voor bij de opdracht

### De datum en tijd weergeven

````Cs
        DateTime now = DateTime.Now;
        int hours = now.Hour;
        int minutes = now.Minute;
        int seconds = now.Second;
````

### Rotaties in Euler-hoeken (in graden)

In een 2D omgeving worden objecten geroteerd om de z-as. Rotaties worden in Unity weergegeven m.b.v. een Quaternion (een 4 dimensionale vector), maar kunnen met de methode "Euler" de rotatie in graden om respectievelijk de x-, y- en z-as worden opgegeven. 
```` cs
secondsHand.transform.rotation = Quaternion.Euler(new Vector3(x-as, y-as, z-as))
````

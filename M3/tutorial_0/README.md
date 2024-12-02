# Tutorial 0:

**Let op deze tutorial is enkel ter voorbereiding. Het telt niet mee voor de af te tekenen tutorials!**

**Ontwikkelomgeving opzetten en simpele jump mechanic**

## Leerdoelen:

- Jullie weten wat een IDE (integrated development environment) is en kunnen die opzetten voor Unity game projecten
- Jullie kunnen een unity project opzetten voor de arcade mechanics opdrachten
- Jullie kunnen simpele game objecten in de scene creeren
- Jullie kunnen de Rigidbody en Script components aan gameobjecten toevoegen
- Jullie weten waar je de Unity code reference kunt vinden en hoe je deze zelfsskunt gebruiken als script ondersteuning
- Jullie kunnen simpele scripts schrijven om gameobjecten te manipuleren

## Stappenplan:

Voer de onderstaande stappen uit en laat in de volgende les zien hoe ver je bent gekomen.

Als je klaar bent laat je het ook zien.

Als je vast zit vraag je om hulp!

### 0. Bekijk de eerste 31:35 minuten van deze video

[![basics](../tutorial_gfx/unity_basics.png)](https://youtu.be/pwZpJzpE2lQ?si=4GncqWjHaXYUy1kV)

### 1. installeer unity HUB

![hub](https://user-images.githubusercontent.com/1262745/216940260-3ecdf60a-4cc5-444c-a402-06dd3459728a.png)

### 2. Installeer de laatste LTS versie van Unity

![lts](https://user-images.githubusercontent.com/1262745/216939918-3874ba56-e1c3-49fb-8bac-005241182cae.png)

### 3. Creer een repo met readme en een unity .gitignore

![repo](https://user-images.githubusercontent.com/1262745/216939622-9a9d53aa-0eeb-4323-85d8-9bda551a301a.png)

### 4. Indien van toepassing : Installeer [MS Visual Studion Community 2022](https://visualstudio.microsoft.com/downloads/)

- Selecteer Game Development with Unity
  ![VSunity](https://user-images.githubusercontent.com/1262745/216986819-4bc6afe0-9967-4879-80f7-504565016f69.png)

- Installeer de **_Markdown Editor (64-bit)_** Extension
  ![markdown](https://user-images.githubusercontent.com/1262745/216987147-a79b5572-6b4d-472e-9f77-259bb7d7b8c4.png)

### 5. Clone de repo vanuit MS Visual Studio

![clone](https://user-images.githubusercontent.com/1262745/216944643-6c447b9f-e305-4dda-a3aa-47179c79d11b.png)

### 6. Maak een 3d Unity project aan

![unityhub](https://user-images.githubusercontent.com/1262745/216937816-a3c0c4ba-9095-4c60-8431-bdf3dff80077.png)

![create game](https://user-images.githubusercontent.com/1262745/216938273-17306e93-32ad-468a-bedf-5efb62c4591e.png)

![patience](https://user-images.githubusercontent.com/1262745/216938677-8133a273-0f83-475e-89bb-1fb380543a95.png)

![unity](https://user-images.githubusercontent.com/1262745/216944716-bf1b346e-4f36-4217-8082-4fb551120f8c.png)

### 7. Verplaats de .gitignore file naar root van je unity project

![root](https://user-images.githubusercontent.com/1262745/216955006-0ab2f920-f0fe-4754-afb4-96b3933d2016.png)

### 8. Maak een **"Scripts"** folder

![script folder](https://user-images.githubusercontent.com/1262745/216945944-54b722e5-ff2a-4234-bb5c-6bdef8abd164.png)

![folders](https://user-images.githubusercontent.com/1262745/216945988-cc0df84c-1d81-4179-b6c3-c882d5b81026.png)

### 9. Maak een eerste script: **HelloUnity.cs**

![hellounity](https://user-images.githubusercontent.com/1262745/216946539-011f9dbc-591c-4de8-b5f6-9074445a63b2.png)

![script](https://user-images.githubusercontent.com/1262745/216946844-b529242a-3546-4190-8e63-3b9fc1886567.png)

![script2](https://user-images.githubusercontent.com/1262745/216947101-31e0775e-e199-44cf-90ef-c5cfe5c260da.png)

### 10. Schrijf code:

```
  void Start(){
    Debug.Log("Hello Unity");
  }
```

### 11. Voeg het script als **_component_** toe aan het **_Main Camera_** object

![component](https://user-images.githubusercontent.com/1262745/216948658-32ab1cfa-e0fd-4cdf-b5ff-bafa1a8deaa9.png)

### 12. Run the game! en check de console.. Zie je een bericht?

![run](https://user-images.githubusercontent.com/1262745/216949259-30d317b7-4d68-410e-ac80-5f6f3b4b8015.png)

### 13. Neem de uitleg over de layout van unity door (Klik op de onderstaande image):

[![image](https://docs.unity3d.com/uploads/Main/using-editor-window.png)](https://docs.unity3d.com/Manual/UsingTheEditor.html)

### 14. Plaats een **_Plane_** en een **_Cube_** in de **_scene_**

![3d](https://user-images.githubusercontent.com/1262745/216987879-0503f333-0bb5-4d58-8db9-d2d1be3c6506.png)

### 15. Voeg een **_Rigidbody_** component toe aan de **_cube_** via de optie **_add component_**

![addObjectsRigid](https://user-images.githubusercontent.com/1262745/216987955-ef5b1fa3-ec39-450a-bbdc-8cfa085fd289.png)

### 16. Maak een nieuw **_LaunchCube.cs_** script aan en hang dat aan de **_Cube_** als component.

![launch cube](https://user-images.githubusercontent.com/1262745/216988688-58fa601b-c638-4c33-92cc-9e7ef36e3404.png)

### 17. Ga naar de [**_Rigidbody_**](https://docs.unity3d.com/ScriptReference/Rigidbody.html) pagina van de Unity scripting manual.

- Gebruik de methode **AddForce()** om de **cube** te lanceren
- Doe dit op het moment dat je de [spatie ingedrukt hebt](https://docs.unity3d.com/ScriptReference/Input.GetKeyDown.html)

### Commit naar je eigen branch en push je werk. Laat je Unity scene, je code en je repository zien aan de docent!

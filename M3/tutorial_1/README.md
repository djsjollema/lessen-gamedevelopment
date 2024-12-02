# Tutorial 1

**Mixamo.com placeholder animaties aansturen**

## Leerdoelen:

- Jullie kunnen snel placeholder animaties implementeren
- Jullie weten hoe je animaties op een goede manier kunt importeren
- Jullie kunnen animaties en transitions maken met behulp van de Animator tool
- Jullie kunnen via scripts de juiste animaties triggeren

## Stappenplan:

Voer de onderstaande stappen uit en laat in de volgende les zien hoe ver je bent gekomen.

Als je klaar bent laat je het ook zien.

Als je vast zit vraag je om hulp!

### 1. Ga naar Mixamo.com en maak een gratis account aan

![Mixamo](../tutorial_gfx/mixamo.png)

- **_Optioneel_** [kun je deze tutorial volgen](https://youtu.be/8Pk7FI629O8)

### 2. Selecteer een character

![Character](../tutorial_gfx/character.png)

### 3. Selecteer een animatie

### 4. Download primaire animatie (idle) met skin

### 5. Selecteer meer animaties en download deze zonder skin

### 6. zorg voor de juiste import settings in Unity

- Model settings:
  ![Model Settings](../tutorial_gfx/model_settings.png)
- Rig settings:
  ![Rig Settings](../tutorial_gfx/rig_settings.png)
- Animation settings
  ![Animation Settings](../tutorial_gfx/animation_settings.png)
- Materials settings
  ![Materials Settings](../tutorial_gfx/materials_settings.png)
- Click op Extract Textures en Materials en sla deze op in je project
  ![Extract](../tutorial_gfx/extract.png)

### 7. Sleep je fbx in de scene

![To Scene](../tutorial_gfx/toScene.png)

### 8. Voeg de animator controller toe

- Maak een Animator Controller aan
  ![Add Animator Controller](../tutorial_gfx/addAnimatorController.png)
- Selecteer je character in de hierarchy
  ![Char Hierarchie](../tutorial_gfx/charHierarchie.png)
- Selecteer de nieuwe Animator Controller
  ![Select Animator Controller](../tutorial_gfx/selectAnimatorController.png)

### 9. Plaats je animaties in de Animator

- Open het Animator Window
  ![Open Animator](../tutorial_gfx/openAnimator.png)
- Sleep je animaties in het animator window
  ![Sleep](../tutorial_gfx/sleep.png)
- Voeg een trigger toe
  ![Trigger](../tutorial_gfx/trigger.png)
- voeg transitions toe
  ![Transition](../tutorial_gfx/transition.png)
- zet als condition de trigger
  ![Condition](../tutorial_gfx/condition.png)

### 10. Maak code om de animatie aan te roepen

- Hang een nieuw script als component aan je character
- Gebruik de methode [Animator.SetTrigger("value")](https://docs.unity3d.com/ScriptReference/Animator.SetTrigger.html)

### 11. Zorg dat er standaard een idle animatie afspeelt en dat je character iets anders doet als je op een knop drukt.

![Animation](../tutorial_gfx/Animation.gif)

### Commit en push je werk naar je eigen branch. Laat je Unity scene, je code en je repository zien aan de docent!

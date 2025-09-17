# Instructieles: Werken met GitHub en een repository klonen naar de lokale computer

## Doel van de les

Na deze les kun je: - Uitleggen wat Git en GitHub zijn.\
- Met de **command prompt** werken om een repository te klonen.\
- Een repository lokaal opslaan in een specifieke directory.

------------------------------------------------------------------------

## 1. Wat is Git en GitHub?

-   **Git** is een versiebeheersysteem: het houdt bij welke wijzigingen
    in je code/project gemaakt worden en door wie.\
-   **GitHub** is een online platform waar je Git-repositories kunt
    opslaan en delen met anderen.\
-   Een **repository (repo)** is een projectmap met bestanden en de
    volledige versiegeschiedenis.

------------------------------------------------------------------------

## 2. Voorbereiding

1.  Zorg dat **Git** geïnstalleerd is op je computer.
    -   Controleer dit met:

        ``` bash
        git --version
        ```

        Als er een versienummer verschijnt, is Git correct
        geïnstalleerd.
2.  Maak de mapstructuur waar je de repository wilt opslaan:
    -   We gaan werken in:

            C:/documents/ma/m1/skill-github/les3

------------------------------------------------------------------------

## 3. Een repository klonen

**Klonen** betekent dat je een kopie maakt van een repository van GitHub
naar je eigen computer.

### Stappenplan:

1.  Open de **Command Prompt** (Windows: zoek naar *cmd* in het
    startmenu).

2.  Navigeer naar de gewenste directory met het commando `cd`:

    ``` bash
    cd C:/documents/ma/m1/skill-github/les3
    ```

3.  Ga naar GitHub en kopieer de **clone-URL** van de repository:

    -   Klik op de groene knop **\<\> Code** in de repository.\
    -   Kies **HTTPS** en kopieer de link (bijvoorbeeld
        `https://github.com/gebruikersnaam/projectnaam.git`).

4.  Voer het clone-commando uit:

    ``` bash
    git clone https://github.com/gebruikersnaam/projectnaam.git
    ```

5.  Na enkele seconden staat er een map in `les3` met de naam van de
    repository.

------------------------------------------------------------------------

## 4. Controleren of het gelukt is

-   Typ in de command prompt:

    ``` bash
    dir
    ```

    → Je ziet nu een map met de naam van de repository.

-   Ga naar die map:

    ``` bash
    cd projectnaam
    ```

-   Controleer de inhoud:

    ``` bash
    dir
    ```

------------------------------------------------------------------------

## 5. Samenvatting

-   Met `cd` navigeer je naar de juiste map.\
-   Met `git clone [URL]` haal je een repository binnen.\
-   De repository wordt lokaal opgeslagen, inclusief alle bestanden en
    de volledige geschiedenis.

------------------------------------------------------------------------

👉 Tip voor leerlingen: oefen dit proces meerdere keren met
verschillende repositories om het goed onder de knie te krijgen.

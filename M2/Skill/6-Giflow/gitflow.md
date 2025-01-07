# Oefening: Samenwerken met Branches en Pull-Requests

## Doel
In deze oefening leer je:
1. Samenwerken aan een project in een GitHub repository.
2. Werken met branches om nieuwe functionaliteit te implementeren.
3. Een pull-request aan te maken en te reviewen.
4. Conflicten oplossen bij het samenvoegen van code.

---

## Voorbereiding
1. Zorg dat je een werkende Git-omgeving hebt.
2. Clone de volgende repository naar je lokale machine:
   ```bash
   git clone https://github.com/jouwgebruikersnaam/team-project.git
   ```
3. Open het project in je favoriete code-editor.

---

## Stap 1: Nieuwe Functionaliteit Toevoegen

1. **Maak een nieuwe branch:**
   Ga naar de terminal en maak een nieuwe branch voor jouw functionaliteit. Gebruik een beschrijvende naam, bijvoorbeeld `feature/profielpagina`.
   ```bash
   git checkout -b feature/profielpagina
   ```

2. **Implementeer de functionaliteit:**
   Voeg een nieuwe functie toe aan het project. Bijvoorbeeld:
   - Creëer een nieuwe HTML-pagina genaamd `profile.html`.
   - Voeg een eenvoudige koptekst toe, zoals:
     ```html
     <h1>Welkom op de profielpagina!</h1>
     ```

3. **Commit je wijzigingen:**
   Voeg je wijzigingen toe aan Git en commit ze:
   ```bash
   git add .
   git commit -m "Toegevoegd: profielpagina"
   ```

4. **Push naar GitHub:**
   Push je branch naar de remote repository:
   ```bash
   git push origin feature/profielpagina
   ```

---

## Stap 2: Pull-Request Aanmaken

1. Ga naar de GitHub-pagina van het project.
2. Klik op **Pull Requests** en klik vervolgens op **New Pull Request**.
3. Selecteer jouw branch (`feature/profielpagina`) als bron en `main` als doel.
4. Voeg een beschrijving toe en stuur de pull-request in.

---

## Stap 3: Review en Samenvoegen

1. **Review:**
   - Laat een andere student jouw pull-request reviewen.
   - Controleer of de code voldoet aan de richtlijnen.
   - Voeg een opmerking toe of keur de pull-request goed.

2. **Conflicten oplossen:**
   - Als er merge-conflicten zijn, los deze op in je lokale repository.
   - Gebruik hiervoor de volgende stappen:
     ```bash
     git checkout main
     git pull origin main
     git checkout feature/profielpagina
     git merge main
     ```
     Los conflicten op in je code-editor, commit de wijzigingen en push naar GitHub.

3. **Samenvoegen:**
   - Na goedkeuring kan de pull-request worden gemerged.
   - Klik op **Merge Pull Request** en verwijder de branch als deze niet meer nodig is.

---

## Bonus: Extra Functionaliteit
- Voeg CSS toe aan je profielpagina om het er mooier uit te laten zien.
- Werk samen met een andere student aan een gezamenlijke feature.

Veel succes!


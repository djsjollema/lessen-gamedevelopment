Lesplan: Werken met Branches in Git (Vervolg)
Doelgroep: Deelnemers met basiskennis van Git (zoals git init, git add, git commit), maar zonder uitgebreide ervaring met branches.

Lesdoelen:

Deelnemers begrijpen het nut en gebruik van branches.
Deelnemers kunnen branches aanmaken, erop werken en samenvoegen.
Deelnemers leren hoe conflicten bij het mergen op te lossen.
Duur: 70 minuten

1. Introductie tot Branches (5 minuten)
Doel: Het concept van branches kort herhalen en hun praktische gebruik uitleggen.

Onderwerpen:

- Wat is een branch?
- Parallelle werklijn binnen een project.
- Waarom branches gebruiken?
- Scheiden van ontwikkeling (features, bugfixes) zonder de hoofdcode te verstoren.
- Ondersteunt samenwerking in teams.

Belangrijkste gebruiksscenario's:
- Feature development: werken aan nieuwe functionaliteiten.
- Bugfixing: snel problemen oplossen in een aparte branch.
- Experimenteren: nieuwe ideeën testen zonder de stabiele code te beïnvloeden.
 
1. Branches Aanmaken en Wisselen (15 minuten)
   1. Doel: Deelnemers oefenen met het aanmaken en wisselen tussen branches.

Stap 1: Aanmaken van een nieuwe branch

Vraag deelnemers om een nieuwe branch aan te maken voor een nieuwe feature:

```bash
git branch feature-xyz
```
Wissel naar de nieuwe branch:

```bash
git checkout feature-xyz
```
Alternatief: gebruik -b om beide stappen in één keer te doen:

```bash
git checkout -b feature-xyz
```
Stap 2: Werken op de nieuwe branch

Laat de deelnemers een wijziging aanbrengen in hun project, bijvoorbeeld een nieuw bestand aanmaken of bestaande code bewerken.

Voeg de wijzigingen toe en commit ze:

```bash
git add .
git commit -m "Feature XYZ toegevoegd"
```

1. Branches Samenvoegen (Mergen) (20 minuten)
Doel: Deelnemers leren hoe ze veranderingen van een feature branch kunnen samenvoegen met de main branch.

Stap 1: Terug naar de main branch

Laat de deelnemers teruggaan naar de main branch:

```bash
git checkout main
```

Stap 2: Samenvoegen van de feature branch

Merg de feature branch met de main branch:

```bash
git merge feature-xyz
```

Als er geen conflicten zijn, wordt de merge automatisch afgerond.

Stap 3: Verwijderen van de branch

Verwijder de branch na het mergen:

```bash
git branch -d feature-xyz
```

4. Conflicten Oplossen (20 minuten)
Doel: Deelnemers leren omgaan met mergeconflicten en hoe deze op te lossen.

Stap 1: Conflict simuleren

Vraag de deelnemers om op dezelfde plaats in een bestand te werken op zowel de main branch als de feature-xyz branch.

Laat de wijzigingen in beide branches committen en probeer vervolgens de branches samen te voegen. Git detecteert het conflict:

```bash
git merge feature-xyz
```

Stap 2: Conflicten bekijken

Laat deelnemers conflicten openen in een teksteditor. Git markeert de conflicterende regels in het bestand met <<<<<<<, =======, en >>>>>>>.

Stap 3: Conflict oplossen

Laat de deelnemers handmatig de conflicterende code bewerken en het probleem oplossen.

Na het oplossen moeten ze het bestand opnieuw toevoegen:
```bash

git add <conflicterend-bestand>
```
Commit vervolgens de opgeloste versie:

```bash
git commit
```

Stap 4: Controleer de merge

Zorg ervoor dat de merge is voltooid en controleer de repository-status om er zeker van te zijn dat alles is bijgewerkt.
1. Branch Workflows (10 minuten)
Doel: Inzicht geven in veelgebruikte branch-strategieën voor teams.

Onderwerpen:

Feature branching: Elke nieuwe feature krijgt zijn eigen branch.
Git Flow: Gestructureerde aanpak met branches zoals develop, release, en hotfix.
Trunk-based development: Korte branches die snel samengevoegd worden met main.
Laat de deelnemers nadenken over hoe ze deze workflows kunnen toepassen in hun eigen projecten.

6. Afsluiting en Vragen (5 minuten)
Doel: Samenvatten van het geleerde en ruimte geven voor vragen.

Wat hebben we behandeld:
Aanmaken en wisselen van branches.
Mergen van branches en het oplossen van conflicten.
Branchstrategieën voor teams.
Vraag of er nog onduidelijkheden of vragen zijn.
Bonus: Optionele Oefeningen
Laat deelnemers experimenteren met het gebruik van git stash om onvoltooide veranderingen op te slaan.
Oefen met rebase om de geschiedenis van branches te herschrijven en te versimpelen.
Materiaal en Vereisten:

Laptop met Git geïnstalleerd.
Toegang tot een teksteditor (bijv. VSCode, Sublime Text).
Een basis Git repository om mee te werken.
Dit lesplan is ontworpen om deelnemers hands-on ervaring te geven met branches in Git, met de nadruk op samenwerking en het oplossen van problemen zoals merge-conflicten.
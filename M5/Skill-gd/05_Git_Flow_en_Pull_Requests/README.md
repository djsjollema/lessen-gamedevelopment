# Versie beheer strategieen

Een Versiebeheerstrategie is een aanpak om wijzigingen in je code, of andere bestanden binnen je project, systematisch bij te houden en te beheren met behulp van een versiebeheer systeem (bijvoorbeeld Git).

Door een vooraf-gedefinieerde strategie te gebruiken is het voor iedereen duidelijk wat de regels zijn en hoe deze strategie toegepast moet worden.

**Wat was tot nu toe je strategie voor het samen voeren van versiebeheer?**

**Wat waren hiervan de voor en nadelen?**

Veelgebruikte versiebeheer strategieën in software development zijn:

- Git Flow
- Github Flow
- Trunk based development

## Git Flow:

![gitflow](../src/05_branching_strategie_git_flow.png)

- Twee primaire branches: main (productie) en develop (laatste ontwikkelingen)
- Feature branches worden gemaakt voor nieuwe functionaliteiten
- Release branches voorbereiden en testen van nieuwe versies
- Hotfix branches voor kritische productie-updates
- Meer geschikt voor grote, complexe software met gereguleerde releases
- Meer complex en overhead voor kleinere teams

## GitHub Flow:

![github flow](../src/05_02_branching_strategie_github_flow.png)

- Eenvoudige, op continue levering gerichte strategie
- Centrale main branch is altijd deployable
- Korte en lichte feature branches
- Pull requests voor code review en samenwerking
- Direct mergen naar main na goedkeuring
- Minimale branching-overhead
- Geschikt voor teams die snel moeten leveren

## Trunk Based Development:

![trunk based](../src/05_03_branching_strategie_trunk_based.png)

- Alle ontwikkelaars committen direct naar centrale main branch
- Minimaal gebruik van branches
- Sterke nadruk op continue integratie en levering
- Vereist sterke test automatisering
- Geschikt voor teams met veel vertrouwen en discipline
- Hoge code kwaliteit is vereist
- Minder controle op elkaars werk

**Welke van de bovenstaande strategieen is volgens jou het meest bruikbaar voor je Vertical Slice project en waarom?**

## Stappen binnen de GitHub Flow strategie:

1. Voordat je een een nieuwe featuren gaat bouwen maak je hiervoor een nieuwe feature branch aan.

- Het vertrekpunt hiervoor is de "main" branch.
- Geef een goed omschrijvende naam. (bijv. feature/enemyBehavior)

2. Gefocuste ontwikkeling.

- Maak kleine, "gefocuste" commits die zich op specifieke kleine onderdelen richt en niet op complete features of systemen.
- Maak Gedetailleerde commit-berichten waarin duidelijk wordt wat je hebt gedaan en wat er is veranderd.
- Regelmatig pushen naar de remote repository zodat de voortgang voor iedereen up to date blijft.

3. Mergen van branches altijd via Pull Requests.

- Merge terug van de feature branch naar de "main" branch.
- Geef in een Pull Request een gedetailleerde beschrijving van alle wijzigingen.
- De teamleden of de lead devloper worden via een Pull Request gevraagd om een code review.
- Zonder code review kan en mag er niet gemerged worden.

4. Code Reviews uitvoeren

- Teamleden of lead developers controleren alle code in de pull request.
- Suggesties en feedback wordt terug gegeven en besproken.
- Eventuele aanpassingen worden doorgevoerd.

5. Merge naar main branch

- Na goedkeuring samenvoegen
- De verandering wodt direct geintegreerd in de productie-omgeving (Verwerken in final scene)

**Heb je een beeld van alle bovenstaande stappen? Wat moet je met je team doen om deze uit te voeren? Welke tools en skills hebben jullie hiervoor nodig?**

## Branches maken en mergen

**Wie weet hoe je een branch maakt? en deze ook weer merged?**

![merge branches](../src/05_09_merge_branches.png)

Oefen dit eventueel eerst door een oefen repository te maken. Daar wat testbranches te maken. Op verschillende branches te comitten en deze ook weer te mergen naar de main.

Commands:

`git branch` : check welke branches er zijn en waar je bent.
`git branch [new name]` : maak een nieuwe branch aan.
`git switch [branch name]` : ga naar deze branch.
`git merge [branch to merge]` : pak de commits van de "branch to merge" en merge die in de branch waar je bent.
`git branch -d [branch to delete]` : verwijder de branch nadat deze gemerged is.
`git branch -D [branch to delete]` : verwijder de branch ook al is die niet gemerged.

## Samen werken in 1 repo "Collaborators"

Om samen te kunnen werken in 1 repo moet de eigenaar anderen toelaten als "collaborators":

![samenwerken](../src/05_07_collaborators.png)

## Pull Requests

**Wie weet wat een pull request is?**

[![image](../src/05_04_pull_request_video.png)](https://youtu.be/FDXSgyDGmho?si=CLn64wiBumTkF0fm)

## Afdingen van pull requests

Je kunt je collaborators dwingen om pull requests te maken voordat nieuwe branches gemerged kunnen worden:

![force pull request](../src/05_08_force_pull_request.png)

Naast het samenvoegen van veranderingen is een pull request ook vooral bedoeld om te controleren of de code wel goed is. We zorgen er dus voor dat er bij elke pull request een code review word uitgevoerd.

Dit kan gedaan worden door een teamgenoot of je kunt er ook voor kiezen om de beste developer, "lead" developer te maken die de taak heeft om alle pull requests te reviewen.

![lead developer](../src/05_08_lead_dev.gif)

## Opdracht 6: De test repo

Maak evt. een test repo aan met je teamgenoten.
Maak een paar nieuwe test branches aan, bijvoorbeeld:
/testAddNewFiles
/testAddImages
/testRemoveFiles

Verander de inhoud van het project in deze branches door er bestanden aan toe te voegen, aan te passen en te verwijdederen.
Maak een pull request aan via github of github desktop
![desktop vs github.com](../src/05_06_pull_requests_desktop_vs_github.png)

Zorg dat je in deze pull request goed omschrijft wat er in die brnch gebeurd is.

Laat iemand anders uit je team controleren of de veranderingen kloppen en de pull request goedkeuren en mergen.

Maak nu zelf eens expres een merge conflict aan. Doe dit door op zowel de main branch als op de testbranch (die je wil mergen) in de zelfde file dezelfde regel aan te passen.

Resolve nu ook het merge conflict op github of in je code editor.

Lever de link naar je test repo in op Simulise.

# Versie beheer strategieen

Een Versiebeheerstrategie is een aanpak om wijzigingen in je code, of andere bestanden binnen je project, systematisch bij te houden en te beheren met behulp van een versiebeheer systeem (bijvoorbeeld Git).

Door een voorafgedefinieerde strategie te gebruiken is het voor iedereen duidelijk wat de regels zijn en hoe deze strategie toegepast moet worden.

**Welke strategie hebben jullie tot nu toe gehanteerd voor jullie versiebeheer?**

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
- Geschikt voor teams met continue integratie en delivery

## Trunk Based Development:

![trunk based](../src/05_03_branching_strategie_trunk_based.png)

- Alle ontwikkelaars committen direct naar centrale main branch
- Minimaal gebruik van branches
- Sterke nadruk op continue integratie
- Vereist sterke test automatisering
- Geschikt voor teams met hoge vertrouwen en discipline
- Hoge code kwaliteit

**Welke van de bovenstaande strategieen is volgens jou het meest bruikbaar voor je Vertical Slice project?**

## Workflow stappen:

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
- Direct deployen naar de productie-omgeving

**Heb je een beeld van alle bovenstaande stappen? Wat moet je met je team doen om deze uit te voeren? Welke tools en skills hebben jullie hiervoor nodig?**

## Branches maken

**wie weet hoe je een branch maakt?**

## Pull Requests

**Wie weet wat een pull request is?**

> > uitleg pull request video<<

- Maak eens een pull request

## Opdracht 6:

Maak een test

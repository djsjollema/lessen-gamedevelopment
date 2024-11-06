Opdrachtomschrijving:
Je gaat een mini-project opzetten waarin je meerdere features ontwikkelt. Dit zal je doen door gebruik te maken van branches, waarbij je elke feature in een aparte branch ontwikkelt en deze later samenvoegt met de main branch. Tijdens het samenvoegen kunnen er conflicten ontstaan, die je zult moeten oplossen.

Stappenplan:
1. Start een nieuw Git-project (5 minuten)
Maak een nieuwe directory aan voor je project:

```bash

mkdir git-branches-opdracht
cd git-branches-opdracht
```
Initieer een nieuwe Git-repository:

```bash
git init
```

Maak een nieuw bestand aan, genaamd README.md, waarin je kort beschrijft wat dit project inhoudt. Voeg het toe aan Git en commit je eerste versie:

```bash
echo "# Git Branches Opdracht" > README.md
git add README.md
git commit -m "Eerste commit: README toegevoegd"
```

2. Feature 1: Nieuwe Functionaliteit Toevoegen (10 minuten)
Maak een nieuwe branch voor de eerste feature:

```bash
git checkout -b feature-1
```

Maak een nieuw bestand aan, genaamd feature1.txt, waarin je kort beschrijft wat de eerste feature doet (bijvoorbeeld: "Deze feature voegt functionaliteit X toe"). Voeg het bestand toe aan Git en commit je wijziging:

```bash
echo "Feature 1: Functionaliteit X toegevoegd" > feature1.txt
git add feature1.txt
git commit -m "Feature 1: functionaliteit X toegevoegd"
```

Wissel terug naar de main branch en merge de feature-1 branch:

```bash
git checkout main
git merge feature-1
```
Verwijder de branch feature-1:

```bash
git branch -d feature-1
```
3. Feature 2: Tweede Functionaliteit Toevoegen (10 minuten)
Maak een nieuwe branch voor de tweede feature:

```bash
git checkout -b feature-2
```
Maak een nieuw bestand aan, genaamd feature2.txt, en beschrijf de tweede functionaliteit in dit bestand (bijvoorbeeld: "Feature 2 voegt functionaliteit Y toe"). Commit de wijziging:

```bash
echo "Feature 2: Functionaliteit Y toegevoegd" > feature2.txt
git add feature2.txt
git commit -m "Feature 2: functionaliteit Y toegevoegd"
```
Wissel terug naar de main branch en merge de feature-2 branch:

```bash
git checkout main
git merge feature-2
```

Verwijder de branch feature-2:

```bash
git branch -d feature-2
4. Feature 3: Bewerk een Bestaand Bestand en Creëer een Conflict (10 minuten)
```

Maak een nieuwe branch aan voor de derde feature:

```bash
git checkout -b feature-3
Bewerk het bestand README.md door een nieuwe regel toe te voegen met de tekst: "Feature 3 voegt een verbeterde functionaliteit toe." 
```

Commit de wijziging:

```bash
echo "Feature 3: Verbeterde functionaliteit toegevoegd" >> README.md
git add README.md
git commit -m "Feature 3: verbeterde functionaliteit toegevoegd"
```

Belangrijk: Wissel terug naar de main branch en bewerk hetzelfde bestand (README.md) door een andere regel toe te voegen, bijvoorbeeld: "Deze regel is toegevoegd in de main branch." Commit deze wijziging:

```bash
echo "Deze regel is toegevoegd in de main branch" >> README.md
git add README.md
git commit -m "Nieuwe regel toegevoegd in main branch"
```
Probeer nu de feature-3 branch samen te voegen met de main branch:

```bash
git merge feature-3
```
Er zal een mergeconflict optreden omdat je hetzelfde bestand hebt bewerkt in zowel de main branch als de feature-3 branch.

5. Oplossen van het Mergeconflict (10 minuten)
Open het bestand README.md in een teksteditor. Je zult zien dat Git het conflict markeert met de symbolen <<<<<<<, =======, en >>>>>>>. Los het conflict op door de gewenste delen van beide wijzigingen te behouden.

Na het oplossen van het conflict, voeg het bestand opnieuw toe aan de staging area:

```bash
git add README.md
```

Commit de oplossing van het conflict:

```bash
git commit -m "Conflicten opgelost: README.md"
```

Verwijder de branch feature-3:

```bash
git branch -d feature-3
```
6. Optionele Uitbreiding: Rebase in Plaats van Merge (10 minuten)
Maak nog een nieuwe branch aan, bijvoorbeeld feature-4:

```bash
git checkout -b feature-4
```

Voeg een nieuw bestand toe en commit het (bijvoorbeeld feature4.txt):

```bash
echo "Feature 4: Functionaliteit Z toegevoegd" > feature4.txt
git add feature4.txt
git commit -m "Feature 4:
Functionaliteit Z toegevoegd"
```

Wissel terug naar de main branch en voeg een extra commit toe, bijvoorbeeld door het wijzigen van een ander bestand.

In plaats van te mergen, gebruik je nu rebase om de commits van feature-4 bovenop de commits van main te plaatsen:

```bash
git checkout feature-4
git rebase main
```

Bekijk hoe de geschiedenis herschikt wordt zonder een merge commit, en voeg de branch samen na het rebase:

```bash
git checkout main
git merge feature-4
```

Inleveren:
Zorg dat je de volledige opdracht hebt uitgevoerd. Maak een overzicht van je Git-commando's, samen met een korte beschrijving van de conflicten die je hebt opgelost en hoe je dat hebt gedaan.
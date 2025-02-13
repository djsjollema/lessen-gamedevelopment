## **Instructie: Start een nieuw 2D-project in Unity**  
### **Projectnaam:** M3-skill  
### **Doel:** Een Unity 2D-project opzetten met een repository voor versiebeheer en controle door de docent.  

---

### **Stap 1: Unity 2D-project aanmaken**  
1. Open **Unity Hub** en klik op **"Nieuw project"**.  
2. Kies als template **2D (Core)**.  
3. Geef het project de naam: **M3-skill**.  
4. Kies een locatie **buiten OneDrive** (bijvoorbeeld: `C:\UnityProjects\M3-skill\`).  
5. Klik op **"Maak aan"** om het project te genereren.  

---

### **Stap 2: Git Repository opzetten en delen**  
1. **Git installeren** (indien nog niet gedaan):  
   - Download en installeer Git vanaf: [https://git-scm.com/](https://git-scm.com/).  
2. **GitHub-account aanmaken** (indien nog niet gedaan).  
3. **Repository aanmaken in GitHub:**  
   - Ga naar [https://github.com/](https://github.com/) en log in.  
   - Klik op **"New repository"**.  
   - Geef de repository de naam: **M3-skill**.  
   - Zet deze **op privé** en voeg een `.gitignore` toe voor Unity.  
   - Klik op **"Create repository"**.  
4. **Repository koppelen via de Command Prompt:**  
   - Open de **Command Prompt** (**cmd**) in Windows.  
   - Navigeer naar de projectmap door het volgende commando uit te voeren:  
     ```cmd
     cd C:\UnityProjects\M3-skill
     ```
   - Voer vervolgens de volgende commando’s uit om het project te koppelen aan de repository:  
     ```cmd
     git init
     git remote add origin https://github.com/jouw-gebruikersnaam/M3-skill.git
     git pull origin main
     git add .
     git commit -m "Eerste commit - project setup"
     git push -u origin main
     ```
5. **Docent toevoegen als collaborator:**  
   - Ga in GitHub naar de repository-instellingen.  
   - Klik op **"Manage access"** > **"Invite a collaborator"**.  
   - Voeg **djsjollema** toe

---

### **Stap 3: Projectstructuur inrichten**  
1. Open Unity en ga naar de **Project**-view.  
2. Maak de volgende mappen aan in de **Assets**-map:  
   - **Scenes** (voor alle opdrachten)  
   - **Sprites** (voor afbeeldingen)  
   - **Scripts** (voor C#-scripts)  
   - **Audio** (voor geluidseffecten/muziek)  
   - **Prefabs** (voor herbruikbare objecten)  

---

### **Stap 4: Scenes voor opdrachten maken**
Alle opdrachten moeten worden uitgevoerd in een aparte scene met als naam van de scene de naam van de opdracht. De eerste opdracht heet Bit.
1. Ga naar de map **Scenes**.  
2. Maak de eerste Scene aan per 
   - **Bit.unity**  

---

### **Stap 5: Eerste push naar GitHub via de Command Prompt**  
1. Open **Command Prompt** (**cmd**) en voer uit:  
   ```cmd
   cd C:\UnityProjects\M3-skill
   git add .
   git commit -m "Projectstructuur aangemaakt"
   git push
   ```
2. Controleer in GitHub of de bestanden correct zijn geüpload.  

---

### **Stap 6: Unity instellen voor versiebeheer**  
1. Ga in Unity naar **Edit** > **Project Settings**.  
2. Ga naar **Editor** en stel **Version Control Mode** in op **Visible Meta Files**.  
3. Ga naar **Asset Serialization** en zet dit op **Force Text**.  
4. Sla de instellingen op.  

---

### **Stap 7: Controle door de docent**  
- Zorg ervoor dat de docent toegang heeft tot de repository.  
- Push regelmatig updates via Git.  
- De docent kan de commits controleren en feedback geven.  

---

✅ **Je Unity 2D-project is nu correct opgezet met versiebeheer!**
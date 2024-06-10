# Azure demo



## 🧬 1 - Klon eksempelkoden
Du finner eksempelkoden [her](https://GitHub.com/emilstromsvag/azure-demo). 
Trykk "Use this template" og klon det til din egen profil.

## 🔑 2 Opprett subscription i Azure
1. Gå til [Subscription](https://portal.azure.com/#view/Microsoft_Azure_Billing/SubscriptionsBladeV2) på azure portalen
2. Trykk på ADD
3. Velg free trial

## ☁️ 3 - Lag en resurs i Azure
1. Gå til [Azureportalen](https://portal.azure.com/#home)
2. Trykk på [Quickstart Center](https://portal.azure.com/#blade/Microsoft_Azure_Resources/QuickstartCenterBlade) (romskipet)
3. Gå på "Projects and guides", deretter "Create a web app".
4.  Velg "Build and host a web app with Azure Web Apps"
   
### 3.1 - Sette opp web appen

   * Velg resursgruppen X
   * Gi den et navn, f.eks. brukernavnet ditt 
   * Programmeringsspråk Python 3.12
   * Region "Norway East"
   * Plan X

Velg "Review + create", deretter "Create" og vent et par strakser.

## 🤩 4 - Nyt den nye webappen din!
1. Trykk på "Go to resource"
2. I "Overview"-tabben, trykk på lenken under "Default domain". Den skal ha navnet du satte på webappen din + ".azurewebsites.net"
3. Trykk på denne og se at appen din we oppe og kjører i skyen!

## ⚙️ 5 - Sett opp deployment med GitHub Actions

1. Gå til koden din i GitHub som du klonet tidligere
2. Trykk på "Actions"
3. Her kan skal vi finne en workflow som Microsoft har laget, som heter "Deploy a Python app to an Azure Web App". Velg "Configure".
4. Legg til riktig navn på webappen din, samt riktig versjon av Python. 
5. Helt nederst i denne filen ser du `publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}`. Dette er koblingen vår mellom GitHub og Azure. Denne skal vi legge inn nå.
   
## 🖇️ 6 - Koble sammen GitHub og Azure
1. Gå til webappen din i Azure, deretter "Settings" og "Configuration". 
2. Skru på "SCM Basic Auth Publishing Credentials" og "FTP Basic Auth Publishing Credentials". Siden dette kun er en demo, så er det ikke nødvendig med mer autentisering, og det gjør det lettere få opp denne demoen ;-)
3. Mens du er inne i "Configuration", legg til følgende i boksen "Startup Command": `gunicorn --bind=0.0.0.0 --timeout 600 app:app`. Dette gir Azure beskjed om å starte Flask-appen den snart skal kjøre.
4. Trykk "Save" og tilbake i "Overview" kan vi gi den en restart, slik at alt er på stell.
5. Her kan vi trykke på "Download publish profile".
6. Tilbake i GitHub, gå til "Settings" -> "Secrets and variables" -> "Actions".
7. Legg til en ny secret her med navnet `AZURE_WEBAPP_PUBLISH_PROFILE` og innholdet i profilen vi nettopp lasted ned fra Azure. 

## 🚀 7 - Få koden din opp i skyen
1. I GitHub, gå til "Actions" og kjør den nye workflowen din. Da skal den sende koden din opp til Azure, der webappen din blir bygget og snart er klar til å nytes.
2. Gå til adressen til webappen din, vent litt og refresh! Snart skal du se at koden din er oppe!

## Bonus
Endre det du ønsker i filen templates/index.html, push det opp til GitHub og se om nettsiden din oppdateres!

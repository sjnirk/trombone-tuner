# Online opslag op je eigen AWS (optioneel)

Zonder dit werkt Trombone Coach gewoon, met je gegevens alleen op het toestel. Met dit sjabloon krijg je:

- **Login** (Cognito): alleen jij, met je e-mailadres en een eigen wachtwoord. Je kunt jezelf niet registreren; het account wordt door het sjabloon aangemaakt.
- **Online opslag** (DynamoDB, versleuteld): je log, voortgang en instellingen, per gebruiker gescheiden.
- **Synchronisatie** tussen je toestellen. Offline blijft alles werken; zodra je online bent wordt bijgewerkt (per onderdeel wint de nieuwste versie).
- **Budgetalarm**: een e-mail als de kosten boven $1 per maand dreigen te komen.

De app zelf blijft op GitHub Pages. In AWS staan alleen de login, een kleine API (API Gateway + Lambda) en de database.

**Kosten:** voor één gebruiker blijft dit vrijwel zeker binnen de gratis laag of op enkele centen per maand. Het budgetalarm waarschuwt als dat niet zo is.

## Installeren (±5 minuten, eenmalig)

1. Log in op **console.aws.amazon.com** en kies rechtsboven de regio **Europe (Frankfurt) eu-central-1**.
2. Zoek **CloudFormation** en kies **Create stack → With new resources (standard)**.
3. Kies **Upload a template file**, selecteer [`template.yaml`](template.yaml) en klik **Next**.
4. **Stack name:** `trombone-coach`. **Email:** je eigen e-mailadres. Laat de rest staan. **Next**, nog eens **Next**.
5. Vink onderaan aan: *I acknowledge that AWS CloudFormation might create IAM resources*. Klik **Submit**.
6. Wacht tot de status **CREATE_COMPLETE** is (2 à 4 minuten).
7. Open het tabblad **Outputs** en kopieer de waarde bij **AppConfig** (één regel die begint met `{"region"`). Er staat niets geheims in.
8. Zet die regel in [`../config.js`](../config.js) als `window.TC_CLOUD = { … };`, of geef hem aan Claude.

Je krijgt een e-mail met een **tijdelijk wachtwoord**. Open de app, ga naar **Logboek → Online opslag → Inloggen**, log in met je e-mailadres en dat wachtwoord, en kies een eigen wachtwoord. Wat al op je toestel stond, wordt meteen online gezet. Doe hetzelfde op je andere toestellen.

## Veiligheid

- Er staan geen sleutels of wachtwoorden in deze repo of in de app. `config.js` bevat alleen openbare adressen.
- Inloggen gaat via Cognito met PKCE. De API accepteert alleen geldige tokens, en elke gebruiker ziet alleen zijn eigen gegevens (de sleutel is de gebruikers-ID uit het token).
- De API accepteert alleen de bekende onderdelen (`settings/profiel`, `log/<datum>`, `voortgang/<stuk>`) tot 64 kB, met een limiet van 10 verzoeken per seconde.
- De database en de gebruikerspool zijn beveiligd tegen per ongeluk verwijderen.

## Weer verwijderen

1. Maak in de app een backup (Logboek → Backup).
2. Zet in de AWS-console de verwijderbeveiliging uit: **Cognito → User pools → trombone-coach-… → Settings → Deletion protection**, en **DynamoDB → Tables → … → Additional settings → Deletion protection**.
3. **CloudFormation → trombone-coach → Delete**. De tabel blijft bewust bewaard (Retain); verwijder hem daarna zelf in DynamoDB als je zeker bent.
4. Zet in `config.js` weer `window.TC_CLOUD = null;`.

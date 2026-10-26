# Trombone Coach

Dagelijkse oefencoach met live tuner voor tenortrombone in Bes (vioolsleutel), op weg naar de brassband.

**Openen:** https://sjnirk.github.io/trombone-tuner/
Tip: zet hem op je beginscherm (Safari → Deel → *Zet op beginscherm*) en open hem altijd vandaar.

## Wat erin zit
- **Vandaag:** sessie van 10 minuten in drie blokken (lange tonen, lipslurs en posities, oefening) met timer, metronoom en stemtoon. Leerlijn van 8 weken in notenschrift, met posities en notennamen, theorie per week, en een mix van brassband (recht, legato) en bigband (swing).
- **Tuner:** luistert via de microfoon: geschreven noot, positie (met alternatieven), afwijking in cent en een spoor van 8 seconden. Met *Meespelen* volgt hij een stuk noot voor noot en geeft hij per noot de zuiverheid.
- **Trainer:** noten lezen (op naam of positie) en ritme meetikken, op niveau van de week.
- **Tempo:** metronoom met maatsoort en tik-tempo, en een stemtoon per noot.
- **Logboek:** 60-dagenraster, reeks, checkpoint, stukken met de doorgaanregel (3 dagen foutloos op tempo = beheerst), notities en backup.

## Privacy
Alles gebeurt in je eigen browser. Je log, voortgang en notities staan alleen op je toestel (localStorage), nergens online. De microfoon is alleen aan zolang je hem aanzet; er wordt niets opgenomen of verstuurd. Deze repo bevat alleen code, geen persoonlijke gegevens.

Let op: Safari en een app op het beginscherm hebben elk hun eigen opslag. Kies er één, en maak af en toe een backup via Logboek → Backup.

## Techniek
Eén HTML-bestand zonder build. Notenschrift via VexFlow 4.2.3 (jsDelivr), toonhoogte met YIN in de browser.

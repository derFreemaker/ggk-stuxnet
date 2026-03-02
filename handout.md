## Was ist Stuxnet?

**Zweck:** Hochspezialisierter Computerwurm, entwickelt um iranische Uranzentrifugen zu sabotieren

**Entdeckung:** Juni 2010 in Weißrussland | Aktiv seit ca. Juni 2009

**Besonderheiten:**
- 20x komplexer als normale Malware
- Nutzte 4 Zero-Day-Exploits (unbekannte Sicherheitslücken)
- 2 gestohlene digitale Signaturen
- Entwicklungsaufwand: 10 Programmierer × 2-3 Jahre = 20-30 Personenjahre
- Erster Angriff, der digitale und physische Welt verband

## Historischer Kontext

**Das Problem:**
- Iran entwickelt Atomprogramm (seit 1950er)
- 2002: Enthüllung geheimer Atomanlagen in Natanz
- Internationale Gemeinschaft fürchtet Atomwaffenentwicklung
- Optionen: Diplomatie (langsam), Krieg / Militär Operation (riskant), Sabotage (?)

**Die Anlage Natanz:**
- Unterirdisches Urananreicherungszentrum
- Ca. 9.000 Zentrifugen installiert
- Vom Internet getrennt (Air-Gap)

## Wie funktionierte Stuxnet?

**Infektionsweg:**
1. USB-Stick wird in Computer gesteckt (wahrscheinlich über Zulieferer/Techniker)
2. Automatische Ausführung durch Windows-Schwachstelle
3. Verbreitung über Netzwerke
4. Suche nach spezifischem Ziel: Steuerungen mit 984 Zentrifugen

**Die Sabotage:**
- Manipulation der Zentrifugen-Geschwindigkeit
- Gleichzeitige Manipulation der Anzeigen (Operatoren sahen normale Werte)
- Ergebnis: Ca. 1.000 Zentrifugen zerstört, Programm um 1-2 Jahre verzögert

**Kollateralschaden:**
- Über 100.000 Computer weltweit infiziert
- Größte Konzentration: Iran (60%), Indonesien, Indien

## Wer steckt dahinter?

**Offiziell:** Niemand hat sich bekannt

**Indizien für USA + Israel:**
- Technische Komplexität → deutet auf größere Ressourcen
- Politisches Motiv (Iran-Konflikt)
- New York Times (2012): "Operation Olympic Games"
- Mögliche weitere Beteiligung: Niederlande, Deutschland, UK/Frankreich

**Rolle Deutschlands:**
- Siemens-Technologie war das Ziel (offiziell keine Beteiligung)
- Deutsche Forscher (Ralph Langner, Frank Rieger) entschlüsselten Stuxnet
- Mögliche nachrichtendienstliche Unterstützung (unbestätigt)

## Begriffe

- **Zero-Day-Exploit:** Sicherheitslücke, die dem Hersteller unbekannt ist
- **Air-Gap:** Physische Trennung vom Internet

## Quellen
- https://www.youtube.com/watch?v=Lc6qNCVHyFo
- https://www.csoonline.com/article/562691/stuxnet-explained-the-first-known-cyberweapon.html
- https://2001-2009.state.gov/r/pa/prs/ps/2003/20439.htm
- https://edition.cnn.com/2002/WORLD/meast/12/13/iran.nuclear/
- https://www.nytimes.com/2012/06/01/world/middleeast/obama-ordered-wave-of-cyberattacks-against-iran.html?_r=2&smid=tw-nytimes&seid=auto
- https://www.spiegel.de/politik/ausland/atomstreit-iran-brueskiert-den-westen-mit-neuen-uran-plaenen-a-664126.html
- https://www.researchgate.net/publication/267156195_Stuxnet_A_new_Cyberwar_weapon_Analysis_from_a_technical_point_of_view

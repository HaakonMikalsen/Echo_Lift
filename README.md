# Norsk
## Oppsummering av analog kretsdeler - Av Håkon Kartveit Mikalsen og Sigurd Berg
For å motta og behandle signalet er det valgt å bruke asynkront system. Dette senker kompleksiteten og kostnaden. En hydrofon mottar signalet og forsterkes. To forskjellige filter med senterfrekvens rundt FSK-frekvensene brukes for å isolere båndene i signalet. Omhyldringsavlesere sammen med avgjøringsenheter brukes for å identifisere om det er mottatt et signal i hver av båndene 
![alt text](image-6.png)
Det implementerte analoge systemet består av en hydrofon med en forforsterker og
![alt text](image-5.png)
Signalet som skulle mottas og dekodes er illustrert under
![alt text](image-17.png)

### Fullstendig krets
![alt text](image-16.png)

### Hydrofon
Hydrofonen er konstruert av en plastsylynder, lim og et piezoelektrisk element. Konstruksjonen kan forbedres og hadde ikke den best ønskelige frekvensresponsen
![alt text](image-7.png)
![alt text](image-8.png)

### Forforsterker
Element et hydrofonen er et piezoelektrisk element. Det er derfor valgt å bruke en charge amplifier.
![alt text](image-9.png)

### Nivåregulator / Automatic gain control
Nivåregulator er implementert med en variable gain forsterker som er styrt av en kontroll krets som måler den gjennomsnittlige spenningen til signalet. Kretsen kunne vært forbedret med høyere forsterkning, men fungerte som ønsket.
![alt text](image-10.png)
![alt text](image-11.png)

### Filter
Signalet ble så filtrert i 2 båndpass filter som fungerte som ønsket. Filtertopoligien valgt er et Delyannis-Friend båndpass da denne topoligien er relativt lite sensitivt til komponenttoleranser, har en lett justerbar Q-faktor og lar en forsterke et bånd rundt senterfrekvensen
![alt text](image-12.png)
![alt text](image-13.png)

### Omhyldringsavleser og avgjøringsenhet 
Det ble brukt en grunnleggende omhylringsavleser til å måle amplitudespenningen på signalet etter filterene
![alt text](image-14.png)
Denne ble brukt sammen med en komparator til å avgjøre om det er mottatt et signal med en gitt frekvens. Signalet fra komparatoren er omgjort til et pull-up signal på 3.3V som ble brukt av FPGA enheten. 
![alt text](image-15.png)


## Prosjektet - Echo Lift
Echo Lift er en prototype av et produkt utviklet i faget Elektronisk systemdesign, prosjekt. Faget besto av å kartlegge en kundes ønsker og problemstillinger og utvikle et produkt for å løse dem. Prototypen består av et undervannskomunikasjonssystem som aktiverer en reservebøye som skal redde opp tapt fiskeutstyr. Prototypen skulle både vise proof of concept og utforske løsninger for å redusere enhets kostnad og påvirkaesle av økosystemet. 

Prosjektet er laget av Albert Waagaard Fougner, Fredrik Sanner, Håkon
Kartveit Mikalsen, Jacob Halsne Berentsen, Sigurd Berg, og
Tario Solberg Hanski


## Bakgrunn og funksjon
En stor mengde fiskeutstyr går tapt hvert år og en del av dette er teiner. Det er estimert at
rundt 1% av en fiskebåt sine teiner går tapt hvert år globalt, og i noen områder går dette
helt opp til 30%. Det tilsvarer over 25 millioner teiner hvert år. Dette bidrar både til
utslipp av plastikk, og spøkelsesfisking som er svært skadelig for økosystemet. Tapt utstyr
fører også til en uønsket økonomisk utgift både for fiskere og opprydningsarbeidere.

Konseptet baserer seg på å forenkle dette oppryddingsarbeidet og øke antall teiner som
fiskerne klarer å hente opp selv. En liten og billig reservebøye festes til teinene. Denne
skal kunne aktiveres akustisk av en fisker og slippe ut reservebøya med en tynn ledelinje
som flyter til overflaten. Etter det kan et tau med krok senkes ned ved hjelp av ledelinen,
og hektes på teina, slik at den kan trekkes opp igjen. Konseptet kan også integreres med
digitale merkesystemer for å hjelpe med å finne det generelle området som teina ligger i
før man aktiverer reservebøya
![alt text](image.png)

## Overordnet system
Systemet består av en undervanns avsender som sender en adresse med en modifisert FSK-modulering. Signalet mottas og behandles og dekodes analogt for å hente ut den avsendte adressen. Den mottatte adressen feilkorrigert av en FPGA. Etter feilkorrigering sjekkes adressen mot enhetens adresse. På denne måten aktiveres kun den ønskede reservebøyen. Reservebøyen bruker et gass system for oppløsning for å redusere bevegelige deler og unngå å legge igjen nedtyngede materiale på havbunnen.  

![alt text](image-1.png)

<!-- 
## Prototype
### Avsending - Tario Solberg Hanski
Signalet sendes med en modifisert FSK-modulering, da dette gir et mer pålitelig resul-
tat. Tradisjonell FSK, Frequency-Shift Keying, baserer seg på at to diskre frekvenser representerer ulike bits. For å slippe å ha en form for synkronisering mellom sender og mottakeren, benyttes 3
diskre frekvenser. Den tredje frekvensen vil bli spilt mellom hver bit av adressen.. Dette har til hensikt å bryte opp hver eneste bit uten en internklokke i
mottakeren som er synkronisert. I tillegg vil en frekvensen som markerer mellomrommet
gjøre at mottakeren lettere kan stille seg inn på volumet til senderen

![alt text](image-2.png)


Det implementerte systemet (se bilde under), og er ikke tiltenkt bruk i et ferdig
produkt, men tjener sitt formål som demonstrasjon av konseptet. Det overordnede sender-
systemet. For å enkelt kunne teste ulike frekvenser og bitlengder
er signalgeneringen implementert i Python, da dette muliggjør rask iterasjon uten kom-
pileringssteg og opplastning på mikrokontrolleren. Den genererte lydfilen overføres til
en mobiltelefon, hvorfra den sendes via Bluetooth.
![alt text](image-3.png)
![alt text](image-4.png)

### Mottakning og analog behandling - Håkon Kartveit Mikalsen og Sigurd Berg
For å motta og behandle signalet er det valgt å bruke asynkront system. Dette senker kompleksiteten og kostnaden. En hydrofon mottar signalet og forsterkes. To forskjellige filter med senterfrekvens rundt FSK-frekvensene brukes for å isolere båndene i signalet. Omhyldringsavlesere sammen med avgjøringsenheter brukes for å identifisere om det er mottatt et signal i hver av båndene 
![alt text](image-6.png)
Det implementerte analoge systemet består av en hydrofon med en forforsterker og
![alt text](image-5.png) -->
# Floor-plan Hassio
*Ringrazio lukevink che ha creato questa spettacolare interfaccia. Questo è il [link](https://github.com/lukevink/hass-config-lajv "link") al suo progetto dove ha implementato molte più funzionalità. Vi lascio anche il link sul forum di [home assistant](https://community.home-assistant.io/t/floorplan-ui-with-color-synced-lights/169417 "home assistant") per domande e/o problemi. Questa guida seguirà molto quella di lukevink; l'adatterò sulla mia configurazione e cercherò di spiegare al meglio alcuni passaggi che dalla guida di lukevink non si capiscono molto, però il ringraziamento va tutto a lui!*

[Hass.io](https://www.home-assistant.io/ "Hass.io") versione 107.7 installata su [raspberrypi](https://www.raspberrypi.org/ "raspberrypi 4 4gb") e in esecuzione su un tablet 10 pollici con [Fully Kiosk Browser](https://play.google.com/store/apps/details?id=de.ozerov.fully&hl=en "Fully Kiosk Browser")

![stanze](https://github.com/bootpi/floor-plan/blob/master/stanze.gif?raw=true)

------------

![dispositivi](https://github.com/bootpi/floor-plan/blob/master/dispositivi.gif?raw=true)

------------

## Funzionalità
- Planimetria 3d interattiva, con possibilità di controllare luci e sensori vari
- Vista HomeKit per controllare le prese smart
- Data, ora e meteo
- Device_tracker dei familiari

## ATTENZIONE
Questo non è un progetto per il quale è possibile copiare ed incollare la configurazione, se provi a eseguire la mia configurazione avrai tanti errori. 
Vi consiglio fortemente di leggere qualche guida di [CSS](https://www.w3schools.com/css/ "css"). Poichè la configurazione è basata su `picture-elements`, e ogni card è progettata con CSS.
**NB** Questo progetto è consigliato per tablet da 10 pollici.

## Barra laterale
La barra laterale viene ripetuta su ogni vista nel file lovelace.yaml e include pulsanti per le viste. 
- **Controllo Stanze:** controlla tutte le luci i vari sensori, le videocamere, e l'allarme
- **Controllo Luci:** accendi e spegni tutte le luci presenti in "Controllo Stanze"
- **Dispositivi:** controllo dei dispositivi smart al di fuori delle luci prensenti in "Controllo Stanze"(prese smart, ciabatte smart")
- **Meteo:** mostra le previsioni meteo
- **Persone:** mostra i familiari prensti a casa

## Hardware
- [Raspberry Pi 4 4GB](https://www.amazon.it/dp/B07WQSYHRJ/ref=cm_sw_em_r_mt_dp_U_ZFEGEbG3X6EN8)
- [Shelly1 ](https://www.shellyitalia.com/shelly-1-v3/ "Shelly1 ")
- [Sensore temperatura](https://www.amazon.it/Xiaomi-Smart-Temperature-humidity-Sensor/dp/B074SX1FNP "Sensore temperatura")
- [Sensore porte](https://www.amazon.it/dp/B07PYG6GVK/ref=cm_sw_em_r_mt_dp_U_WMEGEbPGSNQVT)
- [Sensore consumo energetico](https://hassiohelp.eu/2019/03/27/pzem-016/)

------------

## Progettazione della planimetria
Per prima cosa ho progettato la planimetria con [SweetHome 3D](http://sweethome3d.com/it/ "SweetHome 3D"), vi lascio questa [guida](https://aarongodfrey.dev/home%20automation/tips_for_creating_a_3d_floorplan_using_sweethome3d/ "guida") sulla realizzazione, ed ho fatto il render di tutte le luci; in che senso? Praticamente dovete creare tante foto quante le luci (N Luci= N foto, una foto per una singola luce accesa) 

# Floor-plan Hassio
*Ringrazione lukevink che ha creato questa spettacolare interfaccia. Questo è il [link](https://github.com/lukevink/hass-config-lajv "link") al suo progetto dove ha implementato molte più funzionalità. Vi lascio anche il link sul forum di [home assistant](https://community.home-assistant.io/t/floorplan-ui-with-color-synced-lights/169417 "home assistant") per domande e/o problemi. Questa guida seguià molto quella di lukevink; l'adatterò sulla mia configurazione e cercherò di spiegare al meglio alcuni passaggi che dalla guida di lukevink non si capiscono molto, però il ringraziamento va tutto a lui*

[Hass.io](https://www.home-assistant.io/ "Hass.io") versione 107.7 installata su [raspberrypi 4 4gb](https://www.raspberrypi.org/ "raspberrypi 4 4gb") e in esecuzione su un tablet 10 pollici con [Fully Kiosk Browser](https://play.google.com/store/apps/details?id=de.ozerov.fully&hl=en "Fully Kiosk Browser")

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
**NB** Questo 

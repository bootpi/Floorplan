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
- **Persone:** mostra i familiari presenti a casa

## Hardware
- [Raspberry Pi 4 4GB](https://www.amazon.it/dp/B07WQSYHRJ/ref=cm_sw_em_r_mt_dp_U_ZFEGEbG3X6EN8)
- [Shelly1 ](https://www.shellyitalia.com/shelly-1-v3/ "Shelly1 ")
- [Sensore temperatura](https://www.amazon.it/Xiaomi-Smart-Temperature-humidity-Sensor/dp/B074SX1FNP "Sensore temperatura")
- [Sensore porte](https://www.amazon.it/dp/B07PYG6GVK/ref=cm_sw_em_r_mt_dp_U_WMEGEbPGSNQVT)
- [Sensore consumo energetico](https://hassiohelp.eu/2019/03/27/pzem-016/)

------------

## Progettazione della planimetria
Per prima cosa ho progettato la planimetria con [SweetHome 3D](http://sweethome3d.com/it/ "SweetHome 3D"), vi lascio questa [guida](https://aarongodfrey.dev/home%20automation/tips_for_creating_a_3d_floorplan_using_sweethome3d/ "guida") sulla realizzazione, ed ho fatto il render di tutte le luci; in che senso? Praticamente dovete creare tante foto quante le luci (N Luci= N foto, una foto per una singola luce accesa). Per il render ho usato queste caratteristiche `width: 1900` e `height: 1500`, qualità migliore e per l'orario 12.30 e 20.30 (20.30 anche per il render delle luci).
Alla fine di tutto dovrete avere tot foto per tot luci e in più 2 foto, una di giorno e una di sera. Questo perchè grazie al sensore `sun.sun` andreamo a visualizzare la piantina in base al sole (con l'alba e il tramonto)

![mapped](https://github.com/bootpi/floor-plan/blob/master/mapped-lights-info1.png?raw=true)
*Questa immagine è stata presa dal sito di lukevink, è per solo scopo illustrativio e perchè è ben fatta!*

Fatte le foto useremo un altro programma, molto fondamentale per modificare tutte le immagini, [Gimp](https://www.gimp.org/ "Gimp"). Vi lascio quest'altra [guida](https://aarongodfrey.dev/home%20automation/creating-a-3d-floorplan-in-home-assistant/#creating-the-images "guida"). 
In pratica andiamo a "bucare" o "eliminare" lo sfondo delle immagini e andiamo a rtiagliarle in due zone (zona giorno e zona notte) come nelle foto qui sotto:

![bagno1](https://github.com/bootpi/floor-plan/blob/master/floorplan_bagno_1.png?raw=true)

------------

![salone1](https://github.com/bootpi/floor-plan/blob/master/floorplan_salone_1.png?raw=true)

Per un taglio preciso ed uguale vi consiglio di aprire tutte le foto come livelli su Gimp e ritagliare il primo livello cosi poi da avere lo stesso taglio per i livelli successivi (quella del giorno e della notte non devono essere tagliate). Esportate le immagini con nomi specifici (es: floorplan_salone_1.png; floorplan_bagno.png ecc...).
Apriamo un novo file con queste misure 2560x1600 (misure del dislay del tablet 10 pollici) e anche sidebarBG2.png (barra laterale); posizioniamo quest'ultimo come in foto e questa sarà la base, con l'immagine di notte posizionata al centro della parte bianca rimanente, di tutte le foto che apriremo come livelli.

![base](https://github.com/bootpi/floor-plan/blob/master/base.png?raw=true)

A questo punto apriamo tutte le foto come livelli e le posizioniamo, con la massima precisione,  sopra la piantina di notte (fate questo anche con la piantina di giorno). Dopodichè eliminiamo la barra laterale, eliminiamo nuovamente lo sfondo ed un livello alla volta esportiamo i file cosi da avere le piantine nella posizione corretta per le dimensioni del tablet (salvate anche la piantina di giorno e di notte).

------------


## Lovelace

#### Card
Questi sono i plugin e le integrazioni che ho usato (vi lascio il link del repository):
- [Config Template Card](https://github.com/iantrich/config-template-card "Config template card")
- [Picture Elements](https://www.home-assistant.io/lovelace/picture-elements/ "Picture Elements")
- [Custom Header](https://github.com/maykar/custom-header)
- [Browser-mod](https://github.com/thomasloven/hass-browser_mod)
- [Lovelace Preloader Card](https://github.com/gadgetchnnel/lovelace-card-preloader)
- [Card Mod](https://github.com/thomasloven/lovelace-card-mod)
- [Ligth Entity Card](https://github.com/ljmerza/light-entity-card)
- [Layout Card](https://github.com/thomasloven/lovelace-layout-card)
- [Vertical Stack](https://github.com/ofekashery/vertical-stack-in-card)
- [Popup Backdrop Filter](https://github.com/gabe565/popup-backdrop-filter)
- [Simple Weather Card Bundle](https://github.com/kalkih/simple-weather-card)
- [Homekit Panel](https://github.com/DBuit/Homekit-panel-card)
- [Auto Entities](https://github.com/thomasloven/lovelace-auto-entities)

Card modificate da lukevink (le trovate nella cartella "js"):
- Light Slider Card 

#### Codice
In questa parte cercherò di analizarvi il codice passo passo... Abbiate pietà se dovessi sbagliare qualcosa :tw-1f602:
```yaml
custom_header:
  compact_mode: true
  editor_warnigs: false
  exceptions:
    - conditions:
        user: 'Tablet, tablet'
      config:
        hidden_tab_redirect: false
        kiosk_mode: true
    - conditions:
        user_agent: 'Mozilla/5.0 (Android 7.1.2; Tablet; rv:68.0) Gecki/68.0 Firefox/68.0'
      config:
        hidden_tab_redirect: false
        kiosk_mode: true
```
[`custom_header`](https://github.com/maykar/custom-header) serve per impostare il display in `kiosk_mode` che permette di nascondere la barra laterale e la barra delle pagine di hassio cosi da avere una inquadratura totale per il tablet. Come potete vedere ho imposta la `kiosk_mode` solo all'utente tablet ed al [`user_agent`](https://www.whatsmyua.info/).

```yaml
- type: 'custom:config-template-card'
   entities:
	   - light.bloom_hue                 # STRISCIA LED TV
	   - input_boolean.salone_1     # SALONE
	   - input_boolean.salone_2     # INGRESSO
	   - input_boolean.salone_3     # CORRIDOIO
	   - input_boolean.salone_4     # LAMPADA
	   - input_boolean.camera_1    # CAMERA MATRIMONIALE
	   - input_boolean.camera_2    # BAJOUR SINISTRA
	   - input_boolean.camera_3    # BAJOUR DESTRA
	   - input_boolean.bagno_1     # BAGNO_1
	   - input_boolean.bagno_2     # BAGNO_2
	   - input_boolean.cameretta   # CAMERETTA
	   - input_boolean.ripostiglio   # RIPOSTIGLIO
	   - binary_sensor.porta_contact
	   - group.all_entity
	   - sensor.cpu_temp
	   - sensor.0x00158d000277484c_temperature
	   - camera.ingresso
	   - camera.salone
   card:
	   type: 'custom:hui-picture-elements-card'
```
[`config-template-card`](https://github.com/iantrich/config-template-card) serve per passare tutte l'entità elencate sotto ai modelli utilizzati nei CSS. La card `picture-elements` è racchiusa in questa card.
Ho usato gli `input_boolean` perchè mi devono ancora arrivare gli shelly, ma voi potete benissimo mettere o `lights` o `switch` a seconda della vostra configurazione.

```yaml
- action: none
   entity: sun.sun
   hold_action:
   		action: none
   state_image:
   		above_horizon: /local/floorplan/floorplan/floorplan_day.png
   		below_horizon: /local/floorplan/transparent.png
   style:
   		height: 100%
   		left: 50%
   		mix-blend-mode: lighten
   		opacity: '${ states[''sensor.sunlight_opacity''].state }'
   		top: 50%
   		width: 100%
   tap_action:
   		action: none
   type: image
```
Questo è il sensore `sun.sun` che servirà per aggiungere un livello sopra la piantina di notte e quindi visualizzare la piantina di giorno `flooplan_day.png`. Con `transparent.png` quando è sera vedremo `floorplan_night.png`.
L'immagine `transparent.png` viene utilizzata sui `state-image` del `picture-elements` per nascondere gli elementi se non necessari.

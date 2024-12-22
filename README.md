# 🛠️ YAUB 🤷‍♂️

Sei willkommen zur *Yet another Useless Box*, dem ambitioniertesten Projekt auf dieser Erde, das absolut Tag und Nacht nichts Nützliches leistet! 🎉

## 📦 Was ist die Useless Box?

Die *Useless Box* ist ein ESPHome-basiertes Meisterwerk der Sinnlosigkeit. Sie besteht aus einer Box, einem Schalter und... einem einzigen Ziel: **sich selbst auszuschalten.** 🔄

Stell dir vor: Du betätigst einen Schalter mit der Hoffnung, irgendetwas Tolles zu bewirken. Aber nein – ein kleiner Servomotor aktiviert sich, eine Klappe öffnet sich, und ein mechanischer Finger schaltet das Ganze wieder aus. Das ist Kunst! 🖼️

## 🎯 Ziel des Projekts

> "Weil wir können."  
> – Einstein, wahrscheinlich. oder... Sun Tzu, ist sogar wahrscheinlicher.  


Dieses Projekt ist perfekt, wenn du:
- Deinen ESP32 auf ein neues (tiefes) Level muss 📉  
- Deine Lötkolben-Skills testen willst 🔥
- Freunde, Familie oder Haustiere mal wieder Lachen müssen 😂
- Einfach mal nichts erreichen darfst 🚫
- Zeit auf hohem Nivea verschwenden musst ⏳  


## 🛠️ Hardware

Um das maximal sinnlose Erlebnis zu schaffen, benötigst du:
- 1x ESP32 (weil Overkill!)  
- 1x Mikro-Servomotor 
- 1x Kippschalter (den du bereuen wirst)  
- 1x Box (Zigarrenkiste oder eine alte Keksdose 🍪)  
- Kabel, Lötkolben, Heissklebepistole gepaart mit purer Entschlossenheit und Durchhaltevermögen

### 🖼️ Beispielaufbau

```plaintext
[ Schalter ] -----> [ ESP ] ---> [ Servo ] ---> [ Schalter deaktiviert ]
```

### GPIO-Setup

| Bauteil        | GPIO-Pin |  
|----------------|----------|  
| Servo (PWM)    | GPIO13   |  
| Schalter (Input)| GPIO12   |  

### 🔧 Software
YAML-Konfiguration (ESPHome)
Hier ein minimaler YAML-Auszug, um die Sinnlosigkeit perfekt zu machen:

```yaml
esphome:
  name: YAUB
  friendly_name: YetAnotherUslessBox

ota:
  - platform: esphome
    password: "REDACTED"

captive_portal:

esp32:
  board: esp32dev
  framework:
    #type: arduino
    type: esp-idf

mqtt:
  broker: !secret mqtt_host
  id: mqtt_client

wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  domain: !secret wifi_domain  

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "Uselessbox Fall Back Spot"
    password: "STAs1li2612X"

web_server:
  port: 80

# Enable Home Assistant API
api:
  encryption:
    key: !secret homeassistant_api
  services:
    - service: control_servo
      variables:
        level: float
      then:
        - servo.write:
            id: useless_servo
            level: !lambda 'return level / 100.0;'

binary_sensor:
  - platform: gpio
    pin: GPIO12
    name: "Useless Switch"
    on_press:
      - delay: 50ms
      - servo.write:
          id: useless_servo
          level: -65%
      - delay: 1200ms
      - servo.write:
          id: useless_servo
          level: 100%


number:
  - platform: template
    name: Servo Control
    min_value: -60
    initial_value: 0
    max_value: 100
    step: 1
    optimistic: true
    set_action:
      then:
        - servo.write:
            id: useless_servo
            level: !lambda 'return x / 100.0;'

servo:
  - id: useless_servo
    output: pwm_output
    auto_detach_time: 3s

output:
  - platform: ledc
    id: pwm_output
    pin: GPIO13
    frequency: 50 Hz

logger:

```
### Installation
Lade die yaml Datei auf dein ESPHome und kompiliere es. 
Dann uplaode es auf deinen ESP32.
Montiere den Servo so, dass er den Schalter deaktiviert.
Schalte es ein und genieße den Moment der Enttäuschung.
### 🚀 Funktionsweise
Du: Schalter einschalten.
Box: Nope.
Du: Schalter erneut einschalten.
Box: Nope.
Wiederhole, bis du deine Lebensentscheidungen hinterfragst.
### 🏆 Bonus-Ideen
Füge einen Lautsprecher hinzu, der "Nein" sagt.
Verbinde die Box mit Home Assistant, damit du sie über eine App deaktivieren kannst. (Noch mehr Sinnlosigkeit!)
Statte sie mit RGB-LEDs aus, um sie hübsch und sinnlos zu machen.
### ❤️ Warum?
Warum nicht? Manchmal ist das Leben am schönsten, wenn es keinen Zweck hat.

Disclaimer: Die Useless Box ist NICHT nutzlos genug, um dein Leben vollständig zu ruinieren. Für ernsthafte Sinnlosigkeit empfehlen wir Steuererklärungen.
### Troubleshoot
 * an Usb hängen und log ansehen (https://web.esphome.io/)
 * mit Home Assistant verbinden & das log ansehen
 * Servo Stromversorgung, Ansteuerung oder Servo defekt: wenn der servo nicht mehr fest hält und "entspannt" ist
 * Schalter Verbindung wenn Schalteränderungen keinen Logeintrag erzeugen
### Und das wurde nun doch tatsächlich Realisiert mit
 * https://www.youtube.com/watch?v=-SJbdPvgQnE
 * https://www.printables.com/model/665030-useless-box
   keine Blechschachteln vor Weihnachten!!!
 * https://www.tutti.ch/de/q/suche/Ak7Frb252b2x1dCBzY2hhbHRlcsCUwMDAwA?sorting=newest&page=1&query=konvolut+schalter
 * https://de.aliexpress.com/w/wholesale-l%C3%B6tstation-digital.html
 * https://de.aliexpress.com/w/wholesale-usb-kabel.html?spm=a2g0o.productlist.search.0
 * Irgendeinen Laptop
 * https://esphome.io/
 * https://www.home-assistant.io/
 * https://photos.app.goo.gl/wdgyEKsd84tU9TaA8

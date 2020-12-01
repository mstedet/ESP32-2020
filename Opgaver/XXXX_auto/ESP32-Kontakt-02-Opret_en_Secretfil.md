# 02 - Opret en Secretfil 
Gem adgangskoder og andre følsomme data ved hjælp af! Secret
Ligesom i Home Assistant-konfigurationsfiler er det muligt at bruge! Secret i ESPHome. Så i stedet for at have følsomme oplysninger spredt over forskellige konfigurationsfiler, kan du gemme dem alle ét sted.
ESPHome-dashboardet har en Secrets Editor tilgængelig, som er tilgængelig via menuikonet øverst til højre.

## Åben ESPHome's Secrets Editor
* tilføj nu disse liner til filen:
```
My_WiFi_SSID: "HUAWEI-ESP32"
My_WiFi_Pass: "12345678"
My_Access_Pass: "qazwsxedc"
My_AP_Pass: "qwertyuiop"
My_API_Pass: "asdfghjkl"
My_OTA_Pass: "zxcvbnm"
```
* Save & Close filen  

Når du tilføjer noget for første gang via tekstbehandlingen, opretter ESPHome automatisk secrets.yaml-filen inde i ESPHome-mappen i mappen Home Assistant Config.   
* Filem bliver gemt som "/config/esphome/secrets.yaml"

## Åben nu ESP32 configurationsfilen
Efter lagring af data i filen secrets.yaml. For eksempel adgangskoden til WiFi kan du derefter gå til dine ESPHome-enheder og i konfigurationsfilen erstatte adgangskoden med følgende:

### [WiFi Password](https://esphome.io/components/wifi.html#wifi-component)
* fra
```
wifi:
  ssid: "HUAWEI-ESP32"
  password: "12345678"
```
* til 
```
wifi:
  ssid: !secret My_WiFi_SSID
  password: !secret My_WiFi_Pass
```
### [AP Password](https://esphome.io/components/wifi.html#configuration-variables)
* fra
```
  ap:
    ssid: "esp32_01_sekt Fallback Hotspot"
    password: "icec5M2D12pb"
```
til
```
  ap:
    ssid: "esp32_01_sekt Fallback Hotspot"
    password: !secret My_AP_Pass
```
### [API Password](https://esphome.io/components/api.html) 
fra
```
api:
```
til
```
api:
  password: !secret My_API_Pass
```
### [OTA Password](https://esphome.io/components/ota.html)
fra
```
ota:
```
til
```
ota:
  password: !secret My_OTA_Pass
```

* Save & Close filen
Filem bliver gemt som "/config/esphome/esp32_01_sekt.yaml"




## Reprogramer din ESP32 med den nye opsætning
Efter redigering af konfigurationsfilen skal du uploade den til enheden, og den vil erstatte det! Hemmelige navn med de faktiske data, der er på filen secrets.yaml.

* Vælg den USB-port som din ESP32 er forbundet til
* Check Config, hvis ok så fortsæt med næste punkt ellers ret fejl
* Upload nu ændringer til din ESP32


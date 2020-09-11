# Opgave-03 - Byg en ESP32-kontakt med relæ og signal indikator
OK, så du oprettede konfigurationsfilen til ESP32-kontakten. Det har dog kun nogle grundlæggende indstillinger. Hvis du skulle blinke firmwaren til ESP32-kontakten nu, ville den bare oprette forbindelse til din WiFi og intet andet. Så du bliver nødt til at redigere konfigurationsfilen og tilføje et par flere komponenter. For eksempel skifteindstillingerne til at styre relæet for at tænde og slukke for ESP32-kontakten.

## Forbind dit ESP32 Kort som vist på billederne  
![Opgaver-01_bb.png](/Images/Opgaver-01_bb.png) 
### Ledninger tilsluttes som følger:
1. De hvide stifter ved LED forbindes til sorte stifter ved ESP32 (stel)
2. Den røde stift forbindes til ESP32 GPIO-12 
3. Den grønne stift forbindes til ESP32 GPIO-13
4. En hvide stift fra trykknap forbindes til sorte stifter ved ESP32 (stel)
5. En hvid stift fra trykknap forbindes til ESP32 GPIO-2
## Tilføj komponenter til konfigurationsfilen
Lad os gennemgå nogle af de tilgængelige indstillinger, som du kan tilføje. Klik på Rediger for at åbne konfigurationsfilen og indtaste følgende nederst:
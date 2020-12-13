# Sådan installeres Argon One Pi 4 V2
## Tænd / sluk-knap og blæserregulering
1. Forbind til internettet.
2. Åben "Terminal vindue" på din Raspberry OS 
3. Skriv cmmandoen som vist herunder:
``` 
curl https://download.argon40.com/argon1.sh | bash
``` 
### Tænd / Sluk-knappens Funktioner
| Argon One PI 4 State | Action               | Function                           |
| ----                 | ----                 | ----                               |
| OFF                  | Kort tryk            | Tænde for                          |
| ON                   | Langt tryk (> = 3 s) | Blød nedlukning og strømafbrydelse |
| ON                   | Kort tryk (<3 s)     | Ikke noget                         |
| ON                   | Dobbeltklik          | Genstart                           |
| ON                   | Langt tryk (> = 5 s) | Tvungen nedlukning                 |

## Blæserhastighed
| CPU Temp | Ventilatoreffekt |
| ----     | ----             |
| 55 C     | 10%              |
| 60 C     | 55%              | 
| 65 C     | 100%             |

### Ændre disse værdier 
1. Åben et terminal vindue
2. indstat kommandoen som herunder:
``` 
argonone-config
``` 
## Indbygget infrarød modtager
1. For at konfigurere det infrarøde modtager ON / OFF-signal fra Argon ONE V2 og M.2 
2. Skal du indtaste kommandoen i terminal vinduet
```
argonone-ir
```

## Fjern Argon ONE Script
```
argonone-uninstall
```

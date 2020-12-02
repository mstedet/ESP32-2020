# Opgave-01 HomeAutomation
## Opret en nye Automatiseringer

* Klik på Indstillinger -> Automatiseringer -> TILFØJ AUTOMASERING -> SKIP 

## Navn
|  Felt:       | Indhold:                    |
| -----        | -------                     |
| Navn         | Tryk for tænd af RedLed     |
| Beskrivelse  |                             |
| Tilstand     | Enkelt (standard)           |

### Udløsere:
|  Felt:       | Indhold:                    |
| -----        | -------                     |
| Udløsertype  | Enhed                       |
| Enhed        | sekt_auto                   |
| Udløser      | sekt_auto_pir_01 tændte     |
| Varihed      | 00:00:02                    |
  
### Betingelser:
|  Felt:         | Indhold:         |
| -----          | -------          |
| Betingelsetype | Sol              |
| Før            |    Solnedgang    |
| Forskydning    |                  |
| Efter          |                  |
| Forskydning    |                  |

|  Felt:         | Indhold:         |
| -----          | -------          |
| Betingelsetype | Og               |
| Betingelsetype | Enhed            |
| Enhed          | sekt_auto        |
| Betingelse     | sekt_auto_Green LED er til |
| Varighed       |                  |

### Handlinger:
|  Felt:         | Indhold:         |
| -----          | -------          |
| Betingelsetype | Enhed            |
| Enhed          | sekt_auto        |
| Handling       | Tæmd for sekt_auto_Red LED |

## Navn
|  Felt:       | Indhold:                    |
| -----        | -------                     |
| Navn         | Sluk lys efter manglende bevægelse i 30 sec |
| Beskrivelse  |                             |
| Tilstand     | Enkelt (standard)           |

### Udløsere:
|  Felt:       | Indhold:                    |
| -----        | -------                     |
| Udløsertype  | Enhed                       |
| Enhed        | sekt_auto                   |
| Udløser      | sekt_auto_pir_01 slukkede   |
| Varihed      | 00:00:30                    |
  
### Betingelser:

### Handlinger:
|  Felt:         | Indhold:         |
| -----          | -------          |
| Betingelsetype | Enhed            |
| Enhed          | sekt_auto        |
| Handling       | Sluk sekt_auto_Red LED |

## Ændre af Udløsertypen fra Enhed til Tilstand
* Før
### Udløsere:
|  Felt:       | Indhold:                    |
| -----        | -------                     |
| Udløsertype  | Enhed                       |
| Enhed        | sekt_auto                   |
| Udløser      | sekt_auto_pir_01 tændte     |
| Varihed      | 00:00:02                    |

* efter
### Udløsere:
|  Felt:       | Indhold:                       |
| -----        | -------                        |
| Udløsertype  | Tilstand                       |
| Entitet      | binary_sensor.sekt_auto_pir_01 |
| Attribute    |                                |
| Fra          | off                            |
| Til          | on                             |
| Varihed      | 00:00:02                       |


### /config/automations.yaml
```
- id: '1606897819547'
  alias: Tænd rød led
  description: ''
  trigger:
  - platform: state
    entity_id: binary_sensor.sekt_auto_pir_01
    from: 'off'
    to: 'on'
    for: 00:00:01
  condition:
  - condition: device
    type: is_on
    device_id: 5dce63ce6734de8c06febc64d20b4c63
    entity_id: switch.sekt_auto_green_led
    domain: switch
  - condition: and
    conditions:
    - condition: sun
      before: sunset
  action:
  - type: turn_on
    device_id: 5dce63ce6734de8c06febc64d20b4c63
    entity_id: switch.sekt_auto_red_led
    domain: switch
  - type: turn_on
    device_id: fe6001b910330ef4e622334c99e99551
    entity_id: switch.bjepp_auto_red_led
    domain: switch
  mode: single
- id: '1606898401191'
  alias: Sluk rød led efter 5 sec.
  description: ''
  trigger:
  - type: turned_off
    platform: device
    device_id: 5dce63ce6734de8c06febc64d20b4c63
    entity_id: binary_sensor.sekt_auto_pir_01
    domain: binary_sensor
    for:
      hours: 0
      minutes: 0
      seconds: 5
  condition: []
  action:
  - type: turn_off
    device_id: 5dce63ce6734de8c06febc64d20b4c63
    entity_id: switch.sekt_auto_red_led
    domain: switch
  - type: turn_off
    device_id: fe6001b910330ef4e622334c99e99551
    entity_id: switch.bjepp_auto_red_led
    domain: switch
  mode: single
```
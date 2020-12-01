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



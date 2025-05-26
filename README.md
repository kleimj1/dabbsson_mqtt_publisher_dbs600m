# 🚀 Dabbsson MQTT Publisher – Home Assistant Add-on (DBS600M)

Dieses Add-on liest über das Tuya-Protokoll (lokal via WLAN) **DPS-Werte vom Dabbsson DBS600M** aus und veröffentlicht diese regelmäßig via **MQTT Discovery** an Home Assistant.

Damit werden **automatisch Sensoren & Schalter** erstellt – komplett lokal, ohne Tuya-Cloud oder Bluetooth!

---

## ✅ Funktionen

- 📡 Liest alle bekannten DPS-Werte (auch versteckte)
- 🔄 MQTT Discovery: automatische Sensor-/Schalter-Erstellung
- 🔧 Unterstützung für steuerbare Entitäten (z. B. AC Out, Zielwert, Inverter-Modus)
- 🧠 Robuste Wiederverbindung & Logging
- 🖥 UI-basierte Konfiguration

---

## 📦 Installation in Home Assistant

1. Öffne Home Assistant → **Einstellungen → Add-ons → Add-on Store**
2. Klicke oben rechts auf **„Add-on Repository hinzufügen“**
3. Füge dieses Repository ein:

https://github.com/kleimj1/dabbsson_mqtt_publisher_dbs600m

Oder klicke direkt hier:

[![Add-on installieren](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https://github.com/kleimj1/dabbsson_mqtt_publisher_dbs600m)

4. Danach: `Dabbsson MQTT Publisher DBS600M` installieren & konfigurieren

---

## ⚙️ Konfiguration (UI)

| Feld                   | Beschreibung                                  |
|------------------------|----------------------------------------------|
| `device_id`            | Tuya Device ID deines DBS600M                |
| `local_key`            | Tuya Local Key                               |
| `ip`                   | Lokale IP-Adresse (z. B. `192.168.178.30`)    |
| `mqtt_host`            | MQTT Broker Hostname/IP (z. B. `core-mosquitto`) |
| `mqtt_port`            | Meist `1883`                                 |
| `mqtt_topic`           | z. B. `dabbsson`                              |
| `mqtt_discovery_prefix`| Meist `homeassistant`                        |

---

## 📡 MQTT Topics & Home Assistant Discovery

Dieses Add-on erzeugt automatisch MQTT Topics im Format:

### **Beispielhafte Topics:**

| MQTT Topic                  | Beschreibung                   | Schreibbar |
|----------------------------|--------------------------------|------------|
| `dabbsson/status/101`      | PV-Leistung [W]                | ❌         |
| `dabbsson/status/104`      | Inverter-Temperatur [°C]       | ❌         |
| `dabbsson/status/108`      | Wechselrichter EIN/AUS         | ✅         |
| `dabbsson/status/110`      | Power Limit [%]                | ✅         |
| `dabbsson/status/120`      | Batterie SoC [%]               | ❌         |
| `dabbsson/status/126`      | Arbeitsmodus (Eco/Ladung)      | ✅         |

### Steuerung per MQTT:

```bash
mosquitto_pub -h localhost -t dabbsson/command/108 -m true
```

---

### 🔍 Device ID & Local Key finden

Erstelle ein Tuya Cloud Projekt: https://iot.tuya.com  
Verknüpfe dein Smart Life Konto  
Gerät → Device-ID & Local-Key einsehen  
👉 Alternativ über Tools wie `tuya-cli`

---

### 👀 Typische Entitäten in Home Assistant

Nach der Installation erscheinen z. B.:

- `sensor.dabbsson_pv_leistung`
- `sensor.dabbsson_temperatur`
- `sensor.dabbsson_batterie_soc`
- `switch.dabbsson_inverter`
- `number.dabbsson_power_limit`

---

### 🧠 Hinweise

- Das Add-on läuft dauerhaft und liest alle 5 Sekunden
- MQTT-Verbindung wird automatisch aufrechterhalten
- Discovery erfolgt über den Prefix `homeassistant`
- DPS-Definition & Metadaten in `dps_metadata.py`

---

### ❤️ Mitmachen

Fehlt dir ein DPS-Wert oder möchtest du helfen?

➡️ Erstelle ein GitHub Issue oder einen Pull Request unter:  
https://github.com/kleimj1/dabbsson_mqtt_publisher_dbs600m

---

### 🧠 Viel Spaß mit deinem Dabbsson DBS600M in Home Assistant!

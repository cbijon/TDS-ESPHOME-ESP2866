# 🐠 Aquarium Water Quality Monitor (ESP8266 + TDS + Temp)

Ce projet DIY permet de **surveiller la qualité de l’eau d’un aquarium tropical** à l’aide d’un **ESP8266**, d’un **capteur TDS** (Total Dissolved Solids) et d’un **capteur de température DS18B20**.


## ⚙️ Fonctionnalités

- 🧪 Mesure du **TDS** (qualité de l’eau) avec correction automatique selon la température
- 🌡️ Suivi de la **température de l’eau** (DS18B20)
- 📡 Intégration avec **Home Assistant** (via ESPHome)
- 🌐 Interface Web embarquée (consultation des données en local)
- 📊 Compatible avec les dashboards Lovelace
- 🔐 Sécurisé (mot de passe OTA, API chiffrée, accès web protégé)

---

## 🧰 Matériel nécessaire

| Composant                    | Référence                     |
|-----------------------------|-------------------------------|
| Microcontrôleur             | ESP8266 (ESP-01M ou D1 Mini)  |
| Sonde de température        | DS18B20 (étanche)             |
| Capteur TDS                 | Gravity Analog TDS Sensor     |
| Résistance Pull-Up          | 4.7 kΩ                        |
| Alimentation                | 3.3V stable (régulée)         |
| Câbles Dupont / soudure     | Pour les connexions           |

---

## 🖧 Schéma de câblage

- **DS18B20** :
  - VCC → 3.3V
  - GND → GND
  - DATA → GPIO2 avec résistance 4.7 kΩ vers VCC

- **TDS** :
  - VCC → 3.3V
  - GND → GND
  - AOUT → A0 (entrée analogique)

---

## 🧠 Calcul du TDS avec correction de température

La formule utilisée dans ESPHome est la suivante :

```c++
float voltage = id(tds_raw).state * 3.3;
float compensation_coefficient = 1.0 + 0.02 * (id(water_temp).state - 25.0);
float compensated_voltage = voltage / compensation_coefficient;
float tds = (133.42 * pow(compensated_voltage, 3)
            - 255.86 * pow(compensated_voltage, 2)
            + 857.39 * compensated_voltage) * 0.5;
```

---

## 🧪 Calibration

- 🌊 **Eau osmosée pure** : TDS ~ 0 ppm
- 🐟 **Eau reminéralisée** : 100–200 ppm selon les espèces
- 💡 Astuce : utiliser une solution étalon à 342 ppm pour calibrer précisément

---

## 🏡 Intégration Home Assistant

- Ajout automatique via `ESPHome`
- Possibilité d’automatiser alertes ou actions (chauffage, électrovanne)
- Dashboard Lovelace conseillé : `history-graph`, `gauge`, `entities`

---

## 📷 Aperçu du Dashboard (optionnel)

*Ajoutez ici une capture d'écran de votre interface Home Assistant avec les données TDS & Température.*

---

## 🔐 Sécurité

- 🔒 Accès web protégé (`admin / XXXXXXX`)
- 🔄 OTA avec mot de passe
- 🔑 API chiffrée
--->>> Please change all XXXXXX values
---

## 📄 Licence

Ce projet est open-source sous licence [MIT](LICENSE).

---

## 🙌 Crédits

Projet développé par **Charles Bijon** pour surveiller un aquarium tropical avec eau osmosée.

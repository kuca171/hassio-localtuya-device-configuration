# Integrace Concept OV2220 Perfect Air Smart do Home Assistant přes Localtuya

<p align="center">
<img src="img/concept_dehumidifier_ov2220.PNG" alt="Odvlhčovač" width="20%"/>
</p>
  
## Požadavky

  - PC s windows
  - mobilní telefon s aplikací tuya
  - přístup do https://iot.tuya.com návod na vytvotvoření projektu -> https://www.home-assistant.io/integrations/tuya
  - Nainstalovaná integrace <a href="https://github.com/rospogrigio/localtuya/">localtuya</a> v Home Assistant

## Spárování odvlhčovače s tuya aplikací

**Odeberte odvlhčovač ze všech aplikací, s kterými jste ho spárovali (například concept home)**

**Pro spárování je nutné přepnout odvlhčovač do režimu párování. Odvlhčovač se do režimu párování přepne stisknutím tlačítka režimu ve vypnutém stavu -> začne blikat symbol wifi. **

- v mobilním telefonu otevřít aplikaci Tuya Smart
- dát volbu přidat zařízení (v pravém horním rohu)

<p align="center">
<img src="img/android01.jpg" alt="android1" width="30%"/>
</p>

- v seznamu zařízení najít "Odvlhčovač Wi-fi"

<p align="center">
<img src="img/android02.jpg" alt="android2" width="30%"/>
</p>

- zadejte údaje ke své wifi

<p align="center">
<img src="img/android03.jpg" alt="android3" width="30%"/>
</p>

- následně ze seznamu zařízení vyberat OV2220 a zařízení bude spárováno s Tuya

## Získání device id a local key

- přihlásit se do https://iot.tuya.com zde najít svůj projekt s odvlhčovačem, kde je device id

![alt tuya iot](img/tuya_iot01.PNG)

- zkopírovat device id a přepnout se do API Explorer

![alt tuya iot](img/tuya_iot02.PNG)

- přepnutí do API "General devices management" -> "Get device information"
- vyplnit device ID a enter

![alt tuya iot](img/tuya_iot03.PNG)

- v pravé části okna by měl být podobný výsledek

```json
{
  "result": {
    "active_time": 1675787210,
    "category": "cs",
    "category_name": "Dehumidifier",
    "create_time": 1670774269,
    "gateway_id": "",
    "icon": "smart/product_icon/cs.png",
    "id": "10017508483fda31449a",
    "ip": "85.160.0.131",
    "lat": "49.5883",
    "local_key": "6x3375e2v9d67cb9",
    "lon": "14.1600",
    "model": "OV2220",
    "name": "OV2220",
    "online": true,
    "owner_id": "45828380",
    "product_id": "uag0ftgtowvsxfk8",
    "product_name": "OV2220",
    "sub": false,
    "time_zone": "+01:00",
    "update_time": 1675787217,
    "uuid": "10017508483fda31449a"
  },
  "success": true,
  "t": 1675862725017,
  "tid": "0b97d8d1a7bc11ed9de742b33a3cd862"
}
```
- vykopírovat local_key

## Přidání do Home Assistant

  - otevřít Home Assistant -> Nastavení -> Zařízení
  - najít položku localtuya -> Nastavit

  ![alt localtuya](img/1_localtuya_device.PNG)
 
  - vybrat volbu add a new device

  ![alt konfigurace](img/2_localtuya_configuration.PNG)
  
  - vybrat zařízení ov2220

  ![alt add device](img/01_select_new_device.PNG)
  
## Zdroje

- https://github.com/make-all/tuya-local/issues/306
- https://community.home-assistant.io/t/wip-smart-dehumidifier/417301/3
- https://github.com/make-all/tuya-local/tree/main/custom_components/tuya_local/devices
- https://github.com/make-all/tuya-local/blob/main/custom_components/tuya_local/devices/jjpro_jpd01_dehumidifier.yaml

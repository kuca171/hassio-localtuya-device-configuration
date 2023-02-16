# Integrace Ledvance WiFi zásuvkové lišty s USB do Home Assistant přes Localtuya

<p align="center">
<img src="img/gcpf359708bd62b48f1a47615f4d9787206.jpeg" alt="Zásuvková lišta Ledvance" width="50%"/>
</p>
  
## Požadavky

  - PC s windows
  - Nainstalovaná integrace <a href="https://github.com/rospogrigio/localtuya/">local tuya</a> v Home Assistant

## Získání device id a local key

  - zařízení spárovat s účtem LDV Wifi (aplikace wifi smart+)
  - Instalace pythonu -> z microsoft store, poslední verzi
  - Otevřít příkazovou řádku a nainstalovat request a pycryptodome
  
  ```cmd
  
    pip install requests 
    pip install pycryptodome
  
  ```
  
  - stáhnout a rozbalit https://github.com/FlagX/ha-ledvance-tuya-resync-localkey
  - v příkazové řádce přejít do adresáře s rozbaleným repozitářem
  - v příkazové řádce zadat:

  ```cmd
  
    python print-local-keys.py 
  
  ```

  - vyplnit přihlašovací údaje  do Ledvance
  - program vrátí device name, device id a local key

  ```cmd
  device name:    LDVWFMULTISOCKETEU
  device id:      bf7971d166aca3c37acxe5
  local key:      2ff3c5fa5ad69968
  ```
  
## Přidání do Home Assistant

  - otevřít Home Assistant -> Nastavení -> Zařízení
  - najít položku localtuya -> Nastavit
  
  ![alt localtuya](img/1_localtuya_device.PNG)
 
  - vybrat volbu add a new device

  ![alt konfigurace](img/2_localtuya_configuration.PNG)
  
  - vybrat zařízení dle device id

  ![alt add device](img/3_add_device.PNG)
  
  - nastavení zařízení: zadání názvu zařízení a local key vašeho zařízení, případně zadat ještě scan interval
  
  ![alt configure device](img/4_configure_device.PNG)
  
  - přídání entity zařízení: přidáme entity pro jednotlivé zásuvky, entity budou typu switch
  
  ![alt entity type](img/5_entity_type.PNG)
  
  - nastavení entity: vyberte ID zařízení (pro zásuvku 1 bude ID/DP 1, pro zásuvku 2 = ID/DP =2 , pro zásuvku 3 = ID/DP =3, pro usb zásuvky = ID/DP = 4), název entity, případně defaulní nastavení po inicializaci

  ![alt configure entity](img/6_configure_entity.PNG)
  
  - po přídání každé entity se objeví dotaz na přidání další entity k zařízení. Pro přídání další je nutné odškrtnout volbu "Do not add any more entities" 

  ![alt entity_type](img/7_entity_type.PNG)
  
  - stejným způsobem zadáme i zásuvky 2,3 a usb, pozor po každém zadání odškrtnout volbu "Do not add any more entities". Příklad entity zásuvky 3 :

  ![alt configure_entity3](img/8_configure_entity3.PNG)
  
  - po přidání všech zásuvek, přidáme entity pro proud, napětí a příkon. Nyní budou entity typu sensor, opět vždy po přidání odškrtnout volbu "Do not add any more entities", pokud chcete ještě zadávat další entity

  ![alt 9_entity_type](img/9_entity_type.PNG)
  
  - proud: dle tuya dokumentace ID/DP = 18, jednotka = mA, device class = current

  ![alt current](img/10_current.PNG)

  - příkon: dle tuya dokumentace ID/DP = 19, jednotka= W, device class = power, scaling faktor = 0.1

  ![alt power](img/11_power.PNG)
  
  - napětí: dle tuya dokumentace ID/DP = 20, jednotka= V, device class = voltage, scaling faktor = 0.1

  ![alt power](img/12_voltage.PNG)
  
  - po přídání všech entit necháme volbu zaškrtnutou "Do not add any more entities"

    ![alt 13_entity_type](img/13_entity_type.PNG)
    
## Výsledek v Home Assistant

  - nějak takto by mělo vypadat přidané zařízení
  
  ![alt 14_result](img/14_result.PNG)

# Zdroje
  - https://developer.tuya.com/en/docs/iot/product-standard-function-introduction?id=K9tp15ceh63gr
  - https://community.home-assistant.io/t/ledvance-integration-this-is-how-to-do-it-as-per-08-22/449783
  - https://github.com/rospogrigio/localtuya/
  - https://github.com/FlagX/ha-ledvance-tuya-resync-localkey
 

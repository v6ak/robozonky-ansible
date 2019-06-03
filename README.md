Experiemntální role pro deploy RoboZonky přes Ansible. Zatím šité horkou jehlou.

## Předpoklady

* systemd
* Nainstalovaná Java pro RoboZonky. Buď může být v $PATH, nebo je potřeba nastavit robozonky_java_home v vars/main.yml.

## Konfigurační soubory

Následující soubory je potřeba přidat:

* files/robozonky-notifications.cfg
* files/robozonky-strategy.cfg
* files/robozonky.keystore
* volitelně files/Google/StoredCredential (pro integraci se Stonky)

## Co upravit?

* vars/main.yml (vizte komentáře v souboru)

## Co by to chtělo vylepšit

* Nějaké lepší rozdělení přinejmenším variables, aby to bylo dobře znovupoužitelné a šlo to aktualizovat.

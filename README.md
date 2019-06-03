Experiemntální role pro deploy RoboZonky přes Ansible. Zatím šité horkou jehlou.

## Předpoklady

* systemd
* Nainstalovaná Java pro RoboZonky. Používá se natvrdo ta v $PATH.

## Konfigurační soubory

Následující soubory je potřeba přidat:

* files/robozonky-notifications.cfg
* files/robozonky-strategy.cfg
* files/robozonky.keystore
* volitelně files/Google/StoredCredential (pro integraci se Stonky)

## Co upravit?

* vars/main.yml (vizte komentáře v souboru)

## Co by to chtělo vylepšit

* Podpora volby jiné verze Javy než v $PATH – asi konfigurací JAVA_HOME. Bude asi potřeba na to udělat nějaký wrapper script nebo úprava samotného RoboZonky.
* Nějaké lepší rozdělení přinejmenším variables, aby to bylo dobře znovupoužitelné a šlo to aktualizovat.

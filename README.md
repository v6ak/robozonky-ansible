Experiemntální role pro deploy RoboZonky přes Ansible. Šité už trochu méně horkou jehlou.

## Předpoklady

* systemd
* Nainstalovaná Java pro RoboZonky. Buď může být v $PATH, nebo je potřeba nastavit robozonky_java_home v vars/main.yml.

## Co nastavit?

Budete potřebovat nastavit pár proměnných

```
robozonky_user_create: yes # If you have created the user somewhere else, just say “no”
robozonky_user_name: robozonky # use any system username you want; The user will be created if it does not exist.
#robozonky_user_uid: 12345 # you can pick a specific UID and uncomment this line

robozonky_zonky_email: your-email@for.zonky.cz
robozonky_zonky_auth_code: abC123 # Authentication code from https://app.zonky.cz/api/oauth/authorize?client_id=robozonky&redirect_uri=https://app.zonky.cz/api/oauth/code&response_type=code&scope=SCOPE_APP_BASIC_INFO%20SCOPE_INVESTMENT_READ%20SCOPE_INVESTMENT_WRITE%20SCOPE_RESERVATIONS_READ%20SCOPE_RESERVATIONS_WRITE%20SCOPE_RESERVATIONS_SETTINGS_WRITE%20SCOPE_RESERVATIONS_SETTINGS_READ%20SCOPE_NOTIFICATIONS_READ%20SCOPE_NOTIFICATIONS_WRITE&state=dffdgdfg

robozonky_storage_password: someeeee-pass-word-forr-keystoreeeee # look at the parameter after -p in robozonky.cli
# robozonky_java_home: /usr/lib/jvm/java-11-openjdk/ # You can put path (without trailing “bin/java” of JRE) if the default JRE is not suitable. Remove leading “#” to make it effective.
# robozonky_instance_name: ansiblozonky # you might want a different name and uncomment this line
robozonky_files_path: "{{playbook_dir}}/files/robozonky" # directory where Ansible should look for config files
# robozonky_data_path: # Directory to store data (e.g., authentication tokens) in.

```

Vedle toho můžete nastavit i pár dalších proměnných:


## Konfigurační soubory

Následující soubory je potřeba přidat do adresáře v robozonky_files_path:

* robozonky-notifications.cfg
* robozonky-strategy.cfg

## Jak aktualizovat RoboZonky

Pokud do role nebudete nijak zasahovat, mělo by stačit aktualizovat tuto roli. Nebo – máte-li odvahu – můžete nastavit proměnnou robozonky_version na verzi RoboZonky, pokud se v RoboZonky nic nezměnilo, mělo by to také fungovat. V případě opravných verzí by toto mělo fungovat bez problémů, v případě větších změn to fungovat nemusí.

Stará verze zůstává nainstalovaná se starými konfiguráky atd. Můžete ji smazat ručně.

## Jak může vypadat Playbook

Pokud znáte Ansible, asi můžete toto přeskočit. Jinak se může hodit tato sekce. Zkusíme si vytvořit uživatele „robozonky“ a nasadit to u něj následujícím příkazem:

    ansible-playbook my-server.yml -i hosts

### my-server.yml

```
---
- hosts: my-server
  roles:
    #- {role: 'basic-setup', tags: 'basic-setup'}
    - {role: 'robozonky', tags: 'robozonky'}
  user: my_administration_user_name
  become: yes
  vars:
    robozonky_user_create: yes
    robozonky_user_name: robozonky # use any username you want; The user will be created if it does not exist.
    robozonky_storage_password: someeeee-pass-word-forr-keystoreeeee # look at the parameter after -p in robozonky.cli
    robozonky_files_path: "{{playbook_dir}}/files/robozonky"
```

### hosts

```
[my-group]
12.34.56.78
```

### roles/robozonky

Sem naklonujte tento repozitář. Jde to udělat třeba tímto příkazem:

    mkdir -p roles && git clone https://github.com/v6ak/robozonky-ansible roles/robozonky

### files/robozonky

Sem přijdou soubory robozonky-notifications.cfg a robozonky-strategy.cfg.



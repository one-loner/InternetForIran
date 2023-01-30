Данный документ является переводом проекта иранских активистов Internet for Iran.   
Учитывая всё большее закручивание гаек в Интернете в России, данный проект может быть применим для решения проблемы блокировок свободного доступа в Интернет на территории РФ.   
Оригинал документа находится по [ссылке](https://github.com/InternetForIran/InternetForIran)   
       
================================================================= Перевод на русский =================================================================     
     

# Интернет для Ирана
[![Twitter](https://img.shields.io/twitter/url/https/twitter.com/fold_left.svg?style=social&label=Follow%20%40InternetForIran)](https://twitter.com/InternetForIran)

## Вступление

IИнтернет сильно ограничен в мобильных (3G / 4G) и жилых (ADSL / TD-LTE) сетях, а подключение к VPN и веб-сайтам за пределами Ирана практически невозможно, Tor не работает надежно, поскольку мосты Tor находятся за пределами Ирана и в основном недоступны для человек внутри Ирана. С другой стороны, правительство еще не заблокировало доступ в Интернет на машинах, расположенных в иранских центрах обработки данных, и люди могут легко подключаться к этим веб-сайтам и серверам.

### Чем я могу помочь?

Нам нужны сервера и помощь в их настройке
| Кто я ?                                                                  | Чем я могу помочь?                                              |
| ------------------------------------------------------------------------ | ------------------------------------------------------------ |
| Иранский эмигрант                                                        | Если вы можете, купите сервер в Иране и отправьте нам IP-адрес и учетные данные ssh по электронной почте InternetForIran@proton.me. Мы настроим сервер и отправим вам детали VPN, чтобы поделиться с вашими друзьями и семьей в Иране.|
| Владелец/основатель/руководитель технической компании в Иране            | Вероятно, у вас уже есть серверы в Иране. Используйте этот документ, чтобы преобразовать один из ваших серверов (или новый сервер) для настройки VPN для вашей команды. Попросите свою команду использовать его и поделитесь информацией о VPN и мосте Tor со своей семьей и друзьями. У вас будет реальный бизнес-пример, чтобы оправдать создание VPN-сервера, даже если правительство придет к вам. |
| Разработчик / системный администратор / инженер DevOps в Иране           | **Мы не рекомендуем вам приобретать серверы в иранских дата-центрах для самостоятельной настройки VPN-сервисов. По IP-адресу сервера, которым вы поделитесь с друзьями и семьей, можно легко отследить вас.** <br />Свяжитесь со своими друзьями и родственниками за пределами Ирана и попросите их приобрести сервер в иранском центре обработки данных и сообщите вам подробности. Настройте его, следуя этому руководству, и поделитесь данными для подключения с друзьями и семьей. |
| Кто-то, у кого недавно умер родственник в Иране                          | Прежде всего, соболезнуем вам :( Вы можете помочь, используя удостоверение личности и дебетовую карту вашего умершего члена семьи, чтобы приобрести сервер в одном из иранских центров обработки данных и отправить нам IP-адрес и учетные данные ssh по электронной почте InternetForIran@proton.me. Мы установим сервер и отправить данные VPN обратно вам, чтобы использовать и поделиться с друзьями и семьей.Правительство не сможет арестовать вашего умершего члена семьи, и не сможет доказать, что вы использовали его личность и дебет данные карты для покупки серверов.<br />**Помните, что важно, чтобы вы использовали как их удостоверение личности, так и дебетовую карту для совершения покупки. Если вы используете свою собственную карту или удостоверение личности, правительство сможет вычислить вас.** |
| Обычный человек в Иране                                                  | **Мы не рекомендуем вам приобретать серверы в иранских дата-центрах для самостоятельной настройки VPN-сервисов.По IP-адресу сервера, которым вы поделитесь с друзьями и семьей, Вас могут легко вычислить**<br /> Отправьте этот документ своим техническим друзьям. Попросите членов вашей семьи за пределами Ирана купить сервер. Делайте ретвиты, лайкайте наши твиты и распространяйте информацию. |
| VPN-провайдер за пределами Ирана                                         | Нам нужны VPN за пределами Ирана (помогает нам заменить машину A на VPN). Пожалуйста, пришлите нам детали VPN-подключения (желательно без ограничений на использование данных, OpenVPN и OpenConnect работают лучше всего) по электронной почте InternetForIran@proton.me. |
| Хакерская группировка                                                    | Если вы скомпрометировали сервер в Иране и получили к нему доступ по ssh, используйте это руководство, чтобы настроить VPN-сервер и поделиться подробностями с нами и вашими подписчиками. |
| Разработчик / системный администратор / инженер DevOps где-бы то ни было | У нас есть сообщения о том, что V2Ray VMess и ShadowSocks работают внутри Ирана даже тогда, когда большинство других инструментов и протоколов не работают. Нам не удалось надежно развернуть и протестировать это (есть много вариантов конфигурации, и неясно, какие методы работают). Пожалуйста, создайте вопрос или отправьте PR, если вы знаете, как это работает и как его развернуть. <br />Нам также нужна ваша помощь в улучшении этого документа: Вы видите потенциальную проблему безопасности? Можете ли вы помочь упростить процесс развертывания или автоматизировать установку с помощью контейнеров докеров и сценариев оболочки? Дополнения приветствуются :)|

### Обзор

Чтобы обойти ограничения, вам нужно иметь два сервера:

- **Машина A**: машина за пределами Ирана (например, в DigitalOcean или других провайдерах). В этом документе мы будем использовать **100.0.0.0** в качестве IP-адреса этой машины. **В этом документе предполагается, что ОС, работающая на машине А  Ubuntu Server 20.04.**
- **Машина B**: машина внутри иранского центра обработки данных с публичным адресом. В этом документе мы будем использовать **200.0.0.0** в качестве IP-адреса этой машины. **В этом документе предполагается, что ОС, работающая на компьютере B  Ubuntu Server 20.04.** 

Мы собираемся установить VPN-сервер на **машине A** (за пределами Ирана) и подключиться к этому VPN-серверу с **машины B** (внутри иранского центра обработки данных). Затем мы можем установить VPN-сервер и мост Tor на **машине B** и поделиться информацией о подключении с людьми, которых мы знаем.



## 1. Вопросы безопасности

Следуя этому документу и настроив эти машины, вам нужно будет поделиться IP-адресом машины B с другими людьми, чтобы они могли подключиться к настроенному вами мосту VPN или Tor. Правительство может связать этот IP-адрес с вашей личностью через поставщика, у которого вы приобрели компьютер B.

Например, вы покупаете машину B в Afranet и сообщаете своим друзьям детали VPN-подключения, включая IP-адрес 200.0.0.0. Одного из ваших друзей, у которого есть эта информация в телефоне, арестовывают, и силовики находят этот IP-адрес в его телефоне, они могут легко проверить через Афрэнет и узнать личность человека, купившего у них эту машину, и прийти за вами.

Насколько это возможно, постарайтесь уговорить одного из ваших друзей за пределами Ирана (или использовать удостоверение личности и дебетовую карту недавно заболевшего человека) для покупки машины B, чтобы даже в случае утечки личности владельца машины никого могли бы арестовать.

Кроме того, не забудьте отключить журналы доступа на машине B, как только вы получите к ней доступ (иначе ваш собственный IP-адрес будет зарегистрирован на машине B, и если машина будет скомпрометирована, ее можно будет отследить до вас).
Мы объясним, как это сделать позже.

## Конфигурация машины А
> Мы рекомендуем вам купить и использовать для этого новую машину, на которой больше ничего нет. Но это можно сделать и на существующей машине. Мы используем Docker для настройки VPN-сервера, и это не должно иметь побочных эффектов для остальной части вашей системы.

Это сервер, который находится за пределами Ирана. У вас могут возникнуть проблемы с подключением к этому серверу напрямую, используя подключение к домашней или мобильной сети. Если это так, вы можете сначала подключиться к серверу B по ssh, а оттуда — к серверу A.

```bash
you@localhost:~$ ssh root@200.0.0.0
Welcome to Ubuntu 20.04.1 LTS (GNU/Linux 5.4.0-48-generic x86_64)
root@200.0.0.0:~# ssh root@100.0.0.0
Welcome to Ubuntu 20.04.1 LTS (GNU/Linux 5.4.0-48-generic x86_64)
root@100.0.0.0:~# 
```
### 2.1 Установите и настройте сервер OpenConnect.

Разверните и запустите ocserv с помощью Docker. OCserv будет выступать в роли сервера OpenConnect:

```bash
root@100.0.0.0:~# mkdir ocserv
root@100.0.0.0:~# cd ocserv
root@100.0.0.0:~/ocserv# wget -qO- https://pastebin.com/raw/WZymtWi2 > ocserv.conf
root@100.0.0.0:~/ocserv# touch ocpasswd
root@100.0.0.0:~/ocserv# cd 
root@100.0.0.0:~# docker run --name ocserv --privileged -e NO_TEST_USER=1 -v $PWD/ocserv/:/etc/ocserv/ -p 8443:443 -p 8443:443/udp -d tommylau/ocserv
```

Это должно запустить контейнер докеров, на котором работает сервер OpenConnect. Теперь вам нужно создать нового пользователя для подключения к этому серверу - замените `USERNAME` на любое имя пользователя, которое вы хотите:

```bash
root@100.0.0.0:~# docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -g "Route,All" USERNAME
Enter password: 
Re-enter password:
```

> Он не покажет пароль, который вы вводите.

Конфигурация машины B

> Используйте новую машину для этой детали. Изменения, которые мы вносим в маршруты и VPN-подключение, которое мы инициируем с машины B, вызовут сбои в работе другого программного обеспечения, которое вы можете запускать на этой машине.

Подключиться к машине B: Конфигурация машины B

> Используйте новую машину для этой детали. Изменения, которые мы вносим в маршруты и VPN-подключение, которое мы инициируем с машины B, вызовут сбои в работе другого программного обеспечения, которое вы можете запускать на этой машине.

Подключиться к машине B:

```bash
you@localhost:~$ ssh root@200.0.0.0
Welcome to Ubuntu 20.04.1 LTS (GNU/Linux 5.4.0-48-generic x86_64)
root@200.0.0.0:~#
```

### 3.1 Отключить журналы доступа

Изменить `/etc/ssh/sshd_config`:

```bash
nano /etc/ssh/sshd_config
```

 далее найти `# LogLevel INFO`. Изменить на:

```
LogLevel QUIET
```

Перезагрузить службы `ssh` и `sshd` :

```bash
root@200.0.0.0:~# systemctl reload ssh 
root@200.0.0.0:~# systemctl reload sshd
```

Отключиться и подключиться к серверу заново:

```bash
root@200.0.0.0:~# exit
Connection to YOUR_LOCAL_IP closed.
you@localhost:~$ ssh root@200.0.0.0
```

После входа очистите логи:

```bash
root@200.0.0.0:~# echo > /var/log/auth.log
root@200.0.0.0:~# rm /var/log/auth.log.*
```

выйдите из системы и войдите снова, проверьте и убедитесь, что `sshd` не регистрирует ваш IP-адрес `/var/log/auth.log`:

```bash
root@200.0.0.0:~# tail /var/log/auth.log
```

Вы должны увидеть следующие:

```
localhost systemd-logind[706]: Session 12 logged out. Waiting for processes to exit.
```

но без IP-адресов.

> Обратите внимание, что это не гарантирует, что правительство не сможет найти ваш локальный IP-адрес. После того, как все настроено, вы должны сначала активировать VPN-подключение, затем ssh к машине A и ssh к машине B с машины A.

### 3.2 Изменить sources.list

Некоторые провайдеры (например, Afranet) развертывают машины со своей собственной версией sources.list, из-за чего Ubuntu загружает пакеты из зеркал репозитория провайдеров. Чтобы повысить безопасность, нам нужно изменить его обратно на официальные зеркала репозитория Ubuntu:

```bash
root@200.0.0.0:~# nano /etc/apt/sources.list
```

Убедитесь, что все строчки начинаются с

```
deb http://archive.ubuntu.com/ubuntu
```

или 

```
deb http://archive.ubuntu.com/ubuntu
```

Если вы увидите следующие:

```
deb http://ubuntu.mirror.afranet.com/ubuntu
```

измените «ubuntu.mirror.afranet.com» в этих строках на «archive.ubuntu.com».

Затем обновите репозитории:

```bash
root@200.0.0.0:~# apt update
```

### 3.3 Настройка маршрутов

Чтобы поддерживать ssh-соединение из вашей локальной сети с машиной A после ее подключения к VPN-серверу на машине B, вам необходимо добавить прямые маршруты к иранским IP-адресам на машине A. Для этого мы создадим сценарий bash и службу systemd. чтобы убедиться, что он выполняется при загрузке.

Сначала создайте сценарий bash и переместите его в `/usr/local/sbin`:

```bash
root@200.0.0.0:~# wget -qO- https://pastebin.com/raw/isEgF5tv > iran_ip_range.json
root@200.0.0.0:~# GATEWAY=`ip route show | grep 'default via' | cut -d' ' -f3`
root@200.0.0.0:~# apt install jq
root@200.0.0.0:~# for range in $(jq .[] iran_ip_range.json | sed 's/"//g' | xargs); do   echo "ip route add $range via $GATEWAY" >> /usr/local/sbin/add-routes.sh ; done;
root@200.0.0.0:~# chmod +x /usr/local/sbin/add-routes.sh
```

Замените `DEFAULT_GATEWAY_IP` на IP-адрес вашего шлюза.

Теперь создайте службу systemd:

```bash
root@200.0.0.0:~# nano /etc/systemd/system/add-routes.service
```

Вставьте в этот файл следующее и сохраните:

```ini
[Unit]
Description=Router configuration service
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=no
RestartSec=3600min
User=root
ExecStart=/bin/bash /usr/local/sbin/add-routes.sh

[Install]
WantedBy=multi-user.target
```

Включите службу add-routes и запустите ее:

```bash
root@200.0.0.0:~# systemctl daemon-reload
root@200.0.0.0:~# systemctl enable add-routes.service
root@200.0.0.0:~# systemctl start add-routes.service
```

### 3.4 Установка и настройка клиента OpenConnect

OpenConnect — это программное обеспечение VPN, которое использует SSL для подключения и передачи сетевых данных. Вам необходимо установить и настроить клиент OpenConnect для подключения к серверу OpenConnect, который вы ранее установили на компьютере A:

```bash
root@200.0.0.0:~# apt install openconnect
```

Откройте `screen`, чтобы иметь возможность запустить клиент OpenConnect VPN и оставить его работающим после выхода из машины B:

```bash
root@200.0.0.0:~# screen
```

Внутри экрана запустите клиент OpenConnect:

```bash
root@200.0.0.0:~# openconnect --user test 100.0.0.0:8443 

POST https://100.0.0.0:8443/
Connected to 100.0.0.0:8443
SSL negotiation with 100.0.0.0
Server certificate verify failed: signer not found

Certificate from VPN server "100.0.0.0" failed verification.
Reason: signer not found
To trust this server in future, perhaps add this to your command line:
    --servercert pin-sha256:xxxxxxxxxxxxxxxxxxxxx
Enter 'yes' to accept, 'no' to abort; anything else to view: yes 
Connected to HTTPS on 100.0.0.0
XML POST enabled
Please enter your username.
Group: [Route[Exclude CN]|All Proxy|All]:All
POST https://100.0.0.0:8443/auth
XML POST enabled
Please enter your username.
POST https://100.0.0.0:8443/auth
Please enter your password.
Password:
POST https://100.0.0.0:8443/auth
Got CONNECT response: HTTP/1.1 200 CONNECTED
CSTP connected. DPD 90, Keepalive 32400
Connected as 192.168.xx.xx, using SSL + LZ4, with DTLS + LZ4 in progress
DTLS handshake failed: Error in the push function.
(Is a firewall preventing you from sending UDP packets?)
```

Теперь вы подключены к VPN-серверу на машине A. Чтобы закрыть экран, нажмите `Ctrl+A+D`. Вы можете возобновить подключение к экрану (чтобы увидеть выходные данные VPN-подключения или остановить подключение, нажав `Ctrl + C`), выполнив следующую команду:

```bash
root@200.0.0.0:~# screen -r
```

### 3.5 Установка и настройка сервера OpenConnect

Это можно сделать, используя тот же процесс, что и на машине А:

```bash
root@200.0.0.0:~# mkdir ocserv
root@200.0.0.0:~# cd ocserv
root@200.0.0.0:~/ocserv# wget -qO- https://pastebin.com/raw/WZymtWi2 > ocserv.conf
root@200.0.0.0:~/ocserv# touch ocpasswd
root@200.0.0.0:~/ocserv# cd 
root@200.0.0.0:~# docker run --name ocserv --privileged -e NO_TEST_USER=1 -v $PWD/ocserv/:/etc/ocserv/ -p 8443:443 -p 8443:443/udp -d tommylau/ocserv
```

Это должно запустить контейнер докеров, на котором работает сервер OpenConnect. Теперь вам нужно создать нового пользователя для подключения к этому серверу - замените `USERNAME` на любое имя пользователя, которое вы хотите:

```bash
root@200.0.0.0:~# docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -g "Route,All" USERNAME
Enter password: 
Re-enter password:
```

> Он не покажет пароль, который вы вводите, не запутайтесь.

### 3.6 Установка и настройка серверов Wireguard и IPSec VPN

OpenConnect обычно имеет проблемы с подключением к продуктам Apple. Вы можете использовать [Algo](https://github.com/trailofbits/algo) для установки Wireguard и IPSec VPN на машине B, чтобы продукты Apple также могли подключаться. Следуйте инструкциям на https://github.com/trailofbits/algo и выберите режим локальной установки, чтобы установить его локально на компьютере B. Дополнительная информация здесь: https://github.com/trailofbits/algo/blob/master/docs/ развертывание-в-ubuntu.md

Вы можете загрузить и использовать этот файл как `config.cfg` для установки Algo: https://pastebin.com/raw/iARF0fGL.
Этот файл конфигурации включает 100 пользователей по умолчанию и включает WireGuard и IPSec.

### 3.7 Тор

Соединения Tor нестабильны. Есть два метода заставить его работать, и каждый метод может работать в разное время. Вы можете сделать и то, и другое и проверить их соединение, чтобы увидеть, какое из них работает для вас лучше всего.

#### 3.7.1 Метод 1: Установка и настройка моста Tor внутри Ирана

Установка моста Tor поможет людям подключаться к Tor через машину B, которая легко доступна из Ирана. Сначала убедитесь, что VPN подключен (шаг 3.4). Затем установите Tor из репозиториев Ubuntu, чтобы установить и запустить начальное подключение Tor, затем добавьте официальный репозиторий Tor и переустановите/обновите Tor из официального репозитория.

```bash
root@200.0.0.0:~# apt install tor 
root@200.0.0.0:~# apt install apt-transport-tor
root@200.0.0.0:~# CODENAME=`lsb_release -c | grep Codename | cut -d: -f2 | tr -d [:space:] `
root@200.0.0.0:~# ARCH=`dpkg --print-architecture`
root@200.0.0.0:~# echo "deb [arch=$ARCH signed-by=/usr/share/keyrings/tor-archive-keyring.gpg] tor://apow7mjfryruh65chtdydfmqfpj5btws7nbocgtaovhvezgccyjazpqd.onion/torproject.org $CODENAME main" > /etc/apt/sources.list.d/tor.list
root@200.0.0.0:~# apt update
root@200.0.0.0:~# apt install tor obfs4proxy
```

Теперь очистите `/etc/tor/torrc` и откройте его в редакторе:

```bash
root@200.0.0.0:~# echo > /etc/tor/torrc
root@200.0.0.0:~# nano /etc/tor/torrc
```

и вставьте это в файл, заменив `200.0.0.0` реальным IP-адресом машины B, а YOU@EMAIL.COM – адресом электронной почты, к которому у вас есть доступ, но вас нельзя отследить:

```
BridgeRelay 1

# Replace "TODO1" with a Tor port of your choice.
# This port must be externally reachable.
# Avoid port 9001 because it's commonly associated with Tor and censors may be scanning the Internet for this port.
ORPort 200.0.0.0:8888

ServerTransportPlugin obfs4 exec /usr/bin/obfs4proxy

# This port must be externally reachable and must be different from the one specified for ORPort.
# Avoid port 9001 because it's commonly associated with Tor and censors may be scanning the Internet for this port.
ServerTransportListenAddr obfs4 0.0.0.0:9888

# Local communication port between Tor and obfs4.  Always set this to "auto".
# "Ext" means "extended", not "external".  Don't try to set a specific port number, nor listen on 0.0.0.0.
ExtORPort auto

# Replace "<address@email.com>" with your email address so we can contact you if there are problems with your bridge.
# This is optional but encouraged.
ContactInfo YOU@EMAIL.COM

```

Перезапустите Tor и получите параметры моста:

```bash
root@200.0.0.0:~# systemctl restart tor
root@200.0.0.0:~# cat /var/lib/tor/pt_state/obfs4_bridgeline.txt 
# obfs4 torrc client bridge line
#
# This file is an automatically generated bridge line based on
# the current obfs4proxy configuration.  EDITING IT WILL HAVE
# NO EFFECT.
#
# Before distributing this Bridge, edit the placeholder fields
# to contain the actual values:
#  <IP ADDRESS>  - The public IP address of your obfs4 bridge.
#  <PORT>        - The TCP/IP port of your obfs4 bridge.
#  <FINGERPRINT> - The bridge's fingerprint.

Bridge obfs4 <IP ADDRESS>:<PORT> <FINGERPRINT> cert=yyyyyyyy iat-mode=0
```

Скопируйте «Bridge obfs4 <IP-АДРЕС>:<ПОРТ> <FINGERPRINT> cert=xxxxxxxx iat-mode=0» и замените «<IP-АДРЕС» на «200.0.0.0» (IP-адрес машины B), замените «<ПОРТ>». порт, указанный для `ServerTransportListenAddr` в `/etc/tor/torrc` (по умолчанию 9888), и `<FINGERPRINT>` с выводом этой команды:

```bash
root@200.0.0.0:~# cat /var/lib/tor/fingerprint
Unnamed xxxxxxxx
```

Параметры моста должна выглядеть так:

```
Bridge obfs4 200.0.0.0:9888 Unnamed xxxxxxxx cert=yyyyyyyy iat-mode=0
```



> В настоящее время Tor не может подтвердить достижимость моста, и вы увидите «Вашему серверу не удалось подтвердить достижимость для своих портов OR» в «/var/log/syslog». Но вы можете подключиться к своему мосту, указав собственный мост в Orbot или Tor Browser.

#### 3.7.2 Метод 2: прокси-трафик Tor из Ирана на мост за пределами Ирана

Этот метод был разработан [@meskio](https://github.com/meskio) и первоначально опубликован [здесь](https://github.com/net4people/bbs/issues/127). Мы просто меняем словарь, чтобы он соответствовал остальной части этого документа.

Во-первых, вам нужно установить мост на машине А (за пределами Ирана). Мы сделаем это с помощью Docker — установите его, если вы еще этого не сделали, следуя инструкциям по ссылке: https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository

```bash
root@100.0.0.0:~# mkdir bridge
root@100.0.0.0:~# cd bridge
root@100.0.0.0:~/bridge# wget https://gitlab.torproject.org/tpo/anti-censorship/docker-obfs4-bridge/-/raw/main/docker-compose.yml
```

Отредактируйте `bridge/.env` со следующим содержимым, заменив `you@email.com` на адрес электронной почты, к которому у вас есть доступ, но который не может быть отслежен до вас:

```ini
# Set required variables
OR_PORT=3344
PT_PORT=3355
EMAIL=your@email.com

# If you want, you could change the nickname of your bridge
#NICKNAME=DockerObfs4Bridge

# Configure the bridge so it will not be distributed by bridgedb:
OBFS4_ENABLE_ADDITIONAL_VARIABLES=1
OBFS4V_BridgeDistribution=none
```

Запустите мост:

```bash
root@100.0.0.0:~/bridge# docker compose up -d
```

Получите параметры моста:

```bash
root@100.0.0.0:~/bridge# docker exec bridge-obfs4-bridge-1 get-bridge-line
obfs4 100.0.0.0:3355 AAABBBBCCCDDDD cert=abcdx iat-mode=0
```

Затем на машине B (внутри Ирана) у вас есть два варианта перенаправления трафика Tor на ваш мост на машине A:

1. Использование переадресации портов SSH
2. Использование kcptun

##### Использование переадресации портов SSH

```bash
root@200.0.0.0:~# ssh -L 4457:127.0.0.1:4457 100.0.0.0:3355
```

##### Использование kcptun

kcptun — это прокси-сервер расширения сети, который туннелирует потоковый трафик по транспортному протоколу UDP.

Выполните следующие команды на машине А:

```bash
root@100.0.0.0~# mkdir kcptun
root@100.0.0.0~# cd kcptun
root@100.0.0.0~/kcptun# wget https://github.com/xtaci/kcptun/releases/download/v20220628/kcptun-linux-amd64-20220628.tar.gz
root@100.0.0.0~/kcptun# server_linux_amd64 -t "127.0.0.1:3355" -l "0.0.0.0:7923" -mtu 1400 --nocomp -sndwnd 16384 --rcvwnd 16384 --datashard 0 --parityshard 0 --crypt aes --smuxver 2 --key "MY_PRE_SHARED_KEY"
```

Обязательно замените MY_PRE_SHARED_KEY в параметре --key на случайно сгенерированную строку и запишите ее. Нам понадобится это значение через минуту.

а затем на машине B:

```bash
root@200.0.0.0~# mkdir kcptun
root@200.0.0.0~# cd kcptun
root@200.0.0.0~/kcptun# wget https://github.com/xtaci/kcptun/releases/download/v20220628/kcptun-linux-amd64-20220628.tar.gz
root@200.0.0.0~/kcptun# client_linux_amd64 -l "0.0.0.0:3355" -r "100.0.0.0:7923" -mtu 1400 --nocomp -sndwnd 16384 --rcvwnd 16384 --datashard 0 --parityshard 0 --crypt aes --smuxver 2 --key "MY_PRE_SHARED_KEY"
```

Замените MY_PRE_SHARED_KEY той же строкой, что и на предыдущем шаге. Также измените «100.0.0.0» на IP-адрес машины A.

### 3.8 Настройка автономного прокси-сервера Snowflake

Вы также можете настроить автономный прокси-сервер Snowflake на машине B, чтобы помочь пользователям, подвергшимся цензуре, подключаться к сети Tor.

Версия docker-compose в Ubuntu 20.04 немного устарела, вам нужно сначала добавить официальный реестр докеров и установить докер оттуда: https://docs.docker.com/engine/install/ubuntu/#set-up-the -хранилище

После завершения установки докера запустите контейнер:

```bash
root@200.0.0.0:~# mkdir snowflake
root@200.0.0.0:~# cd snowflake
root@200.0.0.0:~# wget https://gitlab.torproject.org/tpo/anti-censorship/docker-snowflake-proxy/-/raw/main/docker-compose.yml
root@200.0.0.0:~# docker compose up -d
```

Ваш прокси-сервер Snowflake теперь запущен и работает, и каждый час будет выводить некоторую статистику использования в журналах докеров (первый вывод появится через час после запуска docker контейнера):

```
root@200.0.0.0:~# docker compose logs snowflake-proxy
```

## 4. Подключение к VPN и Tor с ваших локальных устройств

### 4.1 OpenConnect

Вам необходимо установить приложение OpenConnect на свои устройства (Android, Windows и Linux), чтобы подключиться к VPN.

После установки используйте «200.0.0.0:8443» в качестве хоста, а также имя пользователя и пароль, созданные на шаге 2.6.

> Каждая учетная запись OpenConnect VPN может использоваться несколькими пользователями одновременно. Нет необходимости создавать несколько профилей пользователей, если вы хотите, чтобы VPN использовали несколько человек одновременно.

### 4.2 Wireguard и IPSec

Algo сохраняет файлы конфигурации профиля подключения в `/path/to/algo/configs/200.0.0.0/`. Сожмите и скопируйте эту папку на свой локальный компьютер и поделитесь ими с семьей и друзьями. Дополнительная информация здесь: https://github.com/trailofbits/algo#configure-the-vpn-clients.

> Каждый профиль конфигурации Wireguard и IPSec (пользователь) можно использовать одновременно только на одном устройстве. Если вы хотите одновременно подключиться к ноутбуку и мобильному телефону, используйте два отдельных профиля конфигурации. Использование одного профиля для подключения с нескольких устройств вызывает проблемы с подключением.

### 4.3 Тор

#### 4.3.1 Мост внутри Ирана

> Это для использования моста, созданного в разделе 3.7.1

В Orbot или Tor Browser включите «Использовать мосты» и выберите опцию «Пользовательские мосты», а затем введите линию моста, которую вы построили в разделе 3.7.1, в разделе «Вставить мосты». Теперь вы сможете подключиться и использовать Tor за считанные секунды.

#### 4.3.2 Мост за пределами Ирана с прокси-сервером внутри Ирана

> Это для использования моста, созданного в разделе 3.7.2

распределите мост, который вы получили в разделе 3.7.2, заменив IP-адрес на адрес машины B (200.0.0.0):

```
obfs4 200.0.0.0:3355 AAABBBBCCCDDDD сертификат = abcdx iat-mode = 0
```



================================================================= Оригинал на английском =================================================================     
       
# Internet For Iran
[![Twitter](https://img.shields.io/twitter/url/https/twitter.com/fold_left.svg?style=social&label=Follow%20%40InternetForIran)](https://twitter.com/InternetForIran)

## Introduction

Internet is heavily restricted on mobile (3G/4G) and residential (ADSL/TD-LTE) networks and connecting to VPNs and websites outside Iran is close to impossible, Tor is not working reliably as the Tor bridges are outside Iran and mostly inaccessible to people inside Iran. On the other hand, the government has not yet blocked the Internet access on machines located inside Iranian data centers, and people can easily connect to these websites and servers.

### How can I help?

We need servers and we need help setting those servers up.

| Who am I?                                                | How can I help?                                              |
| -------------------------------------------------------- | ------------------------------------------------------------ |
| Iranian expat                                            | If you can, purchase a server inside Iran and send us the IP address and ssh credentials by emailing InternetForIran@proton.me. We will set up the server and send the VPN details back to you to share with your friends and family inside Iran. |
| Tech company owner/founder/C-level exec inside Iran      | You probably already have servers inside Iran. Use this document to convert one of your servers (or a new server) to set up a VPN for your team. Ask your team to use it and share the VPN details and the Tor bridge with their family and friends. You'll have a real business usecase to justify creating the VPN server even if the government comes to your door. |
| Developer / Sys Admin / DevOps engineer inside Iran      | **We do not recommend you purchasing servers from Iranian data centers for setting up VPN services  yourself. The server IP address which you will share with your friends and family can be easily traced back to your identity.** <br />Contact your friends and family outside Iran and ask them to purchase a server from an Iranian datacenter and give you the details. Set it up by following this guide and share the details with your friends and family. |
| Someone who has a recently deceased relative inside Iran | First of all, sorry for your loss. :( One way you can help is to use the identity and debit card of your deceased family member to purchase a server in one of the Iranian datacenters and send us the IP address and ssh credentials by emailing InternetForIran@proton.me. We will set up the server and send the VPN details back to you to use and share with your friends and family. The government won't be able to arrest your deceased family member, and won't be able to prove that you used their identity and debit card information to purchase the servers.<br />**Remember, it is important that you use both their identity AND debit card to make the purchase, if you use your own card or identity, the government will be able to trace it back to you.** |
| Regular person in Iran                                   | **We do not recommend you purchasing servers from Iranian data centers for setting up VPN services  yourself. The server IP address which you will share with your friends and family can be easily traced back to your identity.**<br /> Send this document to your technical friends. Ask your family members outside Iran to purchase server. Retweet and like our tweets and get the word out. |
| VPN provider outside Iran                                | We need VPNs outside Iran (helps us replace Machine A below with a VPN). Please send us VPN connection details (preferably without data usage limits, OpenVPN and OpenConnect work best) by emailing InternetForIran@proton.me. |
| Hacker group                                             | If you compromise a server inside Iran and gain ssh access to, use this guide to set up a VPN server on and share the details with us and your followers. |
| Developer / Sys Admin / DevOps engineer anywhere         | We have reports that V2Ray VMess and ShadowSocks are working inside Iran even at times when most other tools and protocols don't. We haven't been able to reliably deploy and test this (there are many configuration options and it's not clear which methods are working). Please create an issue or send a PR if you know how it works and how to deploy it. <br />We also need your help with improving this document: Do you see a potential security issue? Can you help make the deployment process easier or automate the installation through the use of docker containers and shell scripts? Contributions are welcome :) |

### Overview

To get around the restrictions, you need to have two servers:

- **Machine A**: a machine outside Iran (e.g. on DigitalOcean or other providers). We’ll use **100.0.0.0** as the IP address of this machine througout this document. **This document assumes the OS running on Machine A is  Ubuntu Server 20.04.**
- **Machine B**: a machine inside an Iranian datacenter with a public address. We’ll use **200.0.0.0** as the IP address of this machine throughout this document. **This document assumes the OS running on Machine B is  Ubuntu Server 20.04.** 

We're going to install a VPN server on **Machine A** (outside Iran) and connect to this VPN server from **Machine B** (inside an Iranian datacenter). Then we can install a VPN server and a Tor bridge on **Machine B**, and share the connection details with people we know.



## 1. Security Considerations

By following this document and setting up these machines, you will need to share the IP address of Machine B with other people in order for them to be able to connect to the VPN or Tor bridge that you set up. The government can connect this IP address with your identity through the provider that you purchased Machine B from.

For example, you buy Machine B from Afranet, and share the VPN connection details with your friends which includes the IP address 200.0.0.0. One of your friends who has this information on his phone gets arrested and the security forces find this IP address on his phone, they can easily check with Afranet and find out the identity of the person who purchased this machine from them and come after you.

As much as possible, try to get one of your friends outside Iran (or a use the identity and debit card of a recently diseased person) to purchase Machine B so that even if the identity of the owner of the machine is leaked, no one can be arrested.

Also, make sure to disable access logs on Machine B as soon as you get access to it (otherwise your own IP address will be logged on the Machine B, and if the machine is compromised it can be traced back to you).
We'll explain how to do this later.

## 2. Machine A Configuration
> We recommend that you buy and use a new machine for doing this with nothing else on it. But it can be done on an existing machine as well. We are using Docker to set up the VPN server and it shouldn't have side effects on the rest of your system.

This is the server that is outside Iran. You might have issue connecting to this server directly using your residential or mobile network connections. If that’s the case, you can first ssh into Server B and then ssh into Server A from there.

```bash
you@localhost:~$ ssh root@200.0.0.0
Welcome to Ubuntu 20.04.1 LTS (GNU/Linux 5.4.0-48-generic x86_64)
root@200.0.0.0:~# ssh root@100.0.0.0
Welcome to Ubuntu 20.04.1 LTS (GNU/Linux 5.4.0-48-generic x86_64)
root@100.0.0.0:~# 
```
### 2.1 Install and configure the OpenConnect server

Deploy and run ocserv using Docker. Ocserv will act as the OpenConnect server:

```bash
root@100.0.0.0:~# mkdir ocserv
root@100.0.0.0:~# cd ocserv
root@100.0.0.0:~/ocserv# wget -qO- https://pastebin.com/raw/WZymtWi2 > ocserv.conf
root@100.0.0.0:~/ocserv# touch ocpasswd
root@100.0.0.0:~/ocserv# cd 
root@100.0.0.0:~# docker run --name ocserv --privileged -e NO_TEST_USER=1 -v $PWD/ocserv/:/etc/ocserv/ -p 8443:443 -p 8443:443/udp -d tommylau/ocserv
```

This should start the docker container running the OpenConnect server. Now you need to create a new user for connecting this this server - replace `USERNAME` with whatever username you want:

```bash
root@100.0.0.0:~# docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -g "Route,All" USERNAME
Enter password: 
Re-enter password:
```

> It won't show the password you're typing, don't get confused.

## 3. Machine B Configuration

> Use a brand new machine for this part. The changes we make  to the routes and the VPN connection we initiate from Machine B will cause disruptions for other software you might be running on this machine.

Connect to Machine B:

```bash
you@localhost:~$ ssh root@200.0.0.0
Welcome to Ubuntu 20.04.1 LTS (GNU/Linux 5.4.0-48-generic x86_64)
root@200.0.0.0:~#
```

### 3.1 Disable access logs

Edit `/etc/ssh/sshd_config`:

```bash
nano /etc/ssh/sshd_config
```

 and find the `# LogLevel INFO`. Change it to:

```
LogLevel QUIET
```

Reload `ssh` and `sshd` services:

```bash
root@200.0.0.0:~# systemctl reload ssh 
root@200.0.0.0:~# systemctl reload sshd
```

Logout and ssh into the server again.

```bash
root@200.0.0.0:~# exit
Connection to YOUR_LOCAL_IP closed.
you@localhost:~$ ssh root@200.0.0.0
```

After logging in, clear out the existing access logs:

```bash
root@200.0.0.0:~# echo > /var/log/auth.log
root@200.0.0.0:~# rm /var/log/auth.log.*
```

logout and log back in again, check and make sure `sshd` is not logging your IP in `/var/log/auth.log`:

```bash
root@200.0.0.0:~# tail /var/log/auth.log
```

You should see entries like

```
localhost systemd-logind[706]: Session 12 logged out. Waiting for processes to exit.
```

but no IP addresses.

> Please note that this does not guarantee that the government cannot find your local IP address. Once everything is set up, you should first activate your VPN connection, then ssh into Machine A and ssh into Machine B from Machine A.

### 3.2 Change sources.list

Some providers (such as Afranet) deploy the machines with their own version of sources.list which causes Ubuntu to download packages from providers' repository mirrors. To increase security, we need to change it back to the official Ubuntu repository mirrors:

```bash
root@200.0.0.0:~# nano /etc/apt/sources.list
```

Make sure all lines start with

```
deb http://archive.ubuntu.com/ubuntu
```

or 

```
deb http://archive.ubuntu.com/ubuntu
```

If you see lines like 

```
deb http://ubuntu.mirror.afranet.com/ubuntu
```

change `ubuntu.mirror.afranet.com` on those lines to `archive.ubuntu.com` and you should be good.

Then update the apt repositories:

```bash
root@200.0.0.0:~# apt update
```

### 3.3 Configure routes

To maintain ssh connection from your local network to Machine A after connecting it to the VPN server on Machine B, you need to add direct routes to Iranian IP addresses on Machine A. To do that we'll create a bash script and a systemd service to make sure that it's executed on boot.

First create the bash script and move it to `/usr/local/sbin`:

```bash
root@200.0.0.0:~# wget -qO- https://pastebin.com/raw/isEgF5tv > iran_ip_range.json
root@200.0.0.0:~# GATEWAY=`ip route show | grep 'default via' | cut -d' ' -f3`
root@200.0.0.0:~# apt install jq
root@200.0.0.0:~# for range in $(jq .[] iran_ip_range.json | sed 's/"//g' | xargs); do   echo "ip route add $range via $GATEWAY" >> /usr/local/sbin/add-routes.sh ; done;
root@200.0.0.0:~# chmod +x /usr/local/sbin/add-routes.sh
```

Replace `DEFAULT_GATEWAY_IP` with your gateway ip.

Now create the systemd service:

```bash
root@200.0.0.0:~# nano /etc/systemd/system/add-routes.service
```

Paste the following in this file and save:

```ini
[Unit]
Description=Router configuration service
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=no
RestartSec=3600min
User=root
ExecStart=/bin/bash /usr/local/sbin/add-routes.sh

[Install]
WantedBy=multi-user.target
```

Enable the `add-routes` service and start it:

```bash
root@200.0.0.0:~# systemctl daemon-reload
root@200.0.0.0:~# systemctl enable add-routes.service
root@200.0.0.0:~# systemctl start add-routes.service
```

### 3.4 Install and configure the OpenConnect client

OpenConnect is a VPN software that uses SSL for connecting and transferring network data. You need to install and configure OpenConnect client to connect to the OpenConnect server that you previously installed on Machine A:

```bash
root@200.0.0.0:~# apt install openconnect
```

Open a `screen` to be able to start the OpenConnect VPN client and leave it running after you log out of  Machine B:

```bash
root@200.0.0.0:~# screen
```

Inside the screen, start the OpenConnect client:

```bash
root@200.0.0.0:~# openconnect --user test 100.0.0.0:8443 

POST https://100.0.0.0:8443/
Connected to 100.0.0.0:8443
SSL negotiation with 100.0.0.0
Server certificate verify failed: signer not found

Certificate from VPN server "100.0.0.0" failed verification.
Reason: signer not found
To trust this server in future, perhaps add this to your command line:
    --servercert pin-sha256:xxxxxxxxxxxxxxxxxxxxx
Enter 'yes' to accept, 'no' to abort; anything else to view: yes 
Connected to HTTPS on 100.0.0.0
XML POST enabled
Please enter your username.
Group: [Route[Exclude CN]|All Proxy|All]:All
POST https://100.0.0.0:8443/auth
XML POST enabled
Please enter your username.
POST https://100.0.0.0:8443/auth
Please enter your password.
Password:
POST https://100.0.0.0:8443/auth
Got CONNECT response: HTTP/1.1 200 CONNECTED
CSTP connected. DPD 90, Keepalive 32400
Connected as 192.168.xx.xx, using SSL + LZ4, with DTLS + LZ4 in progress
DTLS handshake failed: Error in the push function.
(Is a firewall preventing you from sending UDP packets?)
```

You are now connected to the VPN server on machine A. To exit the screen, press `Ctrl+A+D`. You can resume the screen connection (to see the VPN connection output or stop the connection by pressing `Ctrl+C`) by running the following command:

```bash
root@200.0.0.0:~# screen -r
```

### 3.5 Install and configure the OpenConnect server

This can be done using the exact same process as was done on Machine A:

```bash
root@200.0.0.0:~# mkdir ocserv
root@200.0.0.0:~# cd ocserv
root@200.0.0.0:~/ocserv# wget -qO- https://pastebin.com/raw/WZymtWi2 > ocserv.conf
root@200.0.0.0:~/ocserv# touch ocpasswd
root@200.0.0.0:~/ocserv# cd 
root@200.0.0.0:~# docker run --name ocserv --privileged -e NO_TEST_USER=1 -v $PWD/ocserv/:/etc/ocserv/ -p 8443:443 -p 8443:443/udp -d tommylau/ocserv
```

This should start the docker container running the OpenConnect server. Now you need to create a new user for connecting this this server - replace `USERNAME` with whatever username you want:

```bash
root@200.0.0.0:~# docker exec -ti ocserv ocpasswd -c /etc/ocserv/ocpasswd -g "Route,All" USERNAME
Enter password: 
Re-enter password:
```

> It won't show the password you're typing, don't get confused.

### 3.6 Install and configure Wireguard and IPSec VPN servers

OpenConnect usually has problems connecting on Apple products. You can use [Algo](https://github.com/trailofbits/algo) to install Wireguard and IPSec VPNs on Machine B so that Apple products can connect as well. Follow the instructions on https://github.com/trailofbits/algo and choose Local installation mode to install it locally on Machine B. More information here: https://github.com/trailofbits/algo/blob/master/docs/deploy-to-ubuntu.md

You can download and  use this file as `config.cfg` for the Algo installation: https://pastebin.com/raw/iARF0fGL  
This configuration file includes 100 users by default and has WireGuard and IPSec enabled. 

### 3.7 Tor

Tor connections are unstable. There are two methods for getting it work, and each method might work at different times. You can do both and test their connection to see which one works for you best.

#### 3.7.1 Method 1: Install and configure a Tor bridge inside Iran

Installing a Tor bridge will help people connect to Tor through Machine B which is easily accessible from within Iran. First make sure that the VPN is connnected (step 3.4). Then install Tor from the Ubuntu repositories to get an initial Tor connection up and runnning, then add the official Tor repository and reinstall/update Tor from the official repo.

```bash
root@200.0.0.0:~# apt install tor 
root@200.0.0.0:~# apt install apt-transport-tor
root@200.0.0.0:~# CODENAME=`lsb_release -c | grep Codename | cut -d: -f2 | tr -d [:space:] `
root@200.0.0.0:~# ARCH=`dpkg --print-architecture`
root@200.0.0.0:~# echo "deb [arch=$ARCH signed-by=/usr/share/keyrings/tor-archive-keyring.gpg] tor://apow7mjfryruh65chtdydfmqfpj5btws7nbocgtaovhvezgccyjazpqd.onion/torproject.org $CODENAME main" > /etc/apt/sources.list.d/tor.list
root@200.0.0.0:~# apt update
root@200.0.0.0:~# apt install tor obfs4proxy
```

Now empty out `/etc/tor/torrc` and open it using an editor:

```bash
root@200.0.0.0:~# echo > /etc/tor/torrc
root@200.0.0.0:~# nano /etc/tor/torrc
```

and paste this into the file, making sure to replace  `200.0.0.0` with the real IP address of Machine B and YOU@EMAIL.COM with an email address that you have access to but cannot be traced back to you:

```
BridgeRelay 1

# Replace "TODO1" with a Tor port of your choice.
# This port must be externally reachable.
# Avoid port 9001 because it's commonly associated with Tor and censors may be scanning the Internet for this port.
ORPort 200.0.0.0:8888

ServerTransportPlugin obfs4 exec /usr/bin/obfs4proxy

# This port must be externally reachable and must be different from the one specified for ORPort.
# Avoid port 9001 because it's commonly associated with Tor and censors may be scanning the Internet for this port.
ServerTransportListenAddr obfs4 0.0.0.0:9888

# Local communication port between Tor and obfs4.  Always set this to "auto".
# "Ext" means "extended", not "external".  Don't try to set a specific port number, nor listen on 0.0.0.0.
ExtORPort auto

# Replace "<address@email.com>" with your email address so we can contact you if there are problems with your bridge.
# This is optional but encouraged.
ContactInfo YOU@EMAIL.COM

```

Restart Tor and get your bridge line:

```bash
root@200.0.0.0:~# systemctl restart tor
root@200.0.0.0:~# cat /var/lib/tor/pt_state/obfs4_bridgeline.txt 
# obfs4 torrc client bridge line
#
# This file is an automatically generated bridge line based on
# the current obfs4proxy configuration.  EDITING IT WILL HAVE
# NO EFFECT.
#
# Before distributing this Bridge, edit the placeholder fields
# to contain the actual values:
#  <IP ADDRESS>  - The public IP address of your obfs4 bridge.
#  <PORT>        - The TCP/IP port of your obfs4 bridge.
#  <FINGERPRINT> - The bridge's fingerprint.

Bridge obfs4 <IP ADDRESS>:<PORT> <FINGERPRINT> cert=yyyyyyyy iat-mode=0
```

Copy `Bridge obfs4 <IP ADDRESS>:<PORT> <FINGERPRINT> cert=xxxxxxxx iat-mode=0` and replace `<IP ADDRESS` with `200.0.0.0` (Machine B IP address), replace `<PORT>` the port specified for `ServerTransportListenAddr` in `/etc/tor/torrc` (9888 by default), and `<FINGERPRINT>` with the output of this command:

```bash
root@200.0.0.0:~# cat /var/lib/tor/fingerprint
Unnamed xxxxxxxx
```

The bridge line should look like this now:

```
Bridge obfs4 200.0.0.0:9888 Unnamed xxxxxxxx cert=yyyyyyyy iat-mode=0
```



> Currently the Tor fails to confirm reachability of the bridge and you'll see `Your server has not managed to confirm reachability for its ORPort(s)` in `/var/log/syslog`. But you can connect to your bridge by specifying a custom bridge in Orbot or Tor Browser.

#### 3.7.2  Method 2: Proxy Tor traffic from Iran to a bridge outside Iran

This method was developed by [@meskio](https://github.com/meskio) and originally published [here](https://github.com/net4people/bbs/issues/127). We're just changing the vocabulary so that it matches the rest of this document.

First, you need to set up a bridge on Machine A (outside Iran). We'll do this using Docker - install it if you haven't already by following the instructions here https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository

```bash
root@100.0.0.0:~# mkdir bridge
root@100.0.0.0:~# cd bridge
root@100.0.0.0:~/bridge# wget https://gitlab.torproject.org/tpo/anti-censorship/docker-obfs4-bridge/-/raw/main/docker-compose.yml
```

Edit `bridge/.env` with the following content, changing `you@email.com` with an email address that you have access to but cannot be traced back to you:

```ini
# Set required variables
OR_PORT=3344
PT_PORT=3355
EMAIL=your@email.com

# If you want, you could change the nickname of your bridge
#NICKNAME=DockerObfs4Bridge

# Configure the bridge so it will not be distributed by bridgedb:
OBFS4_ENABLE_ADDITIONAL_VARIABLES=1
OBFS4V_BridgeDistribution=none
```

Start the bridge:

```bash
root@100.0.0.0:~/bridge# docker compose up -d
```

Get it's bridge line:

```bash
root@100.0.0.0:~/bridge# docker exec bridge-obfs4-bridge-1 get-bridge-line
obfs4 100.0.0.0:3355 AAABBBBCCCDDDD cert=abcdx iat-mode=0
```

Then on Machine B (inside Iran), you have two options for forwarding the Tor traffic to your bridge on Machine A:

1. Using SSH port forwarding
2. Using kcptun

##### Using SSH port forwarding

```bash
root@200.0.0.0:~# ssh -L 4457:127.0.0.1:4457 100.0.0.0:3355
```

##### Using kcptun

kcptun is a network enhancement proxy that tunnel a stream based traffic over a UDP transport protocol.

Run the following commands on Machine A:

```bash
root@100.0.0.0~# mkdir kcptun
root@100.0.0.0~# cd kcptun
root@100.0.0.0~/kcptun# wget https://github.com/xtaci/kcptun/releases/download/v20220628/kcptun-linux-amd64-20220628.tar.gz
root@100.0.0.0~/kcptun# server_linux_amd64 -t "127.0.0.1:3355" -l "0.0.0.0:7923" -mtu 1400 --nocomp -sndwnd 16384 --rcvwnd 16384 --datashard 0 --parityshard 0 --crypt aes --smuxver 2 --key "MY_PRE_SHARED_KEY"
```

Make sure to replace `MY_PRE_SHARED_KEY` for the `--key` parameter with a randomly generated string, and write it down. We'll need this value in a moment.

and then on Machine B:

```bash
root@200.0.0.0~# mkdir kcptun
root@200.0.0.0~# cd kcptun
root@200.0.0.0~/kcptun# wget https://github.com/xtaci/kcptun/releases/download/v20220628/kcptun-linux-amd64-20220628.tar.gz
root@200.0.0.0~/kcptun# client_linux_amd64 -l "0.0.0.0:3355" -r "100.0.0.0:7923" -mtu 1400 --nocomp -sndwnd 16384 --rcvwnd 16384 --datashard 0 --parityshard 0 --crypt aes --smuxver 2 --key "MY_PRE_SHARED_KEY"
```

Replace `MY_PRE_SHARED_KEY` with the same random string from the previous step. Also change `100.0.0.0` with the IP  address of Machine A.

### 3.8 Set up a standalone Snowflake Proxy

You can also set up a standalone Snowflake proxy on Machine B to help censored users connect to the Tor network. 

The docker-compose version on Ubuntu 20.04 is a bit old, you need to first add the official docker registry and install  docker from there: https://docs.docker.com/engine/install/ubuntu/#set-up-the-repository

Once the docker installation is done, run the container:

```bash
root@200.0.0.0:~# mkdir snowflake
root@200.0.0.0:~# cd snowflake
root@200.0.0.0:~# wget https://gitlab.torproject.org/tpo/anti-censorship/docker-snowflake-proxy/-/raw/main/docker-compose.yml
root@200.0.0.0:~# docker compose up -d
```

Your snowflake proxy is now up and running and will output some usage statistics every hour on docker logs (first output will appear one hour after starting the docker container):

```
root@200.0.0.0:~# docker compose logs snowflake-proxy
```

## 4. Connecting to the VPN and Tor from your local devices

### 4.1 OpenConnect

You need to install the OpenConnect app on your devices (Android, Windows and Linux) in order to connect to your VPN.

Once installed, use `200.0.0.0:8443` as host and the username and password you created in step 2.6. 

> Each OpenConnect VPN account can be used by multiple users simultaneously. There's no need to create multiple user profiles if you want the VPN to be used by multiple people at the same time.

### 4.2 Wireguard and IPSec

Algo saves the connection profile configuration files in `/path/to/algo/configs/200.0.0.0/` . Compress and copy this folder to your local machine and share them with your family and friends. More information here: https://github.com/trailofbits/algo#configure-the-vpn-clients

> Each Wireguard and IPSec configuration profile (user) can only be used on a single device si	multaneously. If want to connect with both your laptop and mobile phone at the same time, use two separate configuration profiles. Using a single profile for connecting from multiple devices causes connectivity issues.

### 4.3 Tor

#### 4.3.1 Bridge inside Iran

> This is for using the bridge created in section 3.7.1

In Orbot or Tor Browser, enable `Use Bridges` and select the `Custom Bridges` option, and enter the bridge line you constructed in section 3.7.1 in the `Paste Bridges` section. You should now be able to connect and use Tor in seconds.

#### 4.3.2 Bridge outside Iran with a proxy inside Iran

> This is for using the bridge created in section 3.7.2

distribute the bridgeline you got in section 3.7.2, replacing the IP address with the one of Machine B (200.0.0.0):

```
obfs4 200.0.0.0:3355 AAABBBBCCCDDDD cert=abcdx iat-mode=0
```

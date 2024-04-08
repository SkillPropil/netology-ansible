# Домашнее задание к занятию 2 «Работа с Playbook»
## Основная часть
В общем все задания выполнил, итоговый вывод такой.

```
root@msk1wst405n:/opt/netology-ansible# ansible-playbook -i inventory/prod.yml site.yml -u root -k
SSH password:

PLAY [Install Clickhouse] **********************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get clickhouse distrib] ******************************************************************************************************************************************************************
ok: [clickhouse-01] => (item=clickhouse-client)
ok: [clickhouse-01] => (item=clickhouse-server)
failed: [clickhouse-01] (item=clickhouse-common-static) => {"ansible_loop_var": "item", "changed": false, "dest": "./clickhouse-common-static-22.3.3.44.rpm", "elapsed": 0, "gid": 0, "group": "root", "item": "clickhouse-common-static", "mode": "0644", "msg": "Request failed", "owner": "root", "response": "HTTP Error 404: Not Found", "secontext": "unconfined_u:object_r:admin_home_t:s0", "size": 246310036, "state": "file", "status_code": 404, "uid": 0, "url": "https://packages.clickhouse.com/rpm/stable/clickhouse-common-static-22.3.3.44.noarch.rpm"}

TASK [Get clickhouse distrib] ******************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Install clickhouse packages] *************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Flush handlers] **************************************************************************************************************************************************************************

TASK [Create database] *************************************************************************************************************************************************************************
ok: [clickhouse-01]

PLAY [Install Vector] **************************************************************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Get vector rpm] **************************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Install vector package] ******************************************************************************************************************************************************************
ok: [clickhouse-01]

TASK [Generate vector config] ******************************************************************************************************************************************************************
ok: [clickhouse-01]

PLAY RECAP *************************************************************************************************************************************************************************************
clickhouse-01              : ok=8    changed=0    unreachable=0    failed=0    skipped=0    rescued=1    ignored=0
```
vector установлен, конфигурацию подсунул в j2.
Пытался установить в режиме ручной установки, но либо документация хромает, либо я не понял чего-то, но не получилось.
Так как дедлайн уже истек - решил установить yum'ом

```
● vector.service - Vector
   Loaded: loaded (/usr/lib/systemd/system/vector.service; disabled; vendor preset: disabled)
   Active: active (running) since Mon 2024-04-08 09:15:42 EDT; 6min ago
     Docs: https://vector.dev
  Process: 5086 ExecStartPre=/usr/bin/vector validate (code=exited, status=0/SUCCESS)
 Main PID: 5089 (vector)
   CGroup: /system.slice/vector.service
           └─5089 /usr/bin/vector

Apr 08 09:22:15 skillpropilserv-1.localhost vector[5089]: {"appname":"AnthraX","facility":"mail","hostname":"make.sk","message":"Take a breath, let it go, walk away","msgid":"ID2...version":2}
Apr 08 09:22:16 skillpropilserv-1.localhost vector[5089]: {"appname":"KarimMove","facility":"clockd","hostname":"for.loans","message":"Take a breath, let it go, walk away","msgid...version":2}
Apr 08 09:22:17 skillpropilserv-1.localhost vector[5089]: {"appname":"BronzeGamer","facility":"auth","hostname":"random.xn--90ae","message":"A bug was encountered but not in Vect...version":1}
Apr 08 09:22:18 skillpropilserv-1.localhost vector[5089]: {"appname":"CrucifiX","facility":"kern","hostname":"some.whoswho","message":"We're gonna need a bigger boat","msgid":"ID...version":1}
Apr 08 09:22:19 skillpropilserv-1.localhost vector[5089]: {"appname":"b0rnc0nfused","facility":"local0","hostname":"make.mq","message":"We're gonna need a bigger boat","msgid":"I...version":1}
Apr 08 09:22:20 skillpropilserv-1.localhost vector[5089]: {"appname":"ahmadajmi","facility":"cron","hostname":"for.gay","message":"You're not gonna believe what just happened","m...version":2}
Apr 08 09:22:21 skillpropilserv-1.localhost vector[5089]: {"appname":"devankoshal","facility":"local6","hostname":"for.tl","message":"Pretty pretty pretty good","msgid":"ID290","...version":2}
Apr 08 09:22:22 skillpropilserv-1.localhost vector[5089]: {"appname":"meln1ks","facility":"user","hostname":"make.nab","message":"Take a breath, let it go, walk away","msgid":"ID...version":2}
Apr 08 09:22:23 skillpropilserv-1.localhost vector[5089]: {"appname":"BronzeGamer","facility":"local2","hostname":"for.band","message":"Take a breath, let it go, walk away","msgi...version":1}
Apr 08 09:22:24 skillpropilserv-1.localhost vector[5089]: {"appname":"devankoshal","facility":"audit","hostname":"random.xn--h2breg3eve","message":"You're not gonna believe what ...version":2}
Hint: Some lines were ellipsized, use -l to show in full.

```

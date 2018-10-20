# 1200kbit_infra
1200kbit Infra repository

bastion_IP = 35.204.36.139
someinternalhost_IP = 10.164.0.3

Подключиться по ssh к someinternalhost с клиента с пробросом ключа через bastionhost можно командой:
`ssh -o ProxyCommand="ssh -W %h:%p 1200kbit@35.204.36.139" 1200kbit@10.164.0.3`

Для удобного обращения к хостам пропишем для них алиасы.
Для хоста someinternalhost так же пропишем опцию подключения ProxyCommand.

1. Создадим файл `~/.ssh/config` с содержимым:
```
Host bastion
	Hostname 35.204.36.139
	User 1200kbit

Host someinternalhost
	Hostname 10.164.0.3
	User 1200kbit
	ProxyCommand ssh -W %h:%p bastion
```
2. Возможно понадобится поменять права на файл `~/.ssh/config`, оставив права только для владельца(600).

Теперь подключиться к хосту someinternalhost можно короткой коммандой:
`ssh someinternalhost`

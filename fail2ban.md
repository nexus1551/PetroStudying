**Сегодня мы изучем как поставим свой fail2ban на сервер debian**
-------------------------------------------------------------
1) Обновим сервер до актуального apt update && apt upgrade -y
2) Установим fail2ban на сервер : apt install fail2ban -y
3) Основаная директория будет находиться в /etc/fail2ban/
Так как основной файл jail.conf лучше не трогать, создадим jail.local и настроем его полностью
   
**/etc/fail2ban/jail.local**
[sshd]
git commit enabled = true   #включаем его
git commit port = ssh   #выбираем порт
git commit logpath = /var/log/auth.log   #где будут находится все логи
git commit maxretry = 3   #максимальное кол-во попыток
git commit bantime = 7200   #время бана в секундах
git commit bantime.increment = true   #увеличение бана при неправильном вводе
git commit bantime.factor = 2   #во сколько раз увеличится бан

  На свой сервер мне надо было настроить только fail2ban на ssh из-за этого других настроек тут нет
  4) После всей настройки перезагружаем fail2ban systemctl restart fail2ban
  ------------------------------------------------------------
  **Проверить работает или нет можно по командам**
  - systemctl status fail2ban    #Просто проверяем работает ли сама служба
  - fail2ban-client status sshd    #Проверяем забанненых пользователей по ssh

# Настройка доступа к FoundryVTT на VPS-сервере
Как я уже и писал ранее, второй способ - это размещение FoundryVTT на арендованном VPS/VDS сервере. Можно использовать партнёрские для FoundryVTT хостинги, в этом есть как преимущества, так и недостатки. Давайте взглянем подробнее: 

### Плюсы
- Как и обычные хостинги, серверы, размещенные у партнеров, всегда подключены к сети и обычно имеют более быстрое подключение к Интернету, чем домашнее соединение при селф-хостинге.


- Упрощенная настройка сервера — хостинг-партнер берет на себя тяжелую работу по подключению сервера к сети и поддержанию его в рабочем состоянии.


- Хостинг-партнеры обычно предлагают фиксированные тарифы на выделенные серверы, а поставщики обычных хостингов обычно предлагают условия оплаты по мере использования своих услуг.

### Минусы

- Хостинги-партнеры предлагают более ограниченную гибкость при настройке сервера (например некоторые модули могут быть недоступны для установки и прочие подобные нюансы) — на обычном же сервере возможности настройки неограничены, всё решаете только вы.


- В обмен на дополнительные функции хостинг-партнеры могут взимать больше за то, что вы получаете, чем если бы вы обращались напрямую к провайдеру обычного хостинга и настраивали его самостоятельно.


- Зачастую нельзя оплатить из РФ обычными способами.

В целом, различий не так уж и много. Но например лично мне, гораздо удобнее контролировать сервер целиком и иметь максимальную широту действий. Поэтому я выбираю обычный хостинг, где нужно чуть-чуть заморочиться с настройкой и затем свободно пользоваться. Однако, если вам больше нравятся условия партнерского хостинга, то почему бы и нет. Вот список хостингов-партнёров FoundryVTT : 

- https://www.foundryserver.com/ 
- https://forge-vtt.com/
- https://moltenhosting.com/
- https://www.sqyre.app/

Можете выбирать любой и использовать, все четыре - это официальные партнёры FoundryVTT. Я здесь к сожалению каких-либо советов дать не могу, так как ни разу не пользовался их услугами. А мы тем временем, поедем дальше =)

# Настройка Foundry на вашем сервере

Более детальные комментарии даны в видео, текстовая инструкция лишь шпаргалка, чтобы иметь перед собой алгоритм действий. Поэтому крайне рекоммендую сначала ознакомиться с видео.

[![Видео](https://markdown-videos-api.jorgenkh.no/url?url=https%3A%2F%2Fyoutube.com%2Fwatch%3Fv%3DTJGdipRdwvE)](https://youtube.com/watch?v=TJGdipRdwvE)
> [!IMPORTANT]
> Инструкцию буду поддерживать в актуальном состоянии. Если вы нашли ошибку или что-то идет не так, пишите мне, актуализирую статью:
>
> [@marestore_support](https://t.me/marestore_support)

## Требуемые технические характеристики к серверу

**Минимальные:**
* 1 vCPU
* Место на диске: 1GB
* 2 GB RAM
* Firewall и настройки безопасности настроены так, что позволяют игрокам зайти на сервер на необходимый порт.

**Рекомендуемые:**
* 2 vCPU
* Место на диске: 1GB
* 4 GB RAM
* Firewall и настройки безопасности настроены так, что позволяют игрокам зайти на сервер на необходимый порт.

_Объем памяти, требуемый серверным процессом, зависит от объема данных, включенных в игровую систему и модулей, которые активны в вашем мире. Для более крупных систем или миров, в которых используются более ресурсоемкие модули, потребуется больше оперативной памяти._

**Рекомендую сервера AEZA, сам ими пользуюсь. По этой [реферальной ссылке](https://aeza.net/?ref=352255) вы получите +15% к пополнению в первые 24 часа.**

## Прежде чем начать

Я могу настроить для вас сервер, а также купить foundry. Пишите в телеграм:

[@marestore_support](https://t.me/marestore_support)


## Обновление системы

```bash
sudo apt-get update
```

```bash
sudo apt-get upgrade
```

```bash
reboot
```

## Установка Node.js

```bash
curl -fsSL https://deb.nodesource.com/setup_23.x -o nodesource_setup.sh
```

```bash
sudo -E bash nodesource_setup.sh
```

```bash
sudo apt-get install -y nodejs
```

Проверяем установленные версии

```bash
node --version
```

```bash
npm --version
```

## Установка zip и unzip

```bash
sudo apt-get install zip unzip
```

## Создание пользователя

```bash
adduser foundry
```

```bash
usermod -aG sudo foundry
```

## Войти под новым пользователем

```bash
su - foundry
```

## Установка PM2

```bash
sudo npm install pm2 -g
```

# Установка Foundry

## Создание папок

```bash
mkdir foundryvtt
```

```bash
mkdir foundrydata
```

## Скачивание архива

Для начала надо войти в папку **foundryvtt**

```bash
cd foundryvtt
```
> [!IMPORTANT]
> Войдите в вашу учетную запись на **https://foundryvtt.com/**, перейти в раздел **Purchased Licenses**, в **Operating System** выбрать **Linux/NodeJS**, затем нажать на кнопку **Timed URL**. В буфер обмена скопируется ссылка.

```bash
wget -O 'foundry.zip' 'ССЫЛКА_КОТОРУЮ_МЫ_ПОЛУЧИЛИ_ВЫШЕ'
```

## Распаковка

```bash
unzip foundry.zip
```

# Добавление Foundry в PM2

## Установка PM2

```bash
sudo npm install pm2 -g
```

## Настрйока PM2

```bash
pm2 startup
```

#### Скопировать и выполнить строку, которая выдаст команда выше, должно получится что-то вроде этого:

```bash
sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u ubuntu --hp /home/ubuntu
```

> [!WARNING]
> _Не копируйте эту строку, вашу строку вам выдаст комманда выше, это лишь пример_

## Добавить команду запуска Foundry в PM2

```bash
pm2 start "node $HOME/foundryvtt/resources/app/main.js --dataPath=$HOME/foundrydata" --name foundry
```

**СЕРВЕР РАБОТАЕТ, ДАЛЬНЕЙШИЕ НАСТРОЙКИ ОПЦИОНАЛЬНЫ, ЕСЛИ ИМЕЕТСЯ СВОЙ ДОМЕН**

# Настройка NGINX

## Установка NGINX

```bash
sudo apt-get install nginx
```

## Настройка Firewall

```bash
sudo ufw allow 'Nginx Full'
```

> [!NOTE]
> опционально, если еще не сделали это ранее на своем сервере:
> ```bash
> sudo ufw allow OpenSSH
> ```

```bash
sudo ufw status
```

```bash
sudo ufw enable
```

```bash
systemctl status nginx
```

## Создание конфига

```bash
sudo nano /etc/nginx/sites-available/foundry.example.com
```

## Скопировать и вставить блок ниже

```bash 
server {

    # Enter your fully qualified domain name or leave blank
    server_name             foundry.example.com www.foundry.example.com; #ВАШИ ДОМЕНЫ

    # Listen on port 80 without SSL certificates
    listen                  80;

    # Sets the Max Upload size to 300 MB
    client_max_body_size 300M;

    # Proxy Requests to Foundry VTT
    location / {

        # Set proxy headers
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # These are important to support WebSockets
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "Upgrade";

        # Make sure to set your Foundry VTT port number
        proxy_pass http://localhost:30000;
    }
}
```

> [!IMPORTANT]
> Заменить `foundry.example.com` на ваш домен.

## "Включить" конфиг
```bash
sudo ln -s /etc/nginx/sites-available/foundry.example.com /etc/nginx/sites-enabled/
```

> [!IMPORTANT]
> Заменить `foundry.example.com` на ваш домен.

## Дополнительная настройка
```bash
sudo nano /etc/nginx/nginx.conf
```

Найти и расскомментировать (убрать '#') перед строчкой:

```bash
server_names_hash_bucket_size 64;
```

## Валидация настроек

```bash
sudo nginx -t
```

## Перезапуск NGINX

```bash
sudo systemctl restart nginx
```

# Настройка SSL

## Установка certbot

```bash
sudo apt install certbot python3-certbot-nginx
```

## Создание сертификата для домена
```bash
sudo certbot --nginx -d foundry.example.com -d www.foundry.example.com
```

> [!IMPORTANT]
> Заменить `foundry.example.com` на ваш домен.

## Перезапуск NGINX

```bash
sudo systemctl restart nginx
```


## Полезные ссылки

1. [How To Create a Self-Signed SSL Certificate for Nginx in Ubuntu 22.04](https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-in-ubuntu-22-04)
2. [NodeSource Node.js Binary Distributions | Installation Instructions](https://github.com/nodesource/distributions#installation-instructions)
3. [Ubuntu VM](https://foundryvtt.wiki/en/setup/hosting/Ubuntu-VM)
4. [Recommended Linux Installation and Usage Guide for FoundryVTT](https://foundryvtt.wiki/en/setup/linux-installation)

নিচে আমি তোমার জন্য একটা **GitHub README.md ready file** বানিয়ে দিলাম — তুমি সরাসরি রিপোতে paste করতে পারবে 👇

---

# 🐘 PHP Hello World with Docker

এই project এ একটি simple PHP “Hello World” app Docker ব্যবহার করে run করা হয়েছে।

---

# 📁 Project Structure

```
project-folder/
│
├── index.php
└── Dockerfile
```

---

# 🚀 1. index.php (PHP Code)

```php
<?php
echo "Hello, World!";
?>
```

---

# 🐳 2. Dockerfile

```Dockerfile
FROM php:8.2-apache

COPY . /var/www/html/

EXPOSE 80
```

---

# ⚙️ 3. Docker Commands (Full Guide)

---

## 🟢 Build Docker Image

```bash
docker build -t php-hello .
```

👉 এখানে:

* `php-hello` = image name
* `.` = current folder

---

## 🟢 Run Docker Container

```bash
docker run -d -p 8080:80 php-hello
```

👉 এখানে:

* `-d` = background run
* `-p 8080:80` = local port 8080 → container port 80

---

## 🟢 Run with Custom Name (Recommended)

```bash
docker run -d -p 8080:80 --name myphp php-hello
```

---

## 🟢 Check Running Containers

```bash
docker ps
```

---

## 🟢 Stop Container

### By Name:

```bash
docker stop myphp
```

### By ID:

```bash
docker stop <container_id>
```

---

## 🟢 Remove Container

```bash
docker rm myphp
```

---

## 🟢 View Logs

```bash
docker logs myphp
```

---

## 🟢 Enter Container (Shell Access)

```bash
docker exec -it myphp bash
```

---

## 🟢 Live Code Update (No Rebuild Needed)

```bash
docker run -d -p 8080:80 -v ${PWD}:/var/www/html php-hello
```

👉 Windows CMD:

```bash
docker run -d -p 8080:80 -v %cd%:/var/www/html php-hello
```

---

# 🌐 4. Open in Browser

```
http://localhost:8080
```

👉 Output:

```
Hello, World!
```

---

# 🔥 Important Notes

* Dockerfile change করলে আবার build করতে হবে
* PHP file change করলে volume use করলে rebuild লাগবে না
* Port change করলে `-p` update করতে হবে

---

# 🎯 Bonus Tip

Better workflow:

```bash
docker run -d -p 8080:80 --name php-dev -v ${PWD}:/var/www/html php-hello
```

---

# 🚀 Done!

এটা এখন GitHub এ upload করার জন্য fully ready README.md 🎉

---

চলুন আমি আপনাকে একটা **complete PHP + MySQL full stack Docker Compose project** দেই — যেটা আপনি GitHub এ রাখতে পারবেন এবং real project হিসেবে use করতে পারবেন 🔥

---

# 🐘 PHP + 🐬 MySQL Full Stack (Docker Compose)

---

# 📁 Project Structure

```
project-folder/
│
├── docker-compose.yml
├── Dockerfile
├── index.php
└── db.php
```

---

# 🐳 1. docker-compose.yml

```yaml
version: "3.8"

services:
  php:
    build: .
    container_name: php_app
    ports:
      - "8080:80"
    volumes:
      - .:/var/www/html
    depends_on:
      - db

  db:
    image: mysql:8.0
    container_name: mysql_db
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: testdb
      MYSQL_USER: user
      MYSQL_PASSWORD: user123
    ports:
      - "3306:3306"
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

---

# 🐘 2. Dockerfile (PHP Apache)

```Dockerfile
FROM php:8.2-apache

RUN docker-php-ext-install mysqli pdo pdo_mysql

COPY . /var/www/html/

EXPOSE 80
```

---

# 🌐 3. index.php (Test Page)

```php
<?php
echo "PHP is working! <br>";

// DB connection test
$conn = new mysqli("db", "user", "user123", "testdb");

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

echo "Connected to MySQL successfully!";
?>
```

---

# 🔌 4. db.php (Optional reusable connection)

```php
<?php
$conn = new mysqli("db", "user", "user123", "testdb");

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
?>
```

---

# 🚀 5. Run Commands

## 🟢 Step 1: Build & Start

```bash
docker-compose up -d --build
```

---

## 🟢 Step 2: Check Running Containers

```bash
docker ps
```

---

## 🟢 Step 3: Open Browser

```
http://localhost:8080
```

---

## 🟢 Step 4: Stop Everything

```bash
docker-compose down
```

---

## 🟢 Step 5: Stop + Remove DB Data

```bash
docker-compose down -v
```

---

# 🧠 How it works

| Service         | কাজ                              |
| --------------- | -------------------------------- |
| PHP container   | Web server (Apache + PHP)        |
| MySQL container | Database                         |
| docker-compose  | দুইটা service একসাথে connect করে |

---

# 🔥 Important Tips

### ✔️ DB host name

```php
"db"
```

👉 কারণ docker-compose service name = db

---

### ✔️ Auto reload (development)

```yaml
volumes:
  - .:/var/www/html
```

---

# 🎯 Result

* PHP runs on: `http://localhost:8080`
* MySQL runs internally on Docker network
* Full stack ready for development

---

# 🚀 Bonus (Next Level)

চলুন আমি আপনাকে একটা **production-ready Laravel + MySQL Docker setup** দেই 🔥
এটা আপনি GitHub এ রেখে সরাসরি project start করতে পারবেন।

---

# 🚀 Laravel + MySQL with Docker (Full Setup)

---

# 📁 Project Structure

Laravel project ধরেই ধরুন:

```id="lar1st"
laravel-app/
│
├── docker-compose.yml
├── Dockerfile
├── nginx/
│   └── default.conf
├── src/   (Laravel project এখানে থাকবে)
```

---

# 🐳 1. docker-compose.yml

```yaml id="dc1"
version: "3.8"

services:

  app:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: laravel_app
    volumes:
      - ./src:/var/www/html
    working_dir: /var/www/html
    depends_on:
      - db

  web:
    image: nginx:latest
    container_name: laravel_nginx
    ports:
      - "8000:80"
    volumes:
      - ./src:/var/www/html
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - app

  db:
    image: mysql:8.0
    container_name: laravel_db
    restart: always
    environment:
      MYSQL_DATABASE: laravel
      MYSQL_ROOT_PASSWORD: root
      MYSQL_USER: laravel
      MYSQL_PASSWORD: secret
    ports:
      - "3306:3306"
    volumes:
      - dbdata:/var/lib/mysql

volumes:
  dbdata:
```

---

# 🐘 2. Dockerfile (PHP-FPM)

```Dockerfile id="dc2"
FROM php:8.2-fpm

# System packages
RUN apt-get update && apt-get install -y \
    git curl zip unzip libpng-dev libonig-dev libxml2-dev

# PHP extensions
RUN docker-php-ext-install pdo pdo_mysql mbstring exif pcntl bcmath gd

# Composer install
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

WORKDIR /var/www/html
```

---

# 🌐 3. Nginx Config

📁 `nginx/default.conf`

```nginx id="ng1"
server {
    listen 80;
    index index.php index.html;
    server_name localhost;
    root /var/www/html/public;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass app:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

---

# 🚀 4. Setup Laravel Project

👉 প্রথমে folder এর ভিতরে Laravel install করুন:

```bash id="lv1"
docker run --rm -v ${PWD}/src:/app composer create-project laravel/laravel .
```

---

# ⚙️ 5. Start Docker

```bash id="lv2"
docker-compose up -d --build
```

---

# 🌐 6. Open Browser

```id="lv3"
http://localhost:8000
```

---

# 🧠 7. Laravel .env DB Config

`.env` file এ এটা দিন:

```env id="lv4"
DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=laravel
DB_PASSWORD=secret
```

---

# 🔄 8. Run Migration

```bash id="lv5"
docker exec -it laravel_app php artisan migrate
```

---

# 🛑 9. Stop Project

```bash id="lv6"
docker-compose down
```

---

# 🧹 10. Full Reset (DB delete সহ)

```bash id="lv7"
docker-compose down -v
```

---

# 🔥 System Flow

| Service       | কাজ             |
| ------------- | --------------- |
| app (PHP-FPM) | Laravel backend |
| nginx         | Web server      |
| db (MySQL)    | Database        |

---

# ⚡ Features

✔ Laravel auto run
✔ MySQL connected
✔ Nginx production ready
✔ Volume-based live development
✔ Easy GitHub deploy

---

# 🚀 Bonus (Next Level আমি দিতে পারি)

চাইলে আমি আপনাকে next upgrade দিতে পারি:

* Laravel + React (Docker)
* Laravel + Redis + Queue system
* Laravel + Swagger API setup
* Production deploy (VPS + Docker + SSL)

বললেই next level architect system বানিয়ে দিব 🔥



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

চাইলে আমি আপনাকে next step শিখাতে পারি:

👉 PHP CRUD with MySQL (Create, Read, Update, Delete)
👉 phpMyAdmin add করা
👉 Laravel + MySQL Docker setup
👉 Production-ready Docker setup (Nginx + PHP-FPM)

বললেই next level project বানিয়ে দিব 🔥


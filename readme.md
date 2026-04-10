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

চাইলে আমি তোমার জন্য:
👉 Laravel Docker setup
👉 PHP + MySQL full stack Docker Compose
👉 Auto reload development environment

সব বানিয়ে দিতে পারি 🔥

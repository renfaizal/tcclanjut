
## Part 1 - Deploying Your First Docker Container
#### Step 1 - Menjalankan Sebuah Container
1. Jalankan perintah `docker search redis` untuk mencari image di docker hub.

![01](part1/ss3.jpg)

2. Jalankan perintah `docker run -d redis` untuk membuat dan menjalankan container redis. Untuk melihat status dari container jalankan perintah `docker ps`

![02](part1/ss4.jpg)

#### Step 2 - Menampilkan Container Yang Berjalan
1. 

![03](part1/ss5.jpg)

#### Step 3 - Mengakses Redis 1
Agar container yang dibuat dapat diakses dari publik, maka container tersebut harus dilakukan port expose.
1. 

![04](part1/ss6.jpg)

#### Step 4 - Mengakses Redis 2
1. Selain mengekspose dengan menentukan port yang akan digunakan untuk mengakses dari publik,  port exposing dapat juga dilakukan secara dynamic (random port assignment).

![05](part1/ss7.jpg)

2. Untuk melihat port berapa yang diberikan oleh docker untuk container yang tadi diekspose, dapat digunakan perintah `docker port redisDynamic`.

![06](part1/ss8.jpg)

3. Untuk melihat daftar container yang berjalan, gunakan perintah `docker ps`.

![07](part1/ss9.jpg)

#### Step 5 - Menjalankan Kontainer
#### Step 6 - Menjalankan Kontainer

## Part 2 - Deploy Static HTML Website as Container
## Part 3 - Building Container Images

<p align="center">
  <img src="https://gitforwindows.org/img/gwindows_logo.png"/>
</p>


# Docker Network

<p align="center">
  <img src="https://www.docker.com/sites/default/files/social/docker_facebook_share.png"/>
</p>

## Menggunakan Link

Salah satu cara untuk menghubungkan container satu dengan container lainnya pada docker adalah menggunakan Link. Docker Link merupakan sebuah fitur yang memungkinkan kita untuk mengijinkan container untuk melakukan discovery dengan container lainnya dan dapat melakukan pertukaran informasi antar container secara aman.

1. Menjalankan Redis.

	Untuk percobaan jalankan sebuah redis server pada container yang nantinya akan kita hubungkan dengan container lainnnya.
	
	![01](link/ss1.jpg)

2. Membuat link
	
	Untuk terhubung ke sebuah container digunakan tambahan opsi  `--link <container-name|id>:<alias>` pada perintah saat dilakukan launching container baru.

	Cara kerja dari link ini pertama Docker akan membuat sebuah environment berdasarkan pada container yang saling terhubung. Environment ini nantinya akan memberikan sebuah informasi referensi seperti Port dan IP Address dari container.

	![02](link/ss2.jpg)

	Selanjutnya Docker akan mengupdate file HOSTS dari container dengan sebuah entry untuk container asal dengan tiga nama, yaitu: asal, alias dan hash-id.

	![03](link/ss3.jpg)

	Setelah link terbentuk, kita dapat melakukan ping ke source container.

	![04](link/ss4.jpg)

3. Menghubungkan aplikasi

	Dengan dibuatnya link, aplikasi dapat terhubung dan berkomunasi dengan source container dengan cara yang biasa.

	Berikut adalah salah satu contoh aplikasi sederhana dari node.js yang terhubung dengan redis menggunakan hostname redis.

	![05](link/ss5.jpg)

	Untuk mengetes koneksi dapat digunakan perintah `curl docker:3000`

	![06](link/ss6.jpg)

4. Menghubungkan ke CLI Redis

	Selain menghubungkan aplikasi dengan source container, kita juga dapat menghubungkannya dengan tool CLI mereka sendiri.

	Jalankan CLI dari Redis

	![07](link/ss7.jpg)

	Jalankan perintah `KEYS *` untuk menampilkan konten yang saat ini disimpan dalam source container redis

	![08](link/ss8.jpg)

	Ketikkan perintah `QUIT` untuk keluar dari CLI

	![09](link/ss9.jpg)

## Menggunakan Docker Network  
Selain menggunakan link, dapat pula digunakan network untuk saling berkomunikasi antar container.
1. Membuat Network Baru

	Membuat Network
	
	Untuk membuat sebuah network yang nantinya akan digunakan untuk komunikasi antar container dapat digunakan syntax `docker network create`.
	
	![01](network/ss1.jpg)
	
	Menghubungkan ke sebuah Network
	
	Selanjutnya untuk menghubungkan sebuah container ke sebuah network, pada saat dilakukan running container ditambahkan parameter `--net=[nama network]`.
	
	![02](network/ss2.jpg)

2. Komunikasi Dalam Sebuah Network

	Docker Network bersifat seperti network traditional dimana node dapat dihubungkan dan didisconnect.
	Hal pertama yang akan kita sadari yaitu bahwa Docker tidak lagi melakukan assign environment variable ataupun mengupdate file hosts yang berada pada container.

	![03](network/ss3.jpg)

	![04](network/ss4.jpg)

	Terlihat informasi yang tersimpan dalam file hosts container.
	Cara dari container untuk saling berkomunikasi melalui Embedded DNS Server pada Docker.  DNS ini diassign ke semua container melalui IP 127.0.0.11 dan terkonfigurasi pada file resolv.conf

	![05](network/ss5.jpg)

	Ketika sebuah container mencoba untuk mengakses container lain melalui sebuah nama container, maka DNS akan mengambalikan IP Address dari container yang dimaksud.

	![06](network/ss6.jpg)

3. Menghubungkan Dua Container
	
	Docker mendukung multiple network dan caontainer dapat diattach ke lebih dari satu network dalam satu waktu.
	
	Buat network baru dengan syntax `docker network create`
	
	![07](network/ss7.jpg)

	Kemudian hubungkan container ke network yang dimaksud menggunakan perintah `docker network connect`
	
	![08](network/ss8.jpg)
	
	Deploy container baru yang terhubung  dengan network yang baru saja dibuatnya
	
	![09](network/ss9.jpg)
	
	Untuk mengetes container gunakan perintah `curl`
	
	![10](network/ss10.jpg)
	
	
4. Membuat Aliases
	
	Links masih dapat digunakan ketika container menggunakan docker network dan menyediakan sebuah cara untuk mendefinisikan sebuah alias pada nama container.  Hal ini akan memberikan DNS entry tambahan dan dapat digunakan untuk melakukan discovery container.
	
	Untuk menghubungkan container menggunakan alias jalankan syntax berikut
	
	![11](network/ss11.jpg)
	
	Untuk mengetes container apakah container sudah terhubung dengan network atau belum dapat digunakan sntax berikut:
	
	![12](network/ss12.jpg)
	

5. Memutuskan Container

	Untuk menampilkan daftar network yang ada dapat digunakan perintah `docker network ls`
	
	![13](network/ss13.jpg)
	
	Untuk melihat informasi container mana yang yang terhubung dengan sebuah docker network beserta IP Addressnya dapat digunakan perintah `docker network inspect`
	
	![14](network/ss14.jpg)
	
	Untuk melakukan disconnect sebuah container dengan sebuah docker network dapat digunakan perintah `docker network disconnect`
	
	![15](network/ss15.jpg)


# GO WEB

<p align="center">
  <img src="images/go.png"/>
</p>

## Hello World

Go merupakan sebuah bahasa pemrograman yang memiliki webserver built in. Package net/http merupakan library standar yang berisikan semua fungsionalitas untuk protocol HTTP. Termasuk sebuah client HTTP dan server HTTP.


1. Registering a Request Handler

	Pertama, buat sebuah Handler yang digunakan untuk menerima semua koneksi HTTP yang masuk dari browser, client HTTP ataupun request API. Handler pada Go adalah sebuah fungsi yang memiliki struktur sebagai berikut
	
	'func (w http.ResponWritter, r *http.Request)'

	Fungsi tersebut memiliki dua parameter, yaitu:
	
	1. `http.ResponWriter` yang digunakan untuk memberikan respon teks/html
	2. `http.Request` yang berisikan semua informasi mengenai request HTTP, termasuk url maupun header. 

	Untuk mendaftarkan sebuah request handler sebagai HTTP Server default dapat dilakukan dengan cara yang sederhana seperti dibawah ini:

	> http.HandleFunc("/", func (w http.ResponseWriter, r  *http.Request) {
	>	fmt.Fprintf(w, "Hello, you've requested: %s\n", r.URL.Path)
> })


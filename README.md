# Laporan Proyek Machine Learning - Wahyu Bagus Wicaksono

## Project Overview
<br>

### Latar Belakang
Anime merupakan kata bahasa jepang yang berasal dari bahasa inggris yaitu *animation*, pada bahasa indonesia biasa disebut dengan animasi. Anime banyak diminati oleh orang di seluruh dunia salah satunya di indonesia. Selain itu anime sendiri bisa kita tonton dimana saja dan kapan saja karena sudah tersedia di banyak platform seperti *Crunchyroll*, *Netflix*, *Youtube* dan platform lainnya.

Sistem Rekomendasi merupakan suatu aplikasi yang digunakan untuk memberikan rekomendasi dalam membuat suatu keputusan yang diinginkan pengguna, untuk meningkatkan *User experience* dalam menentukan anime yang menarik dan sesuai dengan preferensi user. Jadi user memiliki rekomendasi sesuai dengan genre atau anime yang disukai atau telah ditonton oleh user.

Pada proyek ini, dataset yang dipakai berasal dari situ web [Kaggle](https://www.kaggle.com/datasets/hernan4444/anime-recommendation-database-2020?select=anime.csv), dan dataset ini memiliki 17,562 data anime dan berdasarkan preferensi dari 325,772 pengguna

## Bussiness Understanding
<br>

### Problem Statements
- Bagaimana cara membuat sistem yang dapat merekomendasikan anime berdasarkan genre yang sama ?
- Bagaimana cara membuat sistem yang dapat merekomendasikan anime dari anime yang pernah kita lihat sebelumnya?


### Goals
- Mengetahui cara membuat sistem yang dapat merekomendasikan anime berdasarkan genre yang sama
- Mengetahui cara membuat sistem yang dapat merekomendasikan anime dar anime yang pernah kita lihat sebelumnya

### Solution Statements
Solusi yang saya pilih untuk menyelesaikan masalah ini adalah dengan menggunakan teknik *content-based filtering*, berikut adalah penjelasan teknik-teknik yang digunakan untuk masalah ini :

- **Content-based filtering** : adalah algoritma yang merekomendasikan anime serupa dengan apa yang disukai pengguna, berdasarkan tindakan mereka sebelumnya atau umpan balik eksplisit.
    
## Data Understanding
<br>

### Analisis Data Eksplorasi

Dataset yang saya pakai adalah [Anime Recommendation Database 2020](https://www.kaggle.com/datasets/hernan4444/anime-recommendation-database-2020?select=anime.csv) yang berisi informasi tentang preferensi dari 325,772 pengguna di 17,562 anime pada myanimelist.net, Analisis Data Eksplorasi mencakup proses kritis uji investigasi pendahuluan pada data untuk mengidentifikasi pola,menemukan anomali,menguji hipotesis, dan memeriksa asumsi melalui statistik ringkasan dan representasi visual.

- Dataset ini terdiri dari 17,562 baris data dan 35 kolom data untuk ``anime.csv`` namun diproyek ini saya hanya menggunakan 13 kolom saja, berikut penjelasannya :

    - MAL_ID - kode unik untuk mengindentifikasi setiap anime
    - Name - judul dari anime
    - Score - Rata-rata skor yang diberikan oleh user MAL
    - Genres - Genre dari anime
    - Episodes - Jumlah episode dari anime (1, jika movie atau spesial episode)
    - Producers - Producer yang membuat anime
    - Studios - Studio yang menggarap anime
    - Source - Sumber dari cerita anime
    - Rating - Rating dari anime
    - Ranked - Peringkat dari anime berdasarkan nilai skor
    - Popularity - Peringkat dari anime berdasarkan user menambahkan ke watchlist
    - Members - jumlah anggota komunitas yang ada di "grup" anime
    - Favorites - jumlah anggota komunitas yang menambahkan anime kedalam daftar favorit mereka

- Berikut adalah deskripsi dari dataset yang digunakan

    |      |     MAL_ID |       Score  |     Popularity | Members | Favorites |
    |------|--------------|---------------|-------------|---------|-----------|
    |count|  17562.000000 |  17562.000000 | 17562.000000|1.756200e+04          |17562.000000
    |mean|   21477.192347 |     4.604299  | 8763.452340 |3.465854e+04          |457.746270
    |std|    14900.093170 |     3.054669  | 5059.327278 |1.252821e+05	|4063.473313
    |min|        1.000000 |     0.000000  | 0.000000    |1.000000e+00	|0.000000
    |25%|     5953.500000 |     0.000000  | 4383.500000	|3.360000e+02	|0.000000
    |50%|    22820.000000 |     6.060000  | 8762.500000 |2.065000e+03	|3.000000
    |75%|    35624.750000 |     6.860000  | 13145.000000|1.322325e+04|31.000000
    |max|    48492.000000 |    9.190000   | 17565.000000|2.589552e+06|183914.000000

    Dari output di atas, dapat disimpulkan bahwa nilai maksimum score adalah 9,19 dan nilai minimumnya adalah 0. Artinya, skala score berkisar antara 0 hingga 10.
    Pada tahap ini, saya mengecek apakah ada nilai NaN, namun dataset ini tidak memiliki nilai NaN, kemudian saya mengubah tipe data pada kolom score menjadi float agar bisa divisualisasikan.

- Dataset ini tidak memiliki nilai NaN yang perlu dilakukan penanganan

    | Kolom           	    | Jumlah NaN 	|
    |-----------------	    |------------	|
    | MAL_ID            	    | 0          	|
    | Name            | 0          	|
    | Score       	| 0          	|
    | Genres  	| 0         	|
    | Episodes        	| 0         	|
    | Producers 	        | 0          	|
    | Studios       	| 0          	|
    | Source           | 0          	|
    | Rating           | 0          	|
    | Ranked           | 0          	|
    | Popularity           | 0          	|
    | Members           | 0          	|
    | Favorites         | 0             |

- Informasi yang bisa didapat dari hasil eksplorasi pada variabel pada ``anime.csv``

    <image src="https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/1.png" width=350 />

- Informasi yang saya dapat dari data diatas adalah :
    - Anime dengan tipe TV memiliki jumlah paling banyak dibandingkan dengan yang lain
    - Anime dengan tipe Music memiliki jumlah paling sedikit dibandingkan dengan yang lain
    <br>
    <br>

    <image src="https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/2.png" width=350 />

- Informasi yang saya dapat dari data diatas adalah :
    - Anime dengan rating PG-13 memiliki jumlah paling banyak dibandingkan dengan yang lain
    - Anime dengan tipe R+ memiliki jumlah paling sedikit dibandingkan dengan yang lain
    <br>
    <br>

    <image src="https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/3.png" width=350 />

- Informasi yang saya dapat dari data diatas adalah :
    - Banyak anime yang memiliki rentang nilai dari 6-7 dibandingkan dengan rentang yang lainnya.


## Data Preparation

Sebelum melakukan pembuatan model, perlu dilakukan data preparation, berikut adalah hal yang dilakukan pada proses data preparation

- **Drop Missing Value** : ini bertujuan untuk membersihkan data agar tidak ada data yang kosong, karena data kosong sangat mempengaruhi hasil akurasi dari model

- **Text Cleaning** : ini bertujuan untuk menghapus simbol ataupun teks yang tidak diperlukan dan mengubah semua huruf menjadi huruf kecil

## Modeling

Model yang saya gunakan pada data ini adalah dengan menggunakan teknik *content-based filtering*.
- Saya juga menggunakan ``TF-IDF Vectorizer`` untuk membangun sistem rekomendasi berdasarkan genre, dimana ``TF-IDF`` berfungsi untuk mengukur seberapa pentingnya suatu kata terhadap kata-kata lain dalam dokumen.
- Selanjutnya saya melakukan fit dan transformasi kedalam bentuk matriks, untuk menghitung derajat kesamaan antar anime, disini saya menggunakan teknik *cosine similarity*
- Berikut adalah hasil dari teknik *cosine similarity*
<image src="https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/4.png" width=350 />
<image src="https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/5.png" width=350 />

- Lalu setelah melakukan teknik *cosine similarity* dan muncul rekomendasi, maka saya mencoba membuat fungsi untuk meminta rekomendasi anime berdasarkan judul yang saya inputkan.
<image src="https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/6.png" width=350 />

- Dan berikut adalah hasil dari model *content-based filtering* :
<image src="https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/7.png" width=350 />

    Model berhasil memberikan rekomendasi 10 anime dengan genre yang sama seperti yang diharapkan.

## Evaluasi

- Hasil evaluasi *Content-based filtering* pada evaluasi model ini saya menggunakan metriks *precision*, berikut adalah hasil analisanya:

- Anime yang digunakan sebagai data uji coba adalah Inuyasha :
  <image src="https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/8.png" width=350 />

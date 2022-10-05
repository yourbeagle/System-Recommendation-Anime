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

        | Kolom           	    | Deskripsi 	|
        |-----------------	    |------------	|
        | MAL_ID            	| kode unik untuk mengindentifikasi setiap anime          	|
        | Name            | judul dari anime          	|
        | Score       	| Rata-rata skor yang diberikan oleh user MAL          	|
        | Year-Of-Publication  	| 0         	|
        | Publisher         	| 0         	|
        | Image-URL-S 	        | 0          	|
        | Image-URL-M       	| 0          	|
        | Image-URL-L           | 0          	|


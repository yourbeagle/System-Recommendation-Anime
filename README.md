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

Dataset yang saya pakai adalah [Anime Recommendation Database 2020](https://www.kaggle.com/datasets/hernan4444/anime-recommendation-database-2020?select=anime.csv) yang berisi informasi tentang preferensi dari 325,772 pengguna di 17,562 anime pada myanimelist.net, Analisis Data Eksplorasi mencakup proses kritis uji investigasi pendahuluan pada data untuk mengidentifikasi pola,menemukan anomali,menguji hipotesis, dan memeriksa asumsi melalui statistik ringkasan dan representasi visual.

- Dataset ini terdiri dari 17,562 baris data dan 35 kolom data untuk ``anime.csv`` namun diproyek ini saya hanya menggunakan 13 kolom saja, berikut penjelasannya :

    - MAL_ID - kode unik untuk mengindentifikasi setiap anime
    - Name - judul dari anime
    - Score - Rata-rata skor yang diberikan oleh user MAL
    - Genres - Genre dari anime
    - English Name - Nama lengkap anime dalam bahasa inggris
    - Japanese Name - Nama lengkap anime dalam bahasa jepang
    - Type - Tipe Anime (TV, OVA, ONA, Movie)
    - Episodes - Jumlah episode dari anime (1, jika movie atau spesial episode)
    - Aired - tanggal anime di tayangkan
    - Premiered - musim anime ditayangkan
    - Producers - Producer yang membuat anime
    - Studios - Studio yang menggarap anime
    - Source - Sumber dari cerita anime
    - Duration - durasi dari anime
    - Rating - Rating dari anime
    - Ranked - Peringkat dari anime berdasarkan nilai skor
    - Popularity - Peringkat dari anime berdasarkan user menambahkan ke watchlist
    - Members - jumlah anggota komunitas yang ada di "grup" anime
    - Favorites - jumlah anggota komunitas yang menambahkan anime kedalam daftar favorit mereka
    - Watching - jumlah anggota komunitas yang menonton anime tersebut
    - Completed - jumlah anggota komunitas yang sudah selesai menonton anime tersebut
    - On-Hold - jumlah anggota komunitas yang menaruh anime tersebut ke dalam daftar hold
    - Dropped - jumlah anggota komunitas yang menaruh anime tersebut ke dalam daftar tidak tertarik
    - Plan to Watch - jumlah anggota komunitas yang menaruh anime tersebut ke dalam daftar ingin ditonton
    - Score-10 - jumlah anggota komunitas yang memberi nilai 10
    - Score-9 - jumlah anggota komunitas yang memberi nilai 9
    - Score-8 - jumlah anggota komunitas yang memberi nilai 8
    - Score-7 - jumlah anggota komunitas yang memberi nilai 7
    - Score-6 - jumlah anggota komunitas yang memberi nilai 6
    - Score-5 - jumlah anggota komunitas yang memberi nilai 5
    - Score-4 - jumlah anggota komunitas yang memberi nilai 4
    - Score-3 - jumlah anggota komunitas yang memberi nilai 3
    - Score-2 - jumlah anggota komunitas yang memberi nilai 2
    - Score-1 - jumlah anggota komunitas yang memberi nilai 1

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

### Analisis Data Eksplorasi

#### Univariate Analysis
- Informasi yang bisa didapat dari hasil eksplorasi pada variabel pada ``anime.csv``

    ![image](https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/1.png)

    <em>Gambar 1. Univariate Analysis</em>

- Informasi yang saya dapat dari data diatas adalah :
    - Anime dengan tipe TV memiliki jumlah paling banyak dibandingkan dengan yang lain
    - Anime dengan tipe Music memiliki jumlah paling sedikit dibandingkan dengan yang lain
    <br>
    <br>

    ![image](https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/2.png)

    <em>Gambar 2. Univariate Analysis</em>

- Informasi yang saya dapat dari data diatas adalah :
    - Anime dengan rating PG-13 memiliki jumlah paling banyak dibandingkan dengan yang lain
    - Anime dengan tipe R+ memiliki jumlah paling sedikit dibandingkan dengan yang lain
    <br>
    <br>

    ![image](https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/3.png)

    <em>Gambar 3. Univariate Analysis</em>

- Informasi yang saya dapat dari data diatas adalah :
    - Banyak anime yang memiliki rentang nilai dari 6-7 dibandingkan dengan rentang yang lainnya.

#### Multivariate Analysis

 ![image](https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/12.png)

 <em>Gambar 4. Multivariate Analysis</em>

## Data Preparation

Sebelum melakukan pembuatan model, perlu dilakukan data preparation, berikut adalah hal yang dilakukan pada proses data preparation

- **Mengubah Tipe Data Score menjadi Float** : ini bertujuan agar data Score bisa ditampilkan, karena sebelumnya tipe datanya object

    ```
    anime_data['Score'] = anime_data['Score'].replace(['Unknown'],0)
    anime_data['Score'] = anime_data['Score'].astype('float')
    }
    ```

- **Drop Missing Value** : ini bertujuan untuk membersihkan data agar tidak ada data yang kosong, karena data kosong sangat mempengaruhi hasil akurasi dari model, disini saya membuang beberapa variabel yaitu 'English name','Japanese name', 'Aired', 'Premiered', 'Licensors', 'Duration', 'Watching', 'Completed', 'On-Hold', 'Dropped', 'Plan to Watch','Score-10','Score-9','Score-8','Score-7','Score-6','Score-5','Score-4','Score-3','Score-2','Score-1'


- **Text Cleaning** : ini bertujuan untuk menghapus simbol ataupun teks yang tidak diperlukan dan mengubah semua huruf menjadi huruf kecil

## Modeling

Model yang saya gunakan pada data ini adalah dengan menggunakan teknik *content-based filtering*.
- Saya juga menggunakan ``TF-IDF Vectorizer`` untuk membangun sistem rekomendasi berdasarkan genre, dimana ``TF-IDF`` berfungsi untuk mengukur seberapa pentingnya suatu kata terhadap kata-kata lain dalam dokumen.
- Selanjutnya saya melakukan fit dan transformasi kedalam bentuk matriks, untuk menghitung derajat kesamaan antar anime, disini saya menggunakan teknik *cosine similarity*
- Berikut adalah hasil dari teknik *cosine similarity*

    ![image](https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/4.png)

    <em>Gambar 5. Hasil dari Cosine Similarity</em>

    ![image](https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/13.png)

    

- Lalu setelah melakukan teknik *cosine similarity* dan muncul rekomendasi, maka saya mencoba membuat fungsi untuk meminta rekomendasi anime berdasarkan judul yang saya inputkan.
    ```
    get_anime_recommendations('overlord')
    ```

- Dan berikut adalah hasil 10 anime yang direkomendasikan dari model *content-based filtering* :
![image](https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/7.png)

    <em>Gambar 6. Hasil dari Content-based filtering</em> 

    Model berhasil memberikan rekomendasi 10 anime dengan genre yang sama seperti yang diharapkan.

## Evaluasi

- Hasil evaluasi *Content-based filtering* pada evaluasi model ini saya menggunakan metriks *precision*, berikut adalah hasil analisanya:

- Anime yang digunakan sebagai data uji coba adalah Inuyasha :
  ![image](https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/10.png)

- Hasil 10 anime yang direkomendasikan oleh model :

  ![image](https://raw.githubusercontent.com/yourbeagle/System-Recommendation-Anime/main/image/11.png)

- Untuk mengevaluasi model, saya menampung hasil rekomendasi kedalam variabel ``genre_recom`` kemudian membuat variabel ``get_recom_genre`` untuk menampung genre yang ada pada data uji yang selanjutnya akan dipakai pada evaluasi model

- Setelah itu saya melakukan perulangan berdasarkan genre pada data hasil rekomendasi dan melakukan implementasi dari formula precision

- Berikut adalah hasil dari formula precision

    | Genre           	    | Akurasi 	|
    |-----------------	    |------------	|
    | Action            	    | 100.0          	|
    | Adventure            | 100.0          	|
    | Comedy       	| 100.0          	|
    | Historical  	| 100.0         	|
    | Demons        	| 100.0         	|
    | Supernatural 	        | 100.0          	|
    | Magic       	| 100.0          	|
    | Romance           | 100.0          	|
    | Fantasy           | 100.0          	|
    | Shounen           | 100.0          	|
    
    Hasil yang diberikan cukup baik sehingga dari sini saya bisa mengetahui bahwa model yang saya kembangkan berjalan sesuai dengan yang saya inginkan

- Rumus Metriks Precision
 
$$ Precision = {tp \over tp+fp} $$

- Dimana :
    - TP = True Positives
    - FP = False Positives

### Kesimpulan
- Model terbaik, yaitu Content Based Filtering dapat memprediksi dengan akurasi hingga 100%
- Sistem rekomendasi dapat berjalan dengan baik, dimana sistem ini dapat memberikan rekomendasi anime yang sesuai dengan judul dan genre yang di minta oleh user
- Hasil prediksi mungkin akan lebih baik apabila data tidak memiliki nilai unknown yang banyak.

## Daftar Pustaka 

[1]M. N. uddin, J. Shrestha, and G.-S. Jo, “Enhanced content-based filtering using diverse collaborative prediction for movie recommendation,” 2009 First Asian Conference on Intelligent Information and Database Systems, 2009.

[2]W. Li, “Content-based anime recommendation,” Medium, 07-May-2021. [Online]. Available: https://medium.com/web-mining-is688-spring-2021/content-based-anime-recommendation-4d74038fab67. [Accessed: 05-Oct-2022].

[3]A. Jena, A. Jaiswal, D. Lal, S. Rao, A. Ayubi, and N. Sachdeva, “Recommendation system for anime using machine learning algorithms,” SSRN Electronic Journal, 2022.

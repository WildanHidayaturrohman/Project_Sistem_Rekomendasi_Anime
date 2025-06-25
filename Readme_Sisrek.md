# Laporan Proyek Machine Learning - Wildan Hidayaturrohman

## Project Overview

Industri hiburan digital mengalami pertumbuhan yang sangat pesat dalam beberapa dekade terakhir, termasuk di antaranya adalah industri animasi Jepang atau yang lebih dikenal dengan sebutan anime. Dengan ratusan judul yang dirilis setiap tahunnya dan ribuan judul yang telah tersedia di berbagai platform streaming, user seringkali mengalami kesulitan dalam menentukan anime mana yang sesuai dengan preferensi mereka. Situasi ini menimbulkan kebutuhan akan sistem rekomendasi yang mampu menyaring dan menyarankan judul-judul anime yang relevan dan diminati user.
Sistem rekomendasi menjadi solusi penting dalam membantu user menemukan konten yang sesuai dengan selera mereka tanpa harus mencarinya secara manual. Hal ini tidak hanya meningkatkan kenyamanan user, tetapi juga memberikan dampak signifikan terhadap pengalaman menonton dan loyalitas terhadap platform yang digunakan. Oleh karena itu, pengembangan sistem rekomendasi anime menjadi sangat penting dan relevan di era digital saat ini.
Berbagai pendekatan telah dikembangkan untuk membangun sistem rekomendasi yang efektif. Salah satu pendekatan yang telah terbukti memberikan hasil yang baik adalah metode User-Based Collaborative Filtering. Dalam penelitian yang dilakukan oleh I Kadek Gowinda dan kawan-kawan pada tahun 2023 menyatakan bahwa sistem rekomendasi anime yang dibangun menggunakan pendekatan user-based collaborative filtering yang dikombinasikan dengan Spearman Rank Correlation Coefficient untuk mengukur kesamaan antar user menunjukkan bahwa sistem yang dikembangkan mampu menghasilkan tingkat kesalahan yang cukup rendah, yaitu 15.8%, dan tingkat akurasi yang tinggi, yakni 84.12% [1]. Temuan ini membuktikan bahwa pendekatan tersebut cukup efektif dalam memberikan rekomendasi yang relevan bagi user.
Berdasarkan pentingnya kebutuhan user serta hasil penelitian sebelumnya yang mendukung efektivitas metode tertentu, proyek sistem rekomendasi anime ini akan dikembangkan dengan menggunakan 2 pendekatan yakni content based filtering dan collaborative filtering dengan tujuan untuk membantu user menemukan tontonan yang sesuai dengan minat mereka secara efisien dan personal.

## Business Understanding

Seiring dengan pesatnya pertumbuhan industri hiburan digital, khususnya animasi Jepang (anime), user dihadapkan pada jumlah pilihan yang sangat besar. Banyaknya judul yang tersedia membuat user kesulitan dalam menentukan anime yang sesuai dengan preferensi pribadi mereka. Tanpa bantuan sistem rekomendasi yang tepat, user dapat kehilangan waktu dalam pencarian atau bahkan melewatkan anime yang relevan dengan minat mereka.
Selain itu, platform penyedia anime yang tidak menyediakan rekomendasi yang dipersonalisasi berpotensi kehilangan engagement user karena tidak mampu menyajikan pengalaman yang sesuai secara individual.

### Problem Statements

Masalah utama yang ingin diselesaikan dalam proyek ini adalah:
- Bagaimana membangun sistem rekomendasi anime yang dapat memberikan hasil relevan sesuai preferensi user?
- Bagaimana membangun sistem rekomendasi anime yang dapat memberikan hasil relevan sesuai genre anime yang ditonton user?

### Goals

Tujuan dari proyek ini adalah:
- Membangun sistem rekomendasi anime yang dapat menyajikan 10 daftar tontonan yang relevan berdasarkan preferensi dan riwayat interaksi user.
- Mengembangkan sistem yang mampu merekomendasikan 10 anime berdasarkan kesamaan genre dari anime yang pernah ditonton oleh user.

### Solution statements

Untuk mencapai tujuan yang telah ditetapkan, proyek ini menerapkan dua pendekatan algoritmik dalam membangun sistem rekomendasi anime, yaitu:

1. Content-Based Filtering

Pendekatan Content-Based Filtering kali ini adalah merekomendasikan anime kepada user berdasarkan kemiripan konten antara anime yang telah disukai atau ditonton sebelumnya dengan anime lainnya. Sistem akan memanfaatkan fitur genre untuk membangun profil preferensi user, kemudian mencocokkannya dengan anime lain yang memiliki karakteristik serupa.

2. Collaborative Filtering

Pendekatan Collaborative Filtering kali ini akan memberikan rekomendasi dengan melihat kesamaan pola perilaku antar user. Sistem akan menganalisis user lain yang memiliki selera serupa, kemudian merekomendasikan anime yang disukai oleh user-user tersebut tetapi belum ditonton oleh user target.

## Data Understanding

Data yang diperoleh memiliki 2 dataset yakni anime.csv dan rating.csv. Pada anime.csv terlihat bahwa dataset memiliki 12294 baris dan 7 kolom yakni anime_id, name, genre, type, episodes, rating dan members. Ini mengandung makna bahwa dataset pada anime.csv berjumlah 12294. Sedangkan pada rating.csv, terlihat bahwa dataset memiliki 7813737 baris dan 3 kolom yakni user_id, anime_id dan rating. Ini mengandung makna bahwa dataset pada rating.csv berjumlah 7813737. Selanjutnya dataset anime.csv disimpan dalam dataframe anime_df dan dataset dari rating.csv disimpan dalam dataframe rating_df.
Tautan dataset: https://www.kaggle.com/datasets/CooperUnion/anime-recommendations-database

Variabel-variabel pada dataset anime.csv adalah sebagai berikut:
- anime_id : merupakan id unik setiap anime yang mengidentifikasikan suatu anime.
- name : merupakan judul lengkap suatu anime.
- genre : merupakan daftar genre ysng dipisahkan oleh koma.
- type : merupakan jenis anime seperti Movie, TV, OVA, Special, Music dan ONA.
- episodes : merupakan episode dalam anime tersebut.
- rating : merupakan rate rata-rata dari user yang diberikan untuk setiap anime.
- members : merupakan jumlah anggota komunitas yang tergabung dalam setiap animee.

Variabel-variabel pada dataset rating.csv adalah sebagai berikut:
- user_id : merupakan id unik user yang dibuat secara acak.
- anime_id : merupakan id unik setiap anime yang mengidentifikasikan suatu anime.
- rating : merupakan rate yang diberikan setiap user pada suatu anime (-1 jika user menonton anime namun tidak memberi rating).

### Univariate exploratory data analysis

1. anime_df

Univariate EDA dilakukan untuk lebih memahami isi didalam setiap dataset dengan melihat info, parameter statistiknya dan lain-lain. Berdasarkan anime_df.info(), diperoleh bahwa fitur anime_id memiliki jumlah data sebanyak 12294 dengan type datanya adalah int64, name memiliki jumlah data sebanyak 12294 dengan type datanya adalah object, genre memiliki jumlah data sebanyak 12232 dengan type datanya adalah object, type memiliki jumlah data sebanyak 12269 dengan type datanya adalah object, episodes memiliki jumlah data sebanyak 12294 dengan type datanya adalah object, rating memiliki jumlah data sebanyak 12064 dengan type datanya adalah float64 dan members memiliki jumlah data sebanyak 12294 dengan type datanya adalah int64.
Berdasarkan hasil dari anime_df.describe(), diperoleh bahwa nilai rating berada pada rentang 1.67 sampai 10. Ini berarti bahwa nilai maximal rating yang ada adalah 10. Selanjutnya, setelah dilakukan pengecekan judul atau name unik dan typenya, terlihat bahwa nama atau judul anime secara keseluruhan adalah 12292 dan type anime adalah 6 type yakni Movie, TV, OVA, Special, Music, ONA dan ada pula baris yang kosong. Setelah melihat jumlah judul unik dan typenya, kemudian dilihat pula berapa banyak jumlah genre yang ada. Terlihat bahwa ada 44 kategori genre, kita ketahui pula bahwa satu anime dapat memiliki beberapa genre yang dipisahkan oleh tanda ", " sesuai pada dataframe anime_df. Dimana daftar genre yang ada secara keseluruhan adalah: ['Drama', 'Romance', 'School', 'Supernatural', 'Action', 'Adventure', 'Fantasy', 'Magic', 'Military', 'Shounen', 'Comedy', 'Historical', 'Parody', 'Samurai', 'Sci-Fi', 'Thriller', 'Sports', 'Super Power', 'Space', 'Slice of Life', 'Mecha', 'Music', 'Mystery', 'Seinen', 'Martial Arts', 'Vampire', 'Shoujo', 'Horror', 'Police', 'Psychological', 'Demons', 'Ecchi', 'Josei', 'Shounen Ai', 'Game', 'Dementia', 'Harem', 'Cars', 'Kids', 'Shoujo Ai', nan, 'Hentai', 'Yaoi', 'Yuri'].

2. rating_df

Sama halnya dengan apa yang dilakukan pada anime_df, rating_df pula akan dilakukan EDA untuk lebih memahami isi dataset. Dari rating_df.info() dan rating_df.describe(), dapat diketahui bahwa rating.csv memiliki 3 fitur yakni user_id dengan type data int64 dan berjumlah 7813737, anime_id dengan type data int64 dan berjumlah 7813737 serta rating dengan type data int64 dan berjumlah 7813737. Pada fitur rating pula, diketahui bahwa rating terkecil dimulai dari -1(rating yang digeneralisasi jika user menonton anime tersebut namun tidak memberikan rating) hingga 10.

## Data Preparation

### Pengecekan Missing Value dan Duplikat serta Penanganannya pada Masing-masing Data

Pengecekan missing value dan duplikat merupakan tahap penting dalam proses pra-pemrosesan data untuk memastikan kualitas dan kebersihan dataset yang digunakan dalam pembangunan sistem rekomendasi anime. Missing value atau nilai kosong dapat menyebabkan error saat pelatihan model, terutama dalam algoritma machine learning yang tidak dapat menangani data yang tidak lengkap. Selain itu, informasi yang hilang seperti genre, rating, atau identitas user dapat mengurangi akurasi sistem rekomendasi, karena model tidak memiliki cukup informasi untuk mempelajari preferensi atau kemiripan antar item. Oleh karena itu, penanganan missing value biasanya dilakukan dengan menghapus data yang tidak lengkap jikalau data yang dimiliki berjumalh besar.
Sementara itu, data duplikat dapat menyebabkan bias dalam sistem rekomendasi karena akan membuat model menganggap satu entitas lebih penting dari yang seharusnya. Misalnya, jika satu anime atau satu interaksi user tercatat dua kali, sistem bisa memberikan bobot berlebih pada data tersebut, sehingga hasil rekomendasi menjadi tidak seimbang. Penanganan data duplikat dilakukan dengan menghapus baris yang identik. Dengan membersihkan missing value dan duplikat, proses analisis dan pelatihan model dapat berjalan lebih optimal dan menghasilkan sistem rekomendasi yang lebih akurat dan andal.

1. Pengecekan

Dengan kode anime_df.isnull().sum(), rating_df.isnull().sum(), anime_df.duplicated().sum() dan rating_df.duplicated().sum(), diperoleh bahwa anime_df memiliki beberapa missing value dan 0 duplikat data. Terlihat pula bahwa rating_df tidak memiliki missing value dan terdapat 1 duplikat data. Dimana missing value terjadi pada fitur genre sebanyak 62, fitur type sebanyak 25 dan fitur rating pada anime_df sebanyak 230. Selanjutnya dengan mengecek irisan missing value setiap fitur, diperoleh bahwa missing value pada setiap kolom ternyata memiliki beberapa irisan dengan kolom lain. Hal itu terlihat dari pengecekan dimana missing value pada kolom 'genre' dan 'type': 3, missing value pada kolom 'genre' dan 'rating': 15, missing value pada kolom 'type' dan 'rating': 25 dan missing value pada kolom 'genre', 'type', dan 'rating': 3. Selanjutnya dengan melihat jumlah baris yang memiliki missing value, diperoleh bahwa baris-baris yang memiliki missing value hanya berjumlah 277. Baris-baris ini yang nantinya akan dilakukan penanganan.

2. Penanganan

Karena pada data understanding sebelumnya diketahui bahwa dataset memiliki jumlah yang besar, maka penanganan missing value dan duplikat data pada kali ini adalah dengan menggunakan teknik droping. Dengan menggunakan kode anime_df.dropna(axis = 0, inplace = True) dan rating_df.drop_duplicates(inplace=True), maka missing value dari anime_df dan duplikat dari rating_df sudah 0. Setelah dilakukan penanganan pada anime_df dan rating_df, maka diperoleh jumlah data dengan kode anime_df.info() dan rating_df.info() yakni pada anime_df untuk setiap fiturnya adalah sebanyakn 12017 dan jumlah data pada rating_df untuk setiap fiturnya adalah 7813736.
Pada Univariate EDA sebelumnya, diketahui bahwa jumlah judul anime adalah 12292, sedangkan setelah dilakukan penanganan duplikat dan missing value, jumlah name atau judul anime pada anime_df berjumlah 12017. Hal ini memiliki sedikit keanehan, karena ketika jumlah judul 12292 dan dilakukan penanganan missing value sebanyak 277, maka seharusnya data akhir berjumlah 12015. Ini memiliki arti terdapat indikasi duplikat pada judul. Selanjutnya dengan melihat judul anime yang tidak unik, diperoleh bahwa name yang sama sebanyak 2 name dengan masing-masing memiliki 1 name yang sama. Namun terlihat pula bahwa type dari anime tersebut berbeda, ini menandakan bahwa jenis berbeda walaupun tetap satu anime yang sama. Jadi dari indikasi sebelumnya dapat disimpulkan bahwa data tidak memiliki keanehan karena walaupun memiliki judul yang sama, namun berbeda jenis.

### Data Preprocessing

Tahapan data preparation sangat diperlukan dalam proyek dalam pengembangan sistem rekomendasi anime, karena kualitas data secara langsung memengaruhi performa dan akurasi model yang dibangun. Data yang diperoleh dari sumber awal biasanya belum siap untuk digunakan dalam analisis atau pelatihan model karena masih mengandung nilai kosong (missing values), duplikat, format yang tidak konsisten, atau fitur yang tidak relevan. Oleh karena itu, data perlu dibersihkan, ditata ulang, dan disiapkan agar dapat diolah secara efisien dan memberikan hasil yang bermakna. Dalam konteks sistem rekomendasi, data preparation membantu membentuk struktur data yang tepat untuk mendeteksi pola preferensi user, kesamaan antar item, serta hubungan antar user. Proses ini mencakup berbagai langkah penting, menggabungkan beberapa sumber data, menghapus missing value dan duplikat data dan lain-lain.
Untuk mempersiapkan data ke tahap modeling, maka dilakukan penggabungan data berdasarkan kesamaan anime_id dan mengubah nama kolom rating pada rating_df menjadi rating_user. Selanjutnya hasil dari penggabungan dan perubahan nama fitur tersebut disimpan dalam dataset bernama alldata_df.

### Mempersiapkan Data untuk Model Content Based Filtering

1. Pengecekan deskripsi alldata_df

Pengecekan deskripsi alldata_df sangat penting, pentingnya pengecekan ini terletak pada fungsinya untuk memastikan bahwa proses penggabungan data telah berhasil dilakukan tanpa menyebabkan ketidaksesuaian atau anomali, seperti ketidaksesuaian tipe data dan lain-lain. Dengan mengecek deskripsi pula, kita bisa melihat nilai minimum dan maksimum, nilai rata-rata, standar deviasi, serta jumlah data yang hilang pada setiap kolom. 
Dengan kode alldata_df.info() dan alldata_df.describe(), diperoleh bahwa jumlah data untuk setiap fitur sama dan pada fitur rating minimalnya adalah 1.67 dan maksimalnya 9.5, namun pada fitur rating_user, minimalnya adalah -1 dan maksimalnya adalah 10 dengan -1 berarti user tersebut tidak memberikan rating untuk anime yang ditonton. Ini bukan suatu permasalahan, karena fitur rating adalah rate untuk judul anime dengan type tertentu secara keseluruhan, sedangkan rating_user adalah rating yang diberikan setiap user untuk anime yang ditonton.

2. Pengecekan missing value dan duplikat pada alldata_df

Setelah proses penggabungan data, sangat umum terjadi masalah seperti nilai kosong pada kolom yang berasal dari salah satu tabel yang tidak memiliki pasangan yang sesuai. Misalnya, user yang belum memberikan rating pada anime tertentu atau anime yang tidak memiliki informasi genre. Jika missing value ini tidak ditangani, bisa menyebabkan model kesulitan mengenali pola preferensi atau bahkan gagal diproses oleh algoritma tertentu. Selain itu, data duplikat juga dapat muncul akibat penggabungan yang tidak presisi, seperti kesalahan pada penggabungan berdasarkan kunci yang tidak unik. Maka pengecekan missing value dan duplikat pada alldata_df sangat diperlukan.
Dengan kode alldata_df.isnull().sum() dan alldata_df.duplicated().sum() diperoleh bahwa alldata_df tidak memiliki missing value dan data yang duplikat.

3. Pengecekan jenis genre dari data yang telah digabungkan

Pengecekan jenis genre dari data yang telah digabungkan sangat diperlukan, karena setelah dilakukan penanganan dengan menghapus data duplikat dan kososng, maka banyak data akan hilang. Genre pula menjadi salah satu topik yang akan digunakan untuk merekomendasikan anime. Maka, pengecekan jenis genre dan menyimpan listnya dalam suatu dataframe sangat diperlukan untuk modeling nanti.
Dari hasil pengecekan diperoleh bahwa bahwa jenis genre tidak memiliki keanehan dan sudah benar. Perbedaan yang ada hanya jumlah genre pada data yang telah dilakukan penggabungan serta penanganan missing value dan duplikat berjumlah 43, namun jumlah genre di data awal anime_df adalah 44. Ini tidak memiliki indikasi adanaya keanehan, karena setelah dilakukan penanganan, maka beberapa data awal telah dil;akukan penghapusan yang mengakibatkan jumlah genrenya menjadi berkurang 1. Adapun daftar genre yang ada secara keseluruhan adalah: ['Drama', 'Romance', 'School', 'Supernatural', 'Action', 'Adventure', 'Fantasy', 'Magic', 'Military', 'Shounen', 'Comedy', 'Historical', 'Parody', 'Samurai', 'Sci-Fi', 'Thriller', 'Sports', 'Super Power', 'Space', 'Slice of Life', 'Mecha', 'Music', 'Mystery', 'Seinen', 'Martial Arts', 'Vampire', 'Shoujo', 'Horror', 'Police', 'Psychological', 'Demons', 'Ecchi', 'Josei', 'Shounen Ai', 'Game', 'Dementia', 'Harem', 'Cars', 'Kids', 'Shoujo Ai', 'Hentai', 'Yaoi', 'Yuri'].

4. Mengambil data dari user dengan minimal nonton 1000 anime dan rating >= 7

Untuk mendapatkan rekomendasi yang lebih baik, akan lebih baik mengambil data hanya dari user dengan pengetahuan anime cukup mumpuni. Ini dapat dilihat dari seberapa banyak user tersebut menonton dan memberi rating pada anime yang ditonton. Akan diambil user dengan minimal 1000 interaksi yang dimana ini akan memperkuat kemungkinan bahwa user tersebut sudah menonton banyak jenis anime dari berbagai genre. Hal ini dilakukan karena dimisalkan jika hanya mengambil user dengan jumlah interaksi < 100, maka ada kemungkinan bahwa user tersebut hanya menonton 2 sampai 3 anime dan interaksi tersebut dihasilkan dari setiap episode yang dia rating. Untuk lebih memberikan rekomendasi yang lebih baik, maka hanya akan diambil data dengan rating >= 7. Ini dilakukan agar anime yang direkomendasikan memiliki nilai yang cukup dikatakan bagus dan layak untuk direkomendasikan.
Setelah dilakukan filtering berdasarkan jumlah kemunculan user dan ratingnya, maka dataset berjumlah 134306.

5. Mengonversi data series menjadi list

Untuk membuat rekomendasi berdasarkan genre, maka akan disiapkan datanya yang mencakup fitur name, genre, type dan episodes. List ini sangat penting untuk mempersiapkan data pada proses modeling nanti. Dengan memiliki list pada fitur name, genre, type dan episodes yang merupakan komponen inti dalam melakukan rekomendasi berdasarkan genre, nantinya list tersebut akan digabungkan. Setelah membuat list untuk setiap fitur yang akan digunakan, terlihat bahwa jumlah data masing-masing fitur masih berjumlah 134306.

6. Membuat dictionary untuk rekomendasi berdasarkan genre

Pada tahap ini fitur-fitur name, genre, type dan episodes akan digabungkan dalam dataframe bernama genre_base. Penggabungan ini sangat diperlukan, karena data dari hasil penggabungan ini akan menjadi acuan untuk melakukan rekomendasi berdasarkan genre nanti. Diketahui pula bahwa setelah digabungkan, data berjumlah 134306.

7. Pengecekan dan penanganan duplikat dari dataframe baru yakni genre_base yang akan dirujuk untuk membuat rekomendasi

Setelah proses penggabungan atau ekstraksi genre dari data anime, sangat umum terjadi duplikasi entri dalam genre_base, terutama jika satu anime tercatat lebih dari sekali. Jika data duplikat ini tidak ditangani, maka sistem rekomendasi berbasis genre dapat menjadi tidak efisien. Maka proses ini sangat diperlukan untuk meningkatkan kualitas data.
Setelah dilakukan pengecekan, terlihat bahwa genre_base memiliki sangat banyak data duplikat yakni sebanyak 130951. Ini dikarenakan data sebelumnya memiliki fitur user_id dan rating yang memungkinkan ada banyak sekali user yang memberi rating pada satu anime dan episode yang sama. Hal itu tidak dikategorikan menjadi data duplikat karena penonton atau usernya berbeda. Adapula fitur rating, jikalau user memberikan rating yang berbeda pada satu anime dan episode yang sama, maka ini tetap tidak dapat dikatakan duplikat karena perbedaan dari rating yang diberikan. Namun pada dataframe genre_base, hanya diambil fitur judul, genre, jenis dan episode atau pada data sebelumnya bernama name, genre, type, episodes. Maka pastinya data memiliki banyak duplikat karena user_id dan rating telah dihilangkan.
Selanjutnya, dilakukan penanganan terhadap data duplikat tersebut dengan melakukan teknik droping. Setelah dilakukan penanganan terhadap data duplikat, maka data menjadi berjumlah 3355.

8. TF-IDF Vectorizer

TF-IDF Vectorizer digunakan untuk mengubah informasi genre yang berbentuk teks menjadi bentuk numerik yang bisa dihitung kemiripannya menggunakan algoritma seperti cosine similarity.
Setelah dilakukan TF-IDF Vectorizer, terlihat bahwa matriks yang dimiliki berukuran (3355, 43). Nilai 3355 merupakan ukuran data dan 43 merupakan matrik genre. Selanjutnya vektor TF-IDF telah diubah ddalam bentuk matriks dengan fungsi todense(). Selanjutnya, dibuat dataframe untuk matriks TF-IDF dengan kolom diisi dengan genre dan baris diisi dengan 'judul', 'episode', dan 'jenis'. Output dataframe matriks tfidf ini adalah kecocokan judul, episode dan type berdasarkan genre. Contohnya adalah (Kirarin☆Revolution, 153, TV) yang memiliki nilai 0.443141 pada genre drama. Ini mengandung arti bahwa (Kirarin☆Revolution, 153, TV) memiliki genre drama dan seterusnya.

### Mempersiapkan Data untuk Model Collaborative Filtering

Pada proses sebelumnya, kita sudah memiliki data yang telah dilakukan penggabungan dengan nama alldata_df. Maka akan dilakukan preparation data dari data tersebut.

1. Menghapus rating_user < 0 dan mengambil data dari user dengan minimal interaksi 1000

Pada sebelumnya, kita ketahui bahwa rating_user -1 adalah rating yang digeneralisasi untuk user yang nonton anime namun tidak memberikan rating. Maka hal itu tidak akan dijadikan acuan dalam rekomendasi dan akan dihapus. Dengan kode alldata_df = alldata_df[alldata_df['rating_user'] >= 0]. Maka diperoleh bahwa rating_user setelah dilakukan penanganan memiliki minimal rating 1.
Selanjutnya, jika diambil data walaupun hanya 1 interaksi, maka itu akan kurang untuk rekomendasi. Hal ini dikarenakan data yang diperoleh dari user tersebut kurang merepresentasikan apa yang disukai oleh user karena hanya menonton 1 episode anime. Itu akan mengurangi akurasi model. Kenyataannya, biasanya dalam 1 anime memiliki sekitar 24 episode untuk 1 season dan biasanya memiliki beberapa season. Jikalau user tersebut hanya melakukan interaksi terhadap 1 anime dengan beebrapa season, maka itu akan tetap kurang merepresentasikan data dari user tersebut. Maka akan diambil data dari user dengan minimal interaksi 1000. Setelah mengambil data dari user dengan minimal interaksi 1000, diperoleh bahwa jumlah data menjadi 218718.

2. Mengambil user_id unik dan melakukan encoding

Proses ini dibuat agar sistem dapat mengenali atau memproses hubungan antar user dan anime secara efektif. Karena tanpe encoding, model akan kesulitan mengenali user_id. Setelah user_id dipetakan kedalam integer 0 sampai dengan banyaknya jumlah user_id, maka hal ini menghasilkan encoding dengan contoh user_id 1497 menjadi 0 dan seterusnya. Hasil dari proses ini disimpan dalam variabel user_to_user_encoded.

3. Mengambil judul atau name unik dan melakukan encoding

Sama halnya dengan user_id, judul atau name pula perlu dilakukan encoding agar model dapat mengenalinya. Setelah name dipetakan kedalam integer 0 sampai dengan banyaknya jumlah judul, maka hal ini menghasilkan encoding dengan contoh name Kimi no Na wa. menjadi 0 dan seterusnya. Hasil dari proses ini disimpan dalam variabel name_to_encoded.

4. Memetakan user_id dan name ke dataframe yang berkaitan

Pada proses sebelumnya, kita memiliki variabel yang menyimpan setiap proses tersebut. Maka selanjutnya adalah memetakan user_id dengan name pada dataframe yang berkaitan dimana pada hal ini adalah alldata_df. Hasil mapping pada user_id dan name diberi nama fitur user dan judul.

5. Cek jumlah user, jumlah judul, dan mengubah nilai rating_user menjadi float

Mengecek jumlah user dan judul penting untuk memahami ruang masalah dan kualitas data. Mengonversi nilai rating_user ke float memastikan keakuratan pemrosesan numerik, mencegah error, dan memungkinkan model menghitung prediksi secara tepat. Dari hasil pengecekan, diperoleh jumlah user_id: 165, Jumlah Judul: 9186, Min Rating: 1.0 dan Max Rating: 10.0.

6. Mempersiapkan data untuk rekomendasi

Dari data kita ketahui bahwa user telah memberi rating pada beberapa judul anime yang telah mereka tonton. Rating ini digunakan untuk membuat rekomendasi anime yang mungkin cocok untuk user. Judul yang akan direkomendasikan tentulah judul yang belum pernah ditonton oleh user. Maka dari itu, disini dibuat data anime yang belum pernah ditonton oleh setiap user dan melakukan encoding terhadap anime_id.

7. Membagi data

Sebelum membagi data, maka dilakukan pengacakan terhadap data terlebih dahulu. Mengacak dataset sebelum pembagian sangat penting untuk menghindari bias, menjamin keberagaman data, dan menghasilkan model yang lebih general. 
Pada kali ini, dataset di split dengan metode 80:20 dimana 80% untuk data train dan 20% untuk data validasi. Dilain sisi, dataset juga disimpan dalam variabel x yang berisi data user dan judul serta variabel y atau target yang berisi data rating_user.

## Modeling

### Modeling dengan Content Based Filtering

Content-Based Filtering adalah pendekatan dalam sistem rekomendasi yang merekomendasikan item kepada user berdasarkan karakteristik atau atribut dari item itu sendiri. Dalam konteks sistem rekomendasi anime, pendekatan ini dilakukan dengan menganalisis fitur-fitur konten dari anime, seperti genre, sinopsis, atau rating, lalu mencocokkannya dengan preferensi user yang diperoleh dari anime yang pernah ditonton atau disukai sebelumnya. Pada proyek ini, sistem rekomendasi berbasis genre menggunakan Content-Based Filtering dengan fokus pada kesamaan genre antar anime. Artinya, jika seorang user menonton atau menyukai anime bergenre action, maka sistem akan merekomendasikan anime lain yang memiliki genre serupa, seperti action, adventure, atau genre yang sering muncul bersamaan.

**Kelebihan:**

- Personalisasi yang Tinggi.
- Tidak Memerlukan Data User Lain.
- Transparansi dan Interpretabilitas karena merekomendasikan anime dengan jelas berdasarkan kesamaan genre.

**Kekurangan:**

- Rekomendasi Terlalu Mirip sehingga kurang eksploratif.
- Keterbatasan Fitur karena hanya merekomendasikan sesuai genre saja.
- Tidak memanfaatkan wawasan dari user lain.

Adapun proses dalam pembuatan rekomendasi adalah sebagai berikut:

1. Cosine Similarity

Cosine Similarity adalah metode yang digunakan untuk mengukur tingkat kemiripan antara dua vektor berdasarkan sudut kosinus di antara keduanya. Nilai cosine similarity berada dalam rentang 0 hingga 1, dimana rumusnya adalah cos(tetha) = perkalian dot product antara vektor A dan B dibagi dengan norm atau panjang vektor A dikali norm atau panjang vektor B.
Dari dataframe matriks tfidf sebelumnya, dibuat dataframe matriks cosine similarity dengan nama osine_sim_df dimana matriks ini digunakan untuk mengukur kesamaan setiap anime dengan anime lain. Jumlah Shape: (3355, 3355) memiliki arti bahwa matriks cosine similarity memiliki ukuran 3355*3355 dengan 3355 adalah jumlah judul anime. Lalu membuat dataframe dari variabel cosine_sim dengan baris dan kolom berupa judul dan berisi nilai kecocokan setiap judul.

2. Membuat fungsi rekomendasi judul anime berdasarkan kesamaan genre untuk Content Based Filtering

Pada tahap ini, dibuat sebuah fungsi anime_recommendations yang meminta inputan (judul, similarity_data=cosine_sim_df, items=genre_base[['judul', 'genre']], k=10). Pada fungsi ini, telah ditetapkan similarity data dengan osine_sim_df serta item dengan isian judul dan genre dari dataframe genre_base dan jumlah anime yang direkomendasikan atau k sebesar 10. Isi dari fungsi tersebut adalah mengambil data dengan menggunakan argpartition untuk melakukan partisi secara tidak langsung sepanjang sumbu yang diberikan, mengambil data dengan similarity terbesar dari index yang ada dan drop judul anime yang ingin dicari kemiripannya.

3. Mendapatkan rekomendasi

Selanjutnya dengan kode genre_base[genre_base.judul.eq('Death Note')], diketahui isi dari anime target yang akan dicari rekomendasinya adalah sebagai berikut:

judul	genre	                                                      jenis	episode
3761	Death Note	Mystery, Police, Psychological, Supernatural, ...	TV	37

Dengan memanggil fungsi anime_recommendations('Death Note'), maka diperoleh top 10 anime yang mirip dengan Death Note seperti:
    judul	                            genre
1	Death Note Rewrite	Mystery,        Police, Psychological, Supernatural, ...
2	Mousou Dairinin	                    Drama, Mystery, Police, Psychological, Superna...
3	Higurashi no Naku Koro ni Kai	    Mystery, Psychological, Supernatural, Thriller
4	Higurashi no Naku Koro ni Rei	    Comedy, Mystery, Psychological, Supernatural, ...
5	Mirai Nikki (TV)	                Action, Mystery, Psychological, Shounen, Super...
6	Monster	                            Drama, Horror, Mystery, Police, Psychological,...
7	Higurashi no Naku Koro ni	        Horror, Mystery, Psychological, Supernatural, ...
8	Imawa no Kuni no Alice (OVA)	    Action, Psychological, Shounen, Supernatural, ...
9	Zankyou no Terror	                Psychological, Thriller
10	Yakushiji Ryouko no Kaiki Jikenbo	Mystery, Police, Supernatural

### Modeling dengan Collaborative Filtering

Collaborative Filtering adalah salah satu pendekatan paling populer dalam membangun sistem rekomendasi. Alih-alih menggunakan atribut konten dari item seperti genre, Collaborative Filtering mengandalkan perilaku user, misalnya rating atau interaksi user terhadap item untuk memberikan rekomendasi. Dalam proyek sistem rekomendasi anime kali ini, Collaborative Filtering digunakan untuk merekomendasikan anime kepada user berdasarkan riwayat rating user lain yang memiliki preferensi serupa.

**Kelebihan:**

- Tidak Memerlukan Informasi Detail tentang Item.
- Menangkap Preferensi Tersembunyi.
- Fleksibel dan Personal

**Kekurangan:**

- Tidak bisa memberikan rekomendasi untuk user baru atau user yang tidak memberikan rating pada anime.
- Untuk sistem dengan jutaan user dan item, perhitungan kemiripan bisa sangat mahal secara komputasi.
- Sistem cenderung merekomendasikan anime populer yang banyak diberi rating, sehingga anime unik atau kurang dikenal bisa terlewat.

Adapun proses dalam pembuatan rekomendasi adalah sebagai berikut:

1. Menghitung kecocokan user dan judul dengan teknik embedding

Proses pada model RecommenderNet dimulai dengan melakukan embedding terhadap data pengguna (user) dan item (judul). Embedding ini berfungsi untuk mengubah masing-masing ID pengguna dan judul menjadi vektor berdimensi tetap (embedding_size) yang dapat menangkap karakteristik laten dari masing-masing entitas. Pada tahap ini, terdapat dua embedding untuk masing-masing entitas: satu embedding utama yang menghasilkan vektor representasi dan satu embedding tambahan yang menyimpan bias (nilai skalar) untuk masing-masing pengguna dan judul. Setelah embedding diperoleh, dilakukan operasi dot product (perkalian titik) antara vektor embedding pengguna dan judul. Operasi ini menghasilkan skor kecocokan yang mencerminkan seberapa besar kemungkinan seorang pengguna menyukai atau berinteraksi dengan item tertentu. Nilai ini kemudian ditambahkan dengan bias pengguna dan bias judul yang masing-masing bertujuan untuk menyesuaikan skor dengan kecenderungan preferensi pengguna secara umum serta popularitas item secara umum. Hasil akhirnya kemudian diterapkan melalui fungsi aktivasi sigmoid, yang mengubah skor tersebut ke dalam rentang [0, 1]. Model ini diimplementasikan sebagai subclass dari tf.keras.Model, memungkinkan fleksibilitas dalam pengembangan arsitektur dan pelatihan model rekomendasi yang lebih kompleks ke depannya.

2. Mendefinisikan model

Pada proses ini, model RecommenderNet dikompilasi menggunakan Binary Crossentropy sebagai fungsi loss karena model dirancang untuk menyelesaikan masalah klasifikasi biner, yaitu memprediksi apakah seorang pengguna akan menyukai atau berinteraksi dengan suatu item. Fungsi aktivasi sigmoid pada output model memastikan hasil prediksi berada dalam rentang [0, 1], sehingga sangat cocok dipadukan dengan Binary Crossentropy yang menghitung seberapa baik model membedakan antara kelas 0 dan 1. Sebagai optimizer, digunakan Adam (Adaptive Moment Estimation) karena optimizer ini bekerja sangat baik pada skala data yang cukup besar seperti pada kasus ini, seperti yang telah dijelaskan pada data preparation untuk Collaborative Filtering sebelumnya. Adam menggabungkan kelebihan dari RMSProp dan Momentum, mampu beradaptasi terhadap parameter dan memberikan konvergensi cepat serta stabil meskipun pada dimensi embedding tinggi. Learning rate sebesar 0.001 dipilih sebagai titik awal yang umum dan stabil untuk sebagian besar kasus. Untuk evaluasi performa model selama pelatihan, digunakan Root Mean Squared Error (RMSE). Selain itu, diterapkan juga callbacks yang memungkinkan pelatihan dihentikan lebih awal jika akurasi sudah melewati 90%.

3. Training model

Selanjutnya, dilakukan training model dengan 100 epoch dan 8 batch_size serta menerapkan callback yang telah didefinisikan. Dari proses training terlihat bahwa model terhenti di epoch 100 karena nilai akurasi kurang dari 90%, maka dari itu callback tidak dijalankan.

4. Mendapatkan rekomendasi

Selanjutnya, diperoleh rekomendasi dari user dengan user_id 58064 seperti berikut:

Anime with high ratings from user
--------------------------------
Mobile Suit Gundam 00 : Action, Drama, Mecha, Military, Sci-Fi, Space
Toki wo Kakeru Shoujo : Adventure, Drama, Romance, Sci-Fi
Soul Eater : Action, Adventure, Comedy, Fantasy, Shounen, Supernatural
Code Geass: Hangyaku no Lelouch R2 : Action, Drama, Mecha, Military, Sci-Fi, Super Power
Nodame Cantabile : Comedy, Drama, Josei, Music, Romance, Slice of Life
--------------------------------
Top 10 Anime Recommendations
--------------------------------
GJ-bu :  Comedy, School, Slice of Life  (Type:  TV , Episodes:  12 )
Hetalia Axis Powers Movie: Paint it, White :  Comedy, Historical, Parody  (Type:  Movie , Episodes:  1 )
The Cockpit :  Historical, Military  (Type:  OVA , Episodes:  3 )
Hyakka Ryouran: Samurai Girls :  Action, Comedy, Ecchi, Harem, Samurai, School  (Type:  TV , Episodes:  12 )
GR: Giant Robo :  Adventure, Mecha, Military, Sci-Fi, Shounen  (Type:  TV , Episodes:  13 )
Transformers: Car Robots :  Adventure, Comedy, Mecha, Sci-Fi, Shounen  (Type:  TV , Episodes:  39 )
Ishikeri :  Comedy  (Type:  Movie , Episodes:  1 )
Double-J :  Comedy, School, Shounen  (Type:  TV , Episodes:  11 )
Channel 5.5 :  Comedy, Parody  (Type:  ONA , Episodes:  4 )
Otenki Oneesan :  Comedy, Hentai, Yuri  (Type:  OVA , Episodes:  2 )

## Evaluation

### Precision dengan Jaccard Similarity

Dalam penelitian ini, sistem rekomendasi dikembangkan menggunakan pendekatan Content-Based Filtering yang didasarkan pada kemiripan genre antar anime. Karena sistem tidak menggunakan data interaksi pengguna seperti rating atau user ID, maka evaluasi kinerja sistem difokuskan pada kesamaan konten, khususnya genre. Metrik evaluasi yang digunakan adalah Precision@K yang dikombinasikan dengan Jaccard Similarity sebagai pengukur relevansi antara anime rekomendasi dan anime target.
Precision@K mengukur proporsi item yang relevan dari seluruh item yang direkomendasikan. Dalam hal ini, item dianggap relevan apabila memiliki nilai Jaccard Similarity terhadap anime target melebihi ambang batas tertentu, misalnya 0.5. Jaccard Similarity sendiri merupakan ukuran kesamaan antara dua himpunan, yaitu himpunan genre dari anime target dan genre dari anime hasil rekomendasi. Nilai Jaccard dihitung dari perbandingan jumlah genre yang sama dengan jumlah gabungan genre keduanya.
Pemilihan metrik Precision dengan pendekatan Jaccard Similarity sangat sesuai untuk sistem rekomendasi berbasis konten karena Precision sendiri menghitung proporsi anime yang relevan terhadap jumlah total anime yang direkomendasikan. Dalam konteks ini, relevansi ditentukan menggunakan Jaccard Similarity, yang mengukur kesamaan antara genre anime target dan genre anime hasil rekomendasi. Dengan menetapkan ambang batas (threshold) sebesar 0.5, artinya apabila dua anime memiliki kemiripan genre minimal 50%, maka anime rekomendasi dianggap relevan. Pendekatan ini efektif, mengingat setiap anime umumnya memiliki lebih dari satu genre, sehingga perhitungan kemiripan tidak bisa dilakukan secara sederhana. Dengan mengelompokkan anime relevan dan tidak relevan berdasarkan nilai Jaccard, maka Precision dapat dihitung secara objektif dan mencerminkan seberapa baik sistem dalam merekomendasikan anime yang sesuai secara konten.

Untuk menghitung metrik evaluasi Precision, maka diperlukan pengelompokkan relevansi menggunakan Jaccard similarity terlebih dahulu. Jika dimisalkan A adalah himpunan genre dari anime target yang akan dicari rekomendasinya dan B adalah himpunan genre dari anime hasil rekomendasi, maka nilai Jaccard similarity dapat dicari dengan rumus mutlak(A irisan B)/mutlak(A gabungan B). Kemudian dengan mengambil ambang batas 0.5, maka dari hasil Jaccard similarity untuk setiap anime hasil rekomendasi yang pada kali ini adalah top 10 anime, dapat diperoleh jika nilai Jaccard similaritynya >= 0.5, maka anime tersebut dikategorikan relevan atau True Positive(TP), jika sebaliknya maka akan dikategorikan False Positive(FP). Selanjutnya, untuk menghitung evaluasinya berdasarkan Precision, maka digunakan rumus sigma(TP)/(sigma(TP)+sigma(FP)). Rumus ini akan menghitung jumlah anime yang dikategorikan sebagai TP akan dibagi dengan jumlah keseluruhan anime yang direkomendasikan karena jumlah anime yang dikategorikan sebagai TP dan jumlah anime yang dikategorikan sebagai FP, jika dijumlahkan akan menghasilkan jumlah keseluruhan anime yang direkomendasikan.

### Root Mean Squared Error (RMSE)

Evaluasi model merupakan langkah penting untuk mengetahui seberapa baik model yang dibangun mampu memprediksi nilai target berdasarkan data input. Dalam proyek ini, model dievaluasi menggunakan Root Mean Squared Error (RMSE) sebagai satu-satunya metrik evaluasi. RMSE (Root Mean Squared Error) dipilih sebagai metrik evaluasi dalam sistem rekomendasi anime karena mampu mengukur seberapa akurat prediksi yang dihasilkan oleh model dibandingkan dengan dari user. RMSE menghitung akar dari rata-rata kuadrat selisih antara nilai prediksi dan nilai aktual, sehingga memberikan penalti yang lebih besar pada kesalahan prediksi yang signifikan. Hal ini penting agar model tidak hanya menghasilkan prediksi yang rata-rata benar, tetapi juga meminimalkan kesalahan besar yang dapat memengaruhi kualitas rekomendasi. Selain itu, RMSE memiliki satuan yang sama dengan rating, sehingga mudah diinterpretasikan dan menjadi standar umum yang sering digunakan dalam sistem rekomendasi berbasis rating. Dengan sifatnya yang kontinu dan diferensial, RMSE juga mendukung proses optimasi model selama pelatihan, sehingga memudahkan peningkatan performa sistem rekomendasi.

Untuk menghitung nilai RMSE dalam sistem rekomendasi ini, digunakan formulasi RMSE yang merupakan akar dari rata-rata kuadrat selisih antara rating asli dan rating prediksi yang dihasilkan oleh model. Pada kasus ini, y adalah rating yang sudah dinormalisasi menggunakan transformasi (rating_user - min_rating) / (max_rating - min_rating) agar berada dalam rentang 0 hingga 1. Dengan memprediksi rating untuk semua pasangan user dan judul anime yang ada di variabel x pada proses split data sebelumnya, maka dapat dihitung selisih antara rating asli yang sudah dinormalisasi dengan rating prediksi untuk setiap data. Selisih ini kemudian dikuadratkan dan dijumlahkan untuk seluruh data, lalu hasilnya dibagi dengan jumlah data. Langkah terakhir adalah mengakarkan nilai tersebut untuk mendapatkan RMSE. Secara matematis, rumusnya adalah: akar((sigma(y_asli-y_prediksi)^2)/n) dimana n adalah jumlah data.

### Hasil Evaluasi

Dengan mendefinisikan fungci jaccard_similarity yang mengambil 2 inputan yakni himpunan genre anime target dan anime rekomendasi, serta mendefinisikan variabel precision untuk menghitung hasil evaluasinya, maka diperoleh bahwa model yang telah dibuat memiliki nilai akurasi 0.8. Ini sudah baik untuk suatu sistem rekomendasi.
Berdasarkan hasil evaluasi dan visualisasi pula dari model collaborative filtering, diperoleh bahwa proses training model cukup smooth dan model konvergen pada epochs 100. Hal ini dapat dilihat dari grafik hasil evaluasi yang membentuk pola yang sama. Dari proses ini, kita memperoleh nilai error RMSE akhir sebesar 0.1309 pada train dan 0.1380 pada validasi. Nilai tersebut cukup bagus untuk sistem rekomendasi.
Berdasarkan proyek yang telah dibuat, maka proyek telah menjawab problem steatment. Karena model berhasil membangun sistem rekomendasi anime yang relevan sesuai preferensi user dengan pendekatan Collaborative Filtering. dan berdasarkan genre yang ditonton dengan pendekatan Content Based Filtering. Untuk masalah rekomendasi berbasis preferensi user, Content-Based Filtering menggunakan genre sebagai fitur utama untuk menyesuaikan rekomendasi dengan anime yang sudah disukai user. Pada pembuatannya pula, hanya diambil anime dari user yang melakukan interaksi minimal 1000 dan rating lebih dari 7, sehingga ini membuat anime yang direkomendasikan lebih layak dan bagus. Collaborative Filtering menangani aspek rekomendasi berdasarkan pola kesamaan antar user, sehingga memperkaya sistem dengan sudut pandang rating yang diberikan. Dengan demikian, kedua pendekatan ini sudah menjawab problem utama tentang rekomendasi anime yang relevan baik secara individual maupun berdasarkan genre dan pola user lain.
Goals memberikan 10 daftar anime rekomendasi yang relevan berdasarkan preferensi dan riwayat interaksi user berhasil dicapai dengan sistem Content-Based Filtering yang memanfaatkan genre dan Collaborative Filtering yang memperhitungkan pola rating antar user. Sistem dapat menyajikan daftar rekomendasi yang beragam dan sesuai dengan apa yang diinginkan user berdasarkan evaluasi akurasi dan RMSE pada model Collaborative Filtering serta pengujian similarity genre dengan Jaccard similarity dan perhitungan evaluasi dengan precision pada Content-Based Filtering. Dengan evaluasi yang menunjukkan performa baik, goals memberikan rekomendasi relevan sebanyak 10 anime sudah terpenuhi.
Pendekatan ganda Content-Based dan Collaborative Filtering memberikan solusi yang saling melengkapi dan membantu dalam menghasilkan rekomendasi yang relevan dan personal. Content-Based Filtering dengan pemanfaatan genre membantu membangun profil preferensi user yang spesifik. Collaborative Filtering memperluas rekomendasi dengan melihat pola dari user lain yang mirip, mengatasi keterbatasan Content-Based Filtering yang hanya mengandalkan fitur konten. Metode ini terbukti efektif dalam mengevaluasi dan menghasilkan rekomendasi yang sesuai kebutuhan user, sehingga solusi yang diterapkan sangat membantu dalam menjawab problem dan mencapai goals.

## Daftar Pustaka

[1]	J. Elektronik and I. Komputer Udayana, “Sistem Rekomendasi Seri Animasi Jepang (Anime) Menggunakan User-Based Collaborative Filtering dan Spearman Rank Correlation Coefficient”.
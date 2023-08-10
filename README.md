# capstone_project_modul3_modeling_bank_marketing_campaign

## **Business Problem Understanding**
**Context**  
Jenis produk keuangan yang saat ini digunakan masyarakat sangat bervariasi. Salah satu produk keuangan yang cukup dikenal masyarakat adalah term deposit. Mekanisme term deposit adalah nasabah menyimpan sejumlah uang di bank atau lembaga keuangan, dan uang tersebut hanya dapat ditarik setelah jangka waktu tertentu. Sebagai kompensasinya, nasabah akan diberikan bunga tetap sesuai dengan nominal uang yang disetorkan.

Namun demikian, sebagai badan usaha dengan produk keuangan dan nasabahnya masing-masing, bank tetap harus bersaing agar tidak kehilangan nasabah. Salah satu cara untuk mendapatkan pelanggan baru adalah dengan melakukan kampanye pemasaran.

Target :

0 : Tidak melakukan term deposit

1 : Melakukan term deposit

**Problem Statement :**

Kampanye pemasaran dengan menghubungi nasabah bisa memakan waktu dan biaya jika perusahaan menargetkan semua nasabah tanpa melakukan penyaringan terlebih dahulu. Perusahaan ingin meningkatkan efisiensi kampanye dengan mengetahui nasabah mana yang berminat untuk melakukan term deposit. 

**Goals :**

Berdasarkan permasalahan tersebut, perusahaan ingin memiliki kemampuan untuk memprediksi kemungkinan seorang nasabah berminat untuk melakukan term deposit atau tidak sehingga kampanye pemasaran hanya akan difokuskan kepada nasabah yang berminat untuk melakukan term deposit saja.

Dan juga, perusahaan ingin mengetahui faktor apa saja yang membuat seorang nasabah berminat untuk melakukan term deposit, sehingga mereka dapat membuat kampanye pemasaran yang lebih baik untuk diberikan kepada nasabah potensial (nasabah yang berminat untuk melakukan term deposit) .

**Analytic Approach :**

Kita akan menganalisis data untuk menemukan pola yang membedakan nasabah yang berminat melakukan term deposit atau tidak berminat. Kemudian kita akan membangun model klasifikasi yang akan membantu perusahaan untuk dapat memprediksi probabilitas seorang nasabah akan berminat melakukan term deposit atau tidak berminat.

**Evaluation Metric :**

Karena fokus utama kita adalah nasabah yang berminat melakukan term deposit, maka target yang kita tetapkan adalah sebagai berikut:

Target :

0 : Tidak melakukan term deposit

1 : Melakukan term deposit

Type 1 error : False Positive (nasabah yang aktualnya tidak melakukan term deposit tetapi diprediksi melakukan term deposit)

Konsekuensi: Potensi pengeluaran biaya yang tinggi untuk melakukan kampanye pemasaran dengan telefon yang tidak sebanding dengan hasil akhir

Type 2 error : False Negative (nasabah yang aktualnya melakukan term deposit tetapi diprediksi tidak melakukan term deposit)

Konsekuensi: Kehilangan nasabah yang berpotensi meningkatkan pendapatan perusahaan dari term deposit

Untuk memberikan gambaran konsekuensi secara kuantitatif, maka kita akan coba hitung dampak biaya berdasarkan asumsi berikut :
- Menurut [liveagen.com](https://www.liveagent.com/customer-support-glossary/cost-per-call/) Biaya rata-rata telefon untuk setiap panggilan adalah $2.70 – $5.60.
- menurut [blog.hubspot.com](https://blog.hubspot.com/sales/best-times-to-connect-with-leads-infographic), setidaknya kita harus menelfon sebanyak 6 kali kepada konsumen agar konsumen tersebut tertarik pada produk yang kita tawarkan
- Menurut [investopedia.com](https://www.investopedia.com/terms/t/timedeposit.asp) Term deposit sangat menguntungkan untuk bank. Setiap deposit nasabah bisa digunakan bank untuk meminjamkan uang ke nasabah lain atau menginvestasikan uang dari term deposit kepada sekuritas lain yang dapat memberikan profit lebih tinggi daripada yang dibayarkan oleh nasabah.
- Menurut [bankrate.com](https://www.bankrate.com/banking/cds/cd-rates/) Bunga yang diterima dari term deposit sebesar $1000 selama 1 tahun ada di sekitar 5%
- Menurut [westpac.com](https://www.westpac.com.au/personal-banking/bank-accounts/term-deposit/savings-vs-term-deposit/) sebagian besar term deposit memiliki setoran saldo minimum, mayoritas antara $1,000 - $5,000


Berdasarkan asumsi di atas maka kita dapat coba kuantifikasi konsekuensinya sebagai berikut :
- Pengeluaran biaya --> Untuk setiap panggilan, kita asumsikan biayanya adalah $4 dan kita harus menelfon sebanyak 6x, jadi biaya yang dikeluarkan adalah $24 per nasabah
- Kerugian akibat kehilangan nasabah potensial --> Untuk setiap pelanggan yang melakukan term deposit sebesar $1,000 dalam jangka waktu 1 tahun, kita harus mengembalikan bunga sebesar $50 kepada nasabah. Setelah dikurangi dengan bunga,  apabila kita menggunakan uang tersebut sebagai pinjaman untuk nasabah lain, maka kita akan mendapatkan keuntungan sebesar : 
    - Keuntungan = (Nominal deposit x bunga x periode) / jumlah bulan [sumber](https://manajemen.uma.ac.id/2021/02/2-cara-menghitung-bunga-pinjaman-bank-flat-dan-efektif/)
    - Keuntungan = (950 x 5% x 1) / 12 = **$3,95 perbulan** atau **$47,5 pertahun**

Berdasarkan konsekuensinya, kita merasa bahwa keduanya sama-sama penting untuk diminimalisir, kita akan membuat model yang dapat mengurangi jumlah False Negative dan juga False Positive sehingga metric utama yang akan kita gunakan adalah **F1-score**.

---
## **Untuk proses modeling bisa dilihat pada file .ipynb yang sudah diunggah**
---

## **Conclusion**
- Model klasifikasi terbaik untuk memprediksi nasabah yang term deposit atau tidak pada dataset ini adalah Gradient Boost dengan metriks f1_score sebesar 0.72

- Parameter terbaik untuk final model yang dipilih adalah :
    - n_estimator : 0.60
    - max_features : 6
    - max_depth : 3
    - learning_rate : 0.02
    <br><br>

- Model ini bisa menghemat biaya telfon sebesar $11,208 pertahun

- Berdasarkan hasil analisis, nasabah yang cenderung melakukan term deposit adalah nasabah yang bekerja sebagai management, nasabah yang tidak mempunyai pinjaman perumahan atau pinjaman pribadi, dan nasabah yang dihubungi melalui seluler.

- Berdasarkan confusion matrix pada test set di atas terlihat bahwa dengan model yang telah kita buat didapati:
- Jumlah calon nasabah yang aktualnya term deposit dan diprediksi akan term deposit (True Positive) : 515 orang
- Jumlah calon nasabah yang aktualnya term deposit tetapi diprediksi tidak akan term deposit (False Negative) : 154 orang
- Jumlah calon nasabah yang aktualnya tidak term deposit dan diprediksi tidak akan term deposit (True Negative) : 313 orang
- Jumlah calon nasabah yang aktualnya tidak term deposit tetapi diprediksi akan term deposit (False Positive) : 243 orang
- False Positive Rate (aktualnya tidak term deposit, diprediksi term deposit) = 43.7%
- False Negative Rate (aktualnya term deposit, diprediksi tidak term deposit) = 76.9%

---

Saat kita tidak menggunakan machine learning, kita tidak dapat memprediksi calon nasabah yang akan term deposit atau tidak. Dampaknya adalah kita cenderung untuk melakukan kampanye dengan menelepon ke seluruh calon nasabah.

Jumlah calon nasabah untuk dasar perhitungan :
- calon nasabah yang kita tawarkan term deposit = 1225 orang
- calon nasabah yang aktualnya term deposit = 669 orang

Cost Estimation
Kita asumsikan setiap nasabah ditelfon sebanyak 6 kali dengan biaya $4 untuk setiap panggilan
- total panggilan x biaya telfon
- = (Jumlah nasabah yang kita tawarkan term deposit x biaya perpanggilan)
- = 1225 x 24 = $29.400

Profit estimation
- Pendapatan - Biaya
- = (Jumlah calon nasabah yang term deposit x Profit dari term deposit) - ( Jumlah calon nasabah yang term deposit x Biaya penggantian) 
- = (669 x $47,5) - (1225 x $24) = $31,777.5 - $29,400 = $2,377.5

Maka keuntungannya sekitar **$2,377.5**

---
Saat kita menggunakan machine learning, kita hanya menawarkan produk ke calon nasabah yang diprediksi akan term deposit saja.

Jumlah Nasabah untuk dasar perhitungan :
- Calon nasabah yang dihubungi adalah nasabah yang diprediksi term deposit = TP + FP = 515 + 243 = 647 orang
- Calon nasabah yang di prediksi dan actualnya term deposit = TP = 515

Profit Estimation
- Pendapatan - Biaya
- = (Calon nasabah yang di prediksi dan actualnya term deposit x Profit term deposit) - ( Jumlah calon nasabah yang diprediksi term deposit x Biaya penggantian) 
- = (515 x $47,5) - (758 x $24) = $24,462.5 - $18,192 = $6,270.5
Maka keuntungannya sekitar **$6,270.5**

---
Peningkatan Profit = $6,270.5 - $2,377.5 = $3,893

**Persentase kenaikan = (nilai akhir - nilai awal) / nilai awal x 100%** 
- = $3,893 / $2,377.5 x 100% = **1.64%**

Berdasarkan test set, model kita dapat meningkatkan keuntungan hingga **1.64%** dalam setahun.


## **Recommendation**
- Menambahkan lebih banyak fitur yang kemungkinan bisa meningkatkan score model seperti status pernikahan, jumlah anggota keluarga, income, dan sebagainya.

- Menghindari pengisian data dengan nilai 'unknown' atau 'other' karena menyebabkan score model menjadi turun.
- Karena fitur poutcome mengandung nilai 'unknown' dan 'other' yang sangat banyak, fitur tersebut kita hilangkan pada pemodelan ini. Apabila fitur tersebut akan digunakan pada proses modeling selanjutnya, nilai harus diisi dengan 'Success' atau 'Failure' 
- Pada dataset, terlihat bahwa marketing campaign masih dilakukan secara tradisional yaitu melalui telemarketing. Seiring dengan perkembangan zaman, ada baiknya kita bisa mulai meningkatkan kegiatan marketing campaign kita melalui internet (digital marketing) supaya bisa menjangkau calon nasabah secara lebih luas dan lebih efisien.
- Kita bisa memberikan bunga yang lebih kompetitif dibandingkan kompetitor sehingga bisa menarik calon nasabah untuk melakukan term deposit di bank kita.

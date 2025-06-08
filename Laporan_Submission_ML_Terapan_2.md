# Laporan Proyek Machine Learning - Rifky Galuh Yuliawan

## Project Overview

Bagi kebanyakan orang, khususnya wanita penting untuk memperhatikan penampilan baik dari segi fashion, gaya hidup, dan wajah. Setiap orang memiliki kulit wajah dengan warna, tekstur yang berbeda-beda tergantung dari faktor keturunan, kondisi tubuh, dan iklim tempat dimana ia tinggal. Hal yang paling terlihat dari pandangan mata adalah kulit wajah.  Untuk tampil sempurna banyak orang yang rela mengeluarkan banyak uang untuk menjaga dan merawat kulit. 

Menurut data internal Sociolla, sebanyak 17 persen Generasi Z yang rela mengeluarkan uang lebih dari Rp300 ribu untuk berbelanja produk kecantikan. Sementara itu, 35 persen lainnya memilih untuk berbelanja dengan bujet sekitar Rp150 ribu hingga Rp300 ribu. Berbanding balik dengan Generasi Z, 28 persen Milenial justru rela mengeluarkan uang lebih dari Rp 300 ribu untuk berbelanja skincare dan bodycare. Kemudian melalui survei ZAP Beauty Index  2024 menyatakan mayoritas wanita Indonesia rela merogoh kocek lebih dari Rp500 ribu per bulan untuk perawatan di klinik kecantikan.

Walaupun banyak wanita yang rela menghabiskan uang ratusan ribu untuk membeli produk perawatan kulit, namun ternyata belum tentu menjamin mereka itu memahami jenis kulit wajah yang mereka miliki dan belum tentu produk yang mereka beli itu cocok dengan jenis kulit mereka. Nisa et al (2021) berpendapat hal yang sama dalam jurnalnya yang menyatakan bahwa banyak wanita kurang memahami karakteristik jenis kulit wajah sendiri sehingga ketika hendak melakukan perawatan dan menggunakan make up yang seharusnya menunjang penampilan, wanita tersebut mengalami ketidaksesuaian antara produk yang digunakan dengan jenis kulit wajah yang dimiliki. 

Seperti yang diketahui jenis kulit wajah itu ada 3 yaitu Oily (berminyak), Normal, dan Dry (kering). Pengetahuan mengenai jenis kulit wajah dapat memengaruhi keefektifan suatu produk yang dipakai sehingga dapat menekan perilaku impulsif dalam membeli produk skincare dan mencegah penyakit kulit akibat ketidakcocokan dalam menggunakan produk skincare. Dengan adanya kecerdasan buatan (Artificial Intelligence) maka dapat dikembangkan teknologi deteksi jenis kulit wajah yang diharapkan dapat menjadi solusi yang lebih ekonomis dibanding pergi ke klinik kecantikan untuk mengetahui jenis kulit wajah yang dimiliki atau sebagai alat early detection sebelum pergi ke klinik.

### Referensi

- Nissa, N. F., Janiati, A., Cahya, N., Anton, A., & Astuti, P. (2021). Application of deep learning using convolutional neural network (CNN) method for women’s skin classification. Scientific Journal of Informatics, 8(1), 144–153. https://doi.org/10.15294/sji.v8i1.26888
- ZAP Clinic. (2024). ZAP Beauty Index 2024. https://zapclinic.com/files/ZAP_Beauty_Index_2024.pdf

## Business Understanding

### Problem Statements

- Bagaimana cara mengembangkan sistem rekomendasi produk skincare yang sesuai degan jenis kulit wajah?
- Seberapa akurat algoritma sistem rekomendasi yang digunakan dalam memberikan rekomendasi produk skincare berdasarkan jenis kulit wajah?

### Goals

- Mendapatkan model sistem rekomendasi produk skincare yang sesuai dengan kulit wajah dengan bentuk akhir top-N recommendation sebagai outputnya.
- Mengetahui tingkat akurasi model sistem rekomendasi yang telah dikembangkan.

## Data Understanding

Dataset yang digunakan pada proyek ini bersumber dari Kaggle pada [tautan berikut](https://www.kaggle.com/datasets/nadyinky/sephora-products-and-skincare-reviews).

### Variabel-variabel pada Dataset

#### Dataset Products

- `product_id`: identifier unik dari produk
- `product_name`: nama produk
- `brand_id`: identifier unik brand
- `brand_name`: nama brand produk
- `loves_count`: jumlah orang yang memfavoritkan produk
- `rating`:  angka penilaian rata-rata produk dari ulasan pengguna
- `reviews`: jumlah ulasan pengguna untuk produk
- `size`: ukuran produk dalam oz, ml, g, kemasan, atau satuan lain.
- `variation_type`: jenis parameter variasi untuk produk
- `variation_value`: nilai spesifik dari parameter variasi produk
- `variation_desc`: deskripsi dari parameter variasi produk
- `ingredients`: daftar bahan produk
- `price_usd`: harga produk (USD)
- `value_price_usd`: potensi penghematan biaya produk (USD)
- `sale_price_usd`: harga jual produk (USD)
- `limited_edition`: benar atau salah bahwa produk ini edisi terbatas
- `new`: benar atau salah bahwa produk ini baru
- `online_only`: benar atau salah bahwa produk ini hanya dijual daring
- `out_of_stock`: benar atau salah bahwa produk ini sedang kehabisan stok
- `sephora_exclusive`: benar atau salah bahwa produk ini eksklusif untuk Sephora
- `highlights`: kata kunci sorotan dari produk (misalnya 'Vegan', 'Matte Finish')
- `primary_category`: kategori pertama pada bagian breadcrumbs
- `secondary_category`: kategori kedua pada bagian breadcrumbs
- `tertiary_category`: kategori ketiga pada bagian breadcrumbs
- `child_count`: jumlah variasi dari produk
- `child_max_price`: harga tertinggi di antara variasi produk
- `child_min_price`: harga terendah di antara variasi produk

#### Dataset Reviews

- `author_id`: identifier unik dari penulis ulasan
- `rating`: angka penilaian produk dari penulis ulasan
- `is_recommended`: benar atau salah bahwa penulis merekomendasikan produk
- `helpfulness`: rasio semua penilaian terhadap penilaian positif untuk ulasan
  `(total_pos_feedback_count / total_feedback_count)`
- `total_feedback_count`: jumlah keseluruhan umpan balik oleh pengguna lain untuk ulasan ini
- `total_neg_feedback_count`: jumlah pengguna yang memberi umpan balik negatif untuk ulasan ini
- `total_pos_feedback_count`: jumlah pengguna yang memberi umpan balik positif untuk ulasan ini
- `submission_time`: tanggal ulasan diunggah pada situs web dalam format 'yyyy-mm-dd'
- `review_text`: isi ulasan yang ditulis oleh penulis
- `review_title`: judul ulasan yang ditulis oleh penulis
- `skin_tone`: warna kulit penulis (cerah, sawo matang, dsb)
- `eye_color`: warna mata penulis (cokelat, hijau, dsb)
- `skin_type`: jenis kulit penulis (kombinasi, berminyak, dsb)
- `hair_color`: warna rambut penulis (cokelat, merah marun, dsb)
- `product_id`: identifier unik dari produk yang direview
- `product_name`: nama dari produk yang direview
- `brand_name`: brand dari produk yang direview
- `price_usd`: harga USD dari produk yang direview

### Exploratory Data Analysis (EDA)

#### 1. Memahami Struktur Data

- Tinjau jumlah baris dan kolom dalam dataset.

  ![Product Shape](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/product-shape.png)

  Dari gambar di atas dapat diketahui bahwa products_dataset terdiri dari 8494 baris data dengan 27 kolom.

  ![Review Shape](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/review-shape.png)

  Kemudian, dapat diketahui juga dari gambar di atas bahwa reviews_dataset terdiri dari 808855 baris data dengan 18 kolom.

- Tinjau jenis data di setiap kolom (numerikal atau kategorikal).
  
  ![Product Info](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/product-info.png)

  Dari gambar di atas dapat diketahui pada products_dataset terdiri dari 7 kolom bertipe float, 8 kolom bertipe integer yang mana 2 kolom ini menyatakan bahwa dataset terdiri dari 15 kolom numerikal, dan 12 kolom bertipe object yang menyatakan bahwa dataset terdiri dari 12 kolom kategorikal.
  
  ![Review Info](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/review-info.png)

  Sementara pada reviews_dataset terdiri dari 3 kolom bertipe float, 4 kolom bertipe integer yang mana 2 kolom ini menyatakan bahwa dataset terdiri dari 7 kolom numerikal, dan 11 kolom bertipe object yang menyatakan bahwa dataset memiliki 11 kolom kategorikal.

#### 2. Identifikasi Missing Values, dan Duplicated Values

Dataset awal, yaitu product dan review masing-masing memiliki missing values yang cukup banyak, dengan rincian seperti pada gambar berikut.

![Missing Values Product](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/missing-values-product.png)
![Missing Values Review](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/missing-values-review.png)

Namun untuk sementara, missing values tersebut dapat diabaikan saja karena kedua dataset perlu digabungkan dengan memilih fitur yang relevan untuk proses modelling sistem rekomendasi.

Berikut missing values yang terdapat dari gabungan dataset:

![Missing Values](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/missing-values.png)

Setelah memilih fitur yang relevan untuk proses modeling sistem rekomendasi, lalu melakukan merging dataset, pada gambar di atas dapat dilihat bahwa terdapat banyak missing values pada kolom is_recommended dan skin_type.

![Duplicated Values](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/duplicated-values.png)

Selain itu terdapat nilai yang terduplikasi karena ada kemungkinan banyak review yang diberikan untuk satu produk. Saya memutuskan untuk tidak drop kolom yang terdapat nilai duplikat karena adanya duplikasi ini menandakan realitas interaksi pengguna dengan produk.

#### 3. Analisis Distribusi, Korelasi, dan Visualisasi Data

- Analisis distribusi variabel numerik dengan statistik deskriptif dan visualisasi seperti histogram atau boxplot.

  ![Distribution 1](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/distribution-1.png)

  Dari histogram "is_recommended" yang mana fitur ini akan menjadi target label bisa dilihat bahwa fitur tersebut memiliki nilai yang tidak seimbang.
  
  ![Distribution 2](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/distribution-2.png)

  Lalu pada fitur "skin_type" juga terdapat ketidakseimbangan nilai.

- Memeriksa hubungan antara variabel menggunakan matriks korelasi atau scatter plot.

  **Univariate Analysis**

  1. Fitur `author_id`

    ![Univariate Author](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/univariate-author.png)

  2. Fitur `skin_type`

    ![Univariate Skin](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/univariate-skin.png)

  3. Fitur `product_name`

    ![Univariate Product](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/univariate-product.png)

  4. Fitur `brand_name`

    ![Univariate Brand](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/univariate-brand.png)

  **Multivariate Analysis**

  ![Multivariate Pairplot](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/multivariate-pairplot.png)

  ![Multivariate Heatmap](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/multivariate-heatmap.png)

  Dari heatmap Correlation Matrix di atas, dapat diketahui bahwa `is_recommended` berkorelasi positif dengan `rating_reviews`. Hal ini menandakan bahwa semakin tinggi rating yang diberikan oleh pengguna maka semakin besar pula kemungkinan pengguna tersebut merekomendasikan produk.

## Data Preparation

Tahap ini memastikan kualitas data telah baik sebelum digunakan dalam model machine learning. Pada tahap inilah proses-proses transfomasi data yang diperlukan.

Sebelum itu, ada pula proses transformasi data yang sempat diterapkan pada tahap Data Understanding untuk keperluan eksplorasi.

### Transformasi yang Sudah Diterapkan Sebelumnya

Berikut transformasi data yang diperlukan pada tahap eksplorasi data:
1. Menghapus Kolom yang Tidak Digunakan
1. Memilih Fitur yang Relevan
1. Menggabungkan Dataset

#### 1. Menghapus Kolom yang Tidak Digunakan

```python
df_review = df_review.drop(columns=['Unnamed: 0'])
```

Pada awal memuat dataset review, terdapat kolom `Unnamed: 0` yang berupa identifier unik dari setiap baris review. Kolom ini tidak relevan terhadap fitur apapun sehingga dihapus saja dari `DataFrame`.

#### 2. Memilih Fitur yang Relevan

Saat melakukan eksplorasi data, ditemukan banyak missing values pada masing-masing dataset. Dengan ini, perlu dilakukan filter dengan memilih kolom-kolom yang relevan saja pada kedua dataset.

```python
df_product_relevant = df_product.copy()
df_product_relevant = df_product_relevant[['product_name','brand_name','rating','reviews']]

df_review_relevant = df_review.copy()
df_review_relevant = df_review_relevant[['author_id','rating','is_recommended','skin_type','product_name','brand_name']]
```

Dengan ini, dataset akan terfokus pada kolom yang relevan, sehingga penanganan missing values kedepannya akan lebih optimal karena telah mengabaikan fitur yang tidak digunakan.

#### 3. Menggabungkan Dataset

Dataset produk dan review yang telah difilter relevansinya digabungkan menjadi satu melalui dataset review, karena sistem rekomendasi akan dibuat berdasarkan analisa review dari masing-masing produk.

```python
df_merged = pd.merge(df_review_relevant, df_product_relevant, on=['product_name', 'brand_name'], how='left', suffixes=('_reviews', '_products'))
```

Dengan dilakukannya proses ini, otomatis juga akan mempermudah proses pengerjaan proyek selanjutnya, sebab proses analisa, transformasi, dan pelatihan hanya perlu dilakukan dari satu sumber.

### Transformasi Data yang Belum Diterapkan

Adapun proses yang belum dilakukan dan akan diterapkan pada Data Preparation sebagai berikut:
1. Menangani Missing Values
1. Menyesuaikan Tipe Data
1. Identifikasi dan Menangani Outliers
1. Undersampling
1. Data Splitting
1. Feature Encoding & Scaling

#### 1. Menangani Missing Values

Missing values perlu ditangani agar tidak terjadi error pada model yang dikembangkan, sehingga hasil analisis menjadi lebih akurat.

```python
df_merged = df_merged.dropna()
```

Pada proyek ini, baris yang memiliki missing values akan dihapus dengan menjalankan kode di atas.

#### 2. Menyesuaikan Tipe Data

Terdapat beberapa kolom dengan tipe data yang belum sesuai seperti `is_recommended` dan `reviews`. Sehingga perlu dilakukan penyesuaian agar data bisa diproses dengan benar, dan mencegah error saat analisis atau training model.

```python
df_merged['is_recommended'] = df_merged['is_recommended'].astype(int)
df_merged['reviews'] = df_merged['reviews'].astype(int)
```

Dengan menjalankan kode di atas, kolom `is_recommended` dan `reviews` akan diubah menjadi tipe integer.

#### 3. Identifikasi dan Menangani Outliers

Untuk mendeteksi outliers pada fitur numerikal, dibuatlah fungsi berikut.

```python
def detect_outliers(data):
    Q1 = data[data.columns].quantile(0.25)
    Q3 = data[data.columns].quantile(0.75)
    IQR = Q3 - Q1
    lower_bound = Q1 - 1.5 * IQR
    upper_bound = Q3 + 1.5 * IQR
    outlier_mask = (data[data.columns] < lower_bound) | (data[data.columns] > upper_bound)
    outliers = data[outlier_mask.any(axis=1)].index
    return outliers

numeric_features = df_merged.select_dtypes(include=['number'])
detect_outliers(numeric_features)
```

![Outliers 1](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/outliers-1.png)

Pada proyek ini, ditemukan sebanyak 144.079 outliers, yang mana nilai ini cukup besar. Perlu dibuat visualisasi data agar dapat mengetahui dengan mudah di kolom manakah outliers ditemukan seperti gambar di bawah.

![Outliers 2](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/outliers-2.png)

Meskipun ditemukan banyak outliers, namun saya menganggap nilai ekstrem dari kolom-kolom numerik tersebut merupakan outliers dalam konteks bisnis. **Statistical Outliers tidak sama dengan Business Outliers**.

Contohnya pada kolom `rating_reviews` di mana banyak user yang memberi rating di angka 4-5, lalu ada juga user yang memberi rating 1 atau 2. Nilai-nilai ini mungkin bisa dianggap outliers secara statistik, namun sebenarnya masih masuk akal untuk dianggap sebagai sebuah nilai. Sehingga, pada kasus ini outliers tidak di-drop ataupun dilakukan manipulasi.

#### 4. Undersampling

Pada tahap EDA telah diketahui bahwa untuk fitur `skin_type` terdapat ketidakseimbangan distribusi, sehingga perlu dilakukan undersampling agar tidak terjadi bias pada kelas mayoritas.

Perlu dilakukan pencarian target nilai yang akan digunakan sebagai jumlah minimal untuk undersampling dengan kode sebagai berikut:

```python
min_count = df_merged['skin_type'].value_counts().min()
min_count
```

Dengan ini ditemukan bahwa jumlah minimal dataset yang ada adalah 80.571 yang merupakan dataset dengan kelas `oily`. Sehingga nilai target ini akan diterapkan pada kelas `combination` dan `dry` saja. Implementasi ini dilakukan dengan kode sebagai berikut:

```python
u_combination_type = resample(df_merged[df_merged['skin_type'] == 'combination'],
                              replace=False,
                              n_samples=min_count,
                              random_state=42)

u_dry_type = resample(df_merged[df_merged['skin_type'] == 'dry'],
                      replace=False,
                      n_samples=min_count,
                      random_state=42)

normal_type = df_merged[df_merged['skin_type'] == 'normal']

oily_type = df_merged[df_merged['skin_type'] == 'oily']

df_undersampled = pd.concat([u_combination_type, u_dry_type, normal_type, oily_type])
df_undersampled['skin_type'].value_counts()
```

Dengan fungsi `resample()`, dataset target akan diambil berdasarkan `n_samples` yang ditetapkan berdasarkan variabel `min_count` sebelumnya, yaitu jumlah dataset terkecil. Kemudian menggabungkan seluruh dataset ke dalam `DataFrame` baru.

Untuk kelas `normal` dan `oily` tetap menggunakan dataset dengan jumlah awal. Sehingga didapatkan jumlah dataset sebagai berikut.

![Undersampling](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/undersampling.png)

#### 5. Data Splitting

Tahap ini membagi dataset menjadi beberapa subset yang terpisah untuk tujuan pelatihan, validasi, dan pengujian model machine learning.

Alasan perlu dilakukannya tahap ini yaitu:

1. Menghindari overfitting
2. Menghasilkan evaluasi yang akurat

```python
ds_train, ds_test = train_test_split(df_undersampled, test_size=0.2, random_state=42)
```

Pada proyek ini, dataset dibagi menjadi data latih dan data uji (train dan test), dengan `test_size=0.2`. Itu berarti 80% dari keseluruhan data akan digunakan untuk pelatihan dan 20% sisanya untuk pengujian. Lalu `random_state=42` menjamin bahwa pembagian data selalu konsisten setiap kali kode dijalankan (reproducibility).

#### 6. Feature Encoding & Scaling

Pada tahap ini proses encoding dan scaling feature dilakukan. Proses scaling dengan standarisasi `StandardScaler`, juga dikenal sebagai penskalaan Z-score, berfungsi untuk mengubah skala pada suatu fitur sehingga memiliki rata-rata 0 dan standar deviasi 1. Sementara encoding dengan `OneHotEncoder` mengubah data kategoris menjadi format numerik biner sehingga dapat dimengerti oleh komputer.

```python
preprocessor = ColumnTransformer(transformers=[
    ('num', Pipeline([
        ('scaler', StandardScaler())
    ]), numeric_features.columns),
    ('cat', Pipeline([
        ('encoder', OneHotEncoder(handle_unknown='ignore'))
    ]), ['skin_type'])
])
ds_train_transformed = preprocessor.fit_transform(ds_train)
ds_test_transformed = preprocessor.transform(ds_test)
```

Kode di atas menerapkan scaling pada kolom-kolom numerik dan encoding pada kolom kategori, yaitu `skin_type`. Dengan `ColumnTransformer` memungkinkan untuk memproses kolom berbeda dengan teknik yang berbeda sesuai parameter `transformers` yang ditentukan. Misalnya kolom-kolom numerik akan distandardisasi dengan `StandardScaler`. Kemudian kolom `skin_type` akan dilakukan encoding jadi vektor biner dengan `OneHotEncoder`. Terakhir melakukan `fit_transform` pada data latih (melatih dan transformasi sekaligus) serta melakukan `transform` pada data data test.

## Modeling

Pada tahap ini algoritma machine learning digunakan untuk menjawab problem statement. Pendekatan sistem rekomendasi yang dikembangkan yakni pendekatan content based filtering.

- Kelebihan: tidak bergantung pada data pengguna lain (cocok untuk pengguna baru), lebih personal karena fokus pada preferensi user tersebut.
- Kekurangan: kurang mampu memberikan rekomendasi yang "beragam" (cenderung repetitif), tidak memanfaatkan wisdom of the crowd (apa yang disukai pengguna lain).

### Tahap Penyusunan Model

#### 1. Mendapatkan vektor representatif

```python
skin_type_labels = ds_train['skin_type'].unique()
skin_type_encoded = []

for skin in skin_type_labels:
    skin_data_original = ds_train.reset_index()
    indices_for_skin = skin_data_original[skin_data_original['skin_type'] == skin].index
    skin_data_transformed = df_train_transformed.iloc[indices_for_skin]
    skin_profile_vector = skin_data_transformed.mean()
    skin_type_encoded.append(skin_profile_vector)

skin_type_encoded = np.array(skin_type_encoded)
```

Kode di atas akan membuat vektor representasi untuk setiap jenis kulit berdasarkan fitur numerik dari data latih yang telah ditransformasi sebelumnya.

Hasil ini dapat digunakan untuk mengukur kemiripan antar jenis kulit dan merekomendasikan produk yang cocok untuk jenis kulit tertentu melalui pendekatan content-based filtering.

#### 2. Similarity Measure

```python
similarity_matrix = cosine_similarity(df_train_transformed, skin_type_encoded)
```

Kode di atas akan mengukur tingkat kemiripan setiap produk dengan masing-masing jenis kulit berdasarkan vektor fitur yang telah diproses.

#### 3. Mendapatkan rekomendasi 5 produk 

```python
target_skin = 'oily'
target_index = list(skin_type_labels).index(target_skin)

df_train_transformed['similarity'] = similarity_matrix[:, target_index]
df_train_transformed = df_train_transformed.reset_index(drop=True)

df_recommendations = pd.merge(ds_train[['product_name', 'brand_name']], df_train_transformed, left_index=True, right_index=True)
df_recommendations['target_skin_type'] = target_skin

recommendations = df_recommendations.sort_values(by='similarity', ascending=False).drop_duplicates('product_name').reset_index(drop=True).head(5)
print(recommendations[['product_name', 'brand_name', 'similarity','target_skin_type']])
```

Dengan menjalankan kode di atas, akan menghasilkan 5 produk teratas untuk jenis kulit yang diberikan, berdasarkan seberapa mirip fitur produk dengan profil rata-rata kulit tersebut.

![Output](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/output.png)

## Evaluation

Tahap ini melakukan evaluasi performa terhadap model mengenai rekomendasi yang dikeluarkan. Metrik evaluasi yang digunakan pada pendekatan content-based filtering ini adalah `precision@K` dan `recall@K`.

- `precision@K`: mengukur jumlah dari K item teratas yang benar-benar relevan, sesuai dengan data ground truth, misalnya `is_recommended==1`.
- `recall@K`: mengukur jumlah dari produk relevan yang berhasil direkomendasikan.

Pada proyek ini, hal yang akan dievaluasi adalah rekomendasi top 5.

Sehingga precision@5 dihitung sebagai:

```
precision@5 = Jumlah produk yang benar-benar direkomendasikan (label=1) dalam Top-5
  / 5 
```

Sedangkan, `recall@k` dihitung sebagai:

```
recall@5 = Jumlah total produk relevan (label=1) untuk user tersebut
  / Jumlah produk yang benar-benar relevan (label=1) dalam Top-5
```

```python
df_combined_test = pd.concat([ds_test[['product_name', 'skin_type', 'is_recommended']].reset_index(drop=True),
                              df_test_transformed.reset_index(drop=True)], axis=1)
```

Kode di atas menyatukan kembali data test yang telah ditransformasi sebelumnya dengan kolom asli seperti `product_name`, `skin_type`, dan `is_recommended` untuk keperluan evaluasi.

```python
def precision_at_k_content(recommendations, ds_test, target_skin=None, k=5):
    recommended_products = recommendations['product_name'].head(k).values
    actual_recommended = ds_test[
        (ds_test['skin_type'] == target_skin) &
        (ds_test['is_recommended'] == 1)
    ]['product_name'].unique()
    relevant = set(recommended_products) & set(actual_recommended)
    return len(relevant) / k

precision = precision_at_k_content(recommendations, df_combined_test, target_skin)
```

Kode di atas mengukur seberapa akurat rekomendasi 5 produk teratas dibandingkan dengan produk yang benar-benar direkomendasikan pada data test. Fungsi `precision_at_k_content` menerima `recommendations`, yaitu daftar produk yang direkomendasikan dengan kolom `product_name`, data test, dan `target_skin` (sebelumnya didefinisikan oily).

Hasil dari evaluasi di atas adalah:
![Evaluation Precision](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/evaluation-precision.png)

Hasil ini berarti 5 produk teratas yang direkomendasikan oleh model dengan pendekatan content-based filtering benar-benar relevan, yaitu semuanya termasuk dalam produk yang memang diberi label `is_recommended==1` pada data aktual untuk kulit bertipe oily.

```python
def recall_at_k_content(recommendations, ds_test, target_skin=None, k=5):
    recommended_products = recommendations['product_name'].head(k).values
    actual_recommended = ds_test[
        (ds_test['skin_type'] == target_skin) &
        (ds_test['is_recommended'] == 1)
    ]['product_name'].unique()
    relevant = set(recommended_products) & set(actual_recommended)
    return len(relevant) / len(actual_recommended) if len(actual_recommended) > 0 else 0.0

recall = recall_at_k_content(recommendations, df_combined_test, target_skin)
```

Fungsi di atas mengukur berapa banyak dari produk yang seharusnya direkomendasikan untuk tipe kulit tertentu yang berhasil muncul dalam 5 rekomendasi teratas.  Fungsi `recall_at_k_content` menerima `recommendations`, data test, dan `target_skin`.

![Evaluation Recall](https://raw.githubusercontent.com/rfqgal/submission-ml-terapan-2/refs/heads/master/images/evaluation-recall.png)

Nilai `recall@K` yang didapatkan ternyata rendah walaupun `precision@K` tinggi, itu artinya kasus ini memiliki kemungkinan bahwa banyak produk yang seharusnya direkomendasikan namun tidak termasuk ke dalam Top 5. Selain itu mungkin fitur kurang representatif, sehingga perlu penyesuaian kembali mengenai fitur yang digunakan ke dalam model misalnya menambahkan fitur seperti `ingredients`.

Studi Kasus Data Iris : Manipulasi dan Ekspor Data
================
Ferdian Bangkit Wijaya,
05 October 2025

Langkah 0: Persiapan - Memuat Library Pertama, kita muat paket tidyverse
yang berisi dplyr, stringr, dan alat-alat penting lainnya.

``` r
# Opsi global untuk chunk kode:
# echo = TRUE -> menampilkan kode
# message = FALSE -> menyembunyikan pesan/notifikasi dari library
# warning = FALSE -> menyembunyikan peringatan
knitr::opts_chunk$set(echo = TRUE, message = FALSE, warning = FALSE)
library(tidyverse)
```

    ## Warning: package 'ggplot2' was built under R version 4.4.3

    ## Warning: package 'tibble' was built under R version 4.4.3

    ## Warning: package 'purrr' was built under R version 4.4.3

    ## Warning: package 'dplyr' was built under R version 4.4.3

    ## Warning: package 'stringr' was built under R version 4.4.3

    ## Warning: package 'forcats' was built under R version 4.4.3

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.1     ✔ stringr   1.5.2
    ## ✔ ggplot2   4.0.0     ✔ tibble    3.3.0
    ## ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ## ✔ purrr     1.1.0     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

Langkah 1: Memuat & Inspeksi Data Awal Kita akan menggunakan dataset
iris yang sudah tersedia di R. Untuk kemudahan, kita ubah menjadi format
tibble.

``` r
iris_df <- as_tibble(iris)
head(iris_df)
```

    ## # A tibble: 6 × 5
    ##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
    ##          <dbl>       <dbl>        <dbl>       <dbl> <fct>  
    ## 1          5.1         3.5          1.4         0.2 setosa 
    ## 2          4.9         3            1.4         0.2 setosa 
    ## 3          4.7         3.2          1.3         0.2 setosa 
    ## 4          4.6         3.1          1.5         0.2 setosa 
    ## 5          5           3.6          1.4         0.2 setosa 
    ## 6          5.4         3.9          1.7         0.4 setosa

``` r
glimpse(iris_df)
```

    ## Rows: 150
    ## Columns: 5
    ## $ Sepal.Length <dbl> 5.1, 4.9, 4.7, 4.6, 5.0, 5.4, 4.6, 5.0, 4.4, 4.9, 5.4, 4.…
    ## $ Sepal.Width  <dbl> 3.5, 3.0, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1, 3.7, 3.…
    ## $ Petal.Length <dbl> 1.4, 1.4, 1.3, 1.5, 1.4, 1.7, 1.4, 1.5, 1.4, 1.5, 1.5, 1.…
    ## $ Petal.Width  <dbl> 0.2, 0.2, 0.2, 0.2, 0.2, 0.4, 0.3, 0.2, 0.2, 0.1, 0.2, 0.…
    ## $ Species      <fct> setosa, setosa, setosa, setosa, setosa, setosa, setosa, s…

1.  Membuat Variabel Turunan (Derived Variables).  
    Tugas: Membuat kolom Petal.Area dari perkalian Petal.Length dan
    Petal.Width.

``` r
iris_df <- iris_df %>%
  mutate(Petal.Area = Petal.Length * Petal.Width)

# Verifikasi dengan menampilkan kolom-kolom terkait
head(select(iris_df, Petal.Length, Petal.Width, Petal.Area))
```

    ## # A tibble: 6 × 3
    ##   Petal.Length Petal.Width Petal.Area
    ##          <dbl>       <dbl>      <dbl>
    ## 1          1.4         0.2       0.28
    ## 2          1.4         0.2       0.28
    ## 3          1.3         0.2       0.26
    ## 4          1.5         0.2       0.3 
    ## 5          1.4         0.2       0.28
    ## 6          1.7         0.4       0.68

2.  Mengubah Nama Variabel (Rename)  
    Tugas: Mengubah nama kolom agar lebih konsisten (misal: Petal.Length
    menjadi Panjang_Petal).

``` r
iris_df <- iris_df %>%
  rename(
    Panjang_Sepal = Sepal.Length,
    Lebar_Sepal = Sepal.Width,
    Panjang_Petal = Petal.Length,
    Lebar_Petal = Petal.Width
  )

# Tampilkan nama kolom yang baru
names(iris_df)
```

    ## [1] "Panjang_Sepal" "Lebar_Sepal"   "Panjang_Petal" "Lebar_Petal"  
    ## [5] "Species"       "Petal.Area"

``` r
head(iris_df)
```

    ## # A tibble: 6 × 6
    ##   Panjang_Sepal Lebar_Sepal Panjang_Petal Lebar_Petal Species Petal.Area
    ##           <dbl>       <dbl>         <dbl>       <dbl> <fct>        <dbl>
    ## 1           5.1         3.5           1.4         0.2 setosa        0.28
    ## 2           4.9         3             1.4         0.2 setosa        0.28
    ## 3           4.7         3.2           1.3         0.2 setosa        0.26
    ## 4           4.6         3.1           1.5         0.2 setosa        0.3 
    ## 5           5           3.6           1.4         0.2 setosa        0.28
    ## 6           5.4         3.9           1.7         0.4 setosa        0.68

3.  Mengonversi Tipe Variabel  
    Tugas: Mengubah tipe data kolom Panjang_Petal dari numerik (dbl)
    menjadi karakter (chr).

``` r
iris_df <- iris_df %>%
  mutate(Panjang_Petal_Str = as.character(Panjang_Petal))

# Cek kembali struktur data untuk melihat perubahan tipe
glimpse(iris_df)
```

    ## Rows: 150
    ## Columns: 7
    ## $ Panjang_Sepal     <dbl> 5.1, 4.9, 4.7, 4.6, 5.0, 5.4, 4.6, 5.0, 4.4, 4.9, 5.…
    ## $ Lebar_Sepal       <dbl> 3.5, 3.0, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1, 3.…
    ## $ Panjang_Petal     <dbl> 1.4, 1.4, 1.3, 1.5, 1.4, 1.7, 1.4, 1.5, 1.4, 1.5, 1.…
    ## $ Lebar_Petal       <dbl> 0.2, 0.2, 0.2, 0.2, 0.2, 0.4, 0.3, 0.2, 0.2, 0.1, 0.…
    ## $ Species           <fct> setosa, setosa, setosa, setosa, setosa, setosa, seto…
    ## $ Petal.Area        <dbl> 0.28, 0.28, 0.26, 0.30, 0.28, 0.68, 0.42, 0.30, 0.28…
    ## $ Panjang_Petal_Str <chr> "1.4", "1.4", "1.3", "1.5", "1.4", "1.7", "1.4", "1.…

4.  Recode Kategori  
    Tugas: Menyingkat nama Species menjadi “S”, “VE”, dan “VI”.

``` r
iris_df <- iris_df %>%
  mutate(
    Species_Code = case_when(
      Species == "setosa"     ~ "S",
      Species == "versicolor"  ~ "VE",
      Species == "virginica"   ~ "VI"
    )
  )

# Tampilkan hasil recode
head(select(iris_df, Species, Species_Code))
```

    ## # A tibble: 6 × 2
    ##   Species Species_Code
    ##   <fct>   <chr>       
    ## 1 setosa  S           
    ## 2 setosa  S           
    ## 3 setosa  S           
    ## 4 setosa  S           
    ## 5 setosa  S           
    ## 6 setosa  S

5.  Membuat Variabel Logika  
    Tugas: Membuat kolom Is_Panjang (TRUE/FALSE) jika Panjang_Petal \>
    5.

``` r
iris_df <- iris_df %>%
  mutate(Is_Panjang = Panjang_Petal > 5)

# Tampilkan contoh hasil
select(iris_df, Panjang_Petal, Is_Panjang) %>% slice(c(50, 101, 106))
```

    ## # A tibble: 3 × 2
    ##   Panjang_Petal Is_Panjang
    ##           <dbl> <lgl>     
    ## 1           1.4 FALSE     
    ## 2           6   TRUE      
    ## 3           6.6 TRUE

6.  Operasi String  
    Tugas: Mengubah nama Species menjadi huruf kapital semua.

``` r
iris_df <- iris_df %>%
  mutate(Species_Upper = str_to_upper(Species))

# Tampilkan hasil operasi string
head(select(iris_df, Species, Species_Upper))
```

    ## # A tibble: 6 × 2
    ##   Species Species_Upper
    ##   <fct>   <chr>        
    ## 1 setosa  SETOSA       
    ## 2 setosa  SETOSA       
    ## 3 setosa  SETOSA       
    ## 4 setosa  SETOSA       
    ## 5 setosa  SETOSA       
    ## 6 setosa  SETOSA

7.  Identifikasi Duplikat  
    Tugas: Menemukan dan menghitung baris yang identik dalam dataset.

``` r
jumlah_duplikat <- sum(duplicated(iris_df))

# Tampilkan hasilnya
print(paste("Jumlah baris duplikat yang ditemukan:", jumlah_duplikat))
```

    ## [1] "Jumlah baris duplikat yang ditemukan: 1"

``` r
# Filter baris yang terduplikasi dari awal ATAU dari akhir
semua_baris_terlibat <- iris_df %>%
  filter(duplicated(.) | duplicated(., fromLast = TRUE)) %>%
  arrange(Panjang_Petal, Lebar_Petal) # Diurutkan agar mudah dibandingkan

# Tampilkan hasilnya
print(semua_baris_terlibat)
```

    ## # A tibble: 2 × 10
    ##   Panjang_Sepal Lebar_Sepal Panjang_Petal Lebar_Petal Species   Petal.Area
    ##           <dbl>       <dbl>         <dbl>       <dbl> <fct>          <dbl>
    ## 1           5.8         2.7           5.1         1.9 virginica       9.69
    ## 2           5.8         2.7           5.1         1.9 virginica       9.69
    ## # ℹ 4 more variables: Panjang_Petal_Str <chr>, Species_Code <chr>,
    ## #   Is_Panjang <lgl>, Species_Upper <chr>

8.  Subsetting & Sorting  
    Tugas: Memilih (filter) bunga versicolor, memilih (select) kolom
    Species dan Panjang_Petal, lalu mengurutkan (arrange) dari yang
    terpanjang.

``` r
subset_sorted_df <- iris_df %>%
  filter(Species == "versicolor") %>%
  select(Species, Panjang_Petal) %>%
  arrange(desc(Panjang_Petal))

# Tampilkan hasil subsetting dan sorting
head(subset_sorted_df)
```

    ## # A tibble: 6 × 2
    ##   Species    Panjang_Petal
    ##   <fct>              <dbl>
    ## 1 versicolor           5.1
    ## 2 versicolor           5  
    ## 3 versicolor           4.9
    ## 4 versicolor           4.9
    ## 5 versicolor           4.8
    ## 6 versicolor           4.8

9.  Menggabungkan Data (Merge/Join)  
    Tugas: Membuat tabel baru berisi informasi habitat, lalu
    menggabungkannya ke data utama.

``` r
# Membuat dataframe baru untuk digabungkan
habitat_info <- tibble(
  Species = c("setosa", "versicolor", "virginica"),
  Habitat = c("Sunny Meadow", "Wetland", "Forest Edge")
)

# Menggabungkan dengan left_join
iris_final_df <- iris_df %>%
  left_join(habitat_info, by = "Species")

# Tampilkan contoh hasil akhir dengan kolom Habitat yang baru
head(select(iris_final_df, Species, Habitat, Panjang_Petal))
```

    ## # A tibble: 6 × 3
    ##   Species Habitat      Panjang_Petal
    ##   <chr>   <chr>                <dbl>
    ## 1 setosa  Sunny Meadow           1.4
    ## 2 setosa  Sunny Meadow           1.4
    ## 3 setosa  Sunny Meadow           1.3
    ## 4 setosa  Sunny Meadow           1.5
    ## 5 setosa  Sunny Meadow           1.4
    ## 6 setosa  Sunny Meadow           1.7

10. Ekspor Data ke CSV  
    Tugas: Menyimpan dataframe final (iris_final_df) ke dalam sebuah
    file CSV yang universal. CSV (Comma-Separated Values) adalah format
    teks sederhana yang bisa dibuka oleh hampir semua software analisis
    data.

``` r
# Fungsi write_csv() dari paket readr (bagian dari tidyverse)
# akan membuat file CSV di direktori kerja Anda.
write_csv(iris_final_df, "iris_data_final.csv")

print("File iris_data_final.csv berhasil dibuat.")
```

    ## [1] "File iris_data_final.csv berhasil dibuat."

11. Ekspor Data ke Excel  
    Tugas: Menyimpan dataframe final ke dalam format file Excel (.xlsx),
    yang sangat umum digunakan di lingkungan bisnis. Untuk melakukan
    ini, kita memerlukan paket tambahan seperti writexl.

``` r
# Jika paket 'writexl' belum terinstal, jalankan baris di bawah ini sekali.
# install.packages("writexl")

# Muat library
library(writexl)

# Gunakan fungsi write_xlsx() untuk membuat file Excel
write_xlsx(iris_final_df, "iris_data_final.xlsx")

print("File iris_data_final.xlsx berhasil dibuat.")
```

    ## [1] "File iris_data_final.xlsx berhasil dibuat."

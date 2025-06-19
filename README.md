# speech_classification
# Proyek Klasifikasi Suara Tiruan Hewan dengan CNN

Proyek ini bertujuan untuk membangun dan melatih model *Convolutional Neural Network* (CNN) untuk mengklasifikasikan lima jenis suara tiruan hewan yang berbeda.

## Daftar Kelas Suara

Model ini dilatih untuk mengenali suara tiruan dari hewan-hewan berikut:
1.  **Sapi**: `moo`
2.  **Kucing**: `meow`
3.  **Anjing**: `woof`
4.  **Kambing**: `mbee`
5.  **Burung**: `tweet`

## Arsitektur & Alur Kerja

1.  **Dataset**: Dataset dibuat dari rekaman audio berdurasi 2 detik dengan sample rate 32000 Hz. Untuk kemudahan, notebook ini menyediakan fungsi untuk mensimulasikan dataset menggunakan noise putih.

2.  **Pra-pemrosesan**: Setiap file audio melalui beberapa tahap pra-pemrosesan:
    * **Voice Activity Detection (VAD)**: Untuk menghilangkan bagian yang hening.
    * **Normalisasi**: Menyamakan panjang dan amplitudo setiap sampel.
    * **Ekstraksi Fitur**: Mengubah audio menjadi spektogram **MFCC** (Mel-Frequency Cepstral Coefficients) dengan 40 koefisien. Fitur ini sangat baik dalam merepresentasikan karakteristik suara yang relevan untuk klasifikasi.

3.  **Model CNN**: Arsitektur yang digunakan adalah CNN sederhana dengan:
    * Dua lapisan konvolusi untuk ekstraksi pola dari MFCC.
    * Fungsi aktivasi ReLU dan lapisan Max-Pooling.
    * Satu lapisan *fully connected* di akhir untuk menghasilkan probabilitas klasifikasi ke dalam 5 kelas.

4.  **Pelatihan**: Model dilatih menggunakan *optimizer* Adam dan *loss function* Cross-Entropy selama 100 epoch.

## Cara Menjalankan

1.  **Lingkungan**: Notebook ini dapat dijalankan di Google Colab atau lingkungan Jupyter lokal.
2.  **Instalasi**: Jalankan sel pertama di notebook untuk menginstal semua library yang diperlukan (`torch`, `librosa`, `sounddevice`, dll.).
3.  **Jalankan Semua Sel**: Anda dapat menjalankan semua sel secara berurutan. Dataset akan disimulasikan secara otomatis, sehingga model dapat langsung dilatih dan dievaluasi.
4.  **(Opsional) Gunakan Dataset Anda**:
    * Buat folder `./data/`.
    * Di dalamnya, buat subfolder untuk setiap kelas: `Cow`, `Cat`, `Dog`, `Goat`, `Bird`.
    * Isi setiap folder dengan file audio `.wav` dari suara tiruan yang sesuai.
    * Lewati (atau hapus) sel "Simulasi Dataset" dan jalankan sisa notebook.

## Hasil

Pada dataset simulasi yang kecil (50 sampel train, 25 sampel test), model ini mampu mencapai **akurasi 100%** pada data testing. Hal ini menunjukkan bahwa arsitektur model dan alur kerja pra-pemrosesan sudah tepat.

## Pengembangan Lanjutan

* **Dataset Lebih Besar**: Menguji model pada dataset yang jauh lebih besar dan bervariasi untuk mengukur performa yang lebih akurat.
* **Augmentasi Data**: Menerapkan teknik augmentasi seperti *pitch shifting*, *time stretching*, dan penambahan noise untuk membuat model lebih robust.
* **Arsitektur Lebih Kompleks**: Mencoba arsitektur yang lebih dalam seperti ResNet atau menggunakan model berbasis Transformer untuk audio.

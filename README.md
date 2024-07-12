# PCD_UAS_202231103_2024_ITPLN
```pyton
import cv2
import numpy as np
from matplotlib import pyplot as plt
```
Dengan menggunakan ketiga modul ini kita dapat melakukan berbagai tugas pengolahan gambar, 
seperti membaca gambar, melakukan operasi matematika pada citra (menggunakan NumPy), 
dan menampilkan hasilnya dalam plot atau grafik (menggunakan matplotlib.pyplot).
```
image = cv2.imread('agil.jpg')
```
Kode cv2.imread('agil.jpg') digunakan untuk membaca gambar dengan nama file 'agil.jpg' 
menggunakan OpenCV. Fungsi ini mengembalikan sebuah array NumPy yang mewakili gambar tersebut.
```
# Median Filtering
median_filtered = cv2.medianBlur(image, 5)
```
cv2.medianBlur(image, 5) digunakan untuk menerapkan filter median pada gambar image dengan ukuran kernel 5x5.
```
# Menampilkan hasil
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1), plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)), plt.title('citra asli')
plt.subplot(1, 2, 2), plt.imshow(cv2.cvtColor(median_filtered, cv2.COLOR_BGR2RGB)), plt.title('After Median Filtering')
plt.show()
```
plt.figure(figsize=(10, 5)) untuk Membuat sebuah gambar (figure) dengan ukuran 10x5 inch.
plt.subplot(1, 2, 1), plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)), plt.title('citra asli') untuk membuat subplot pertama (1 baris, 2 kolom, posisi 1) dan menampilkan gambar asli. 
Fungsi cv2.cvtColor digunakan untuk mengubah format warna dari BGR (format bawaan OpenCV) menjadi RGB (format yang lebih umum digunakan dalam matplotlib).
plt.subplot(1, 2, 2), plt.imshow(cv2.cvtColor(median_filtered, cv2.COLOR_BGR2RGB)), plt.title('After Median Filtering') untuk membuat subplot kedua (1 baris, 2 kolom, posisi 2) dan menampilkan gambar setelah proses median filtering.
Kita perlu mengganti median_filtered dengan variabel yang sesuai yang berisi hasil dari proses median filtering gambar.
plt.show() untuk menampilkan gambar-gambar yang sudah ditentukan dalam figure yang telah dibuat sebelumnya.
```
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
```
cv2.cvtColor(image, cv2.COLOR_BGR2GRAY) digunakan untuk mengubah gambar berwarna (BGR) menjadi citra keabuan (grayscale).
```
def mean_filter(image, kernel_size):
    # Mendapatkan dimensi gambar
    h, w = image.shape
    
    # Membuat padding untuk gambar
    pad_size = kernel_size // 2
    padded_image = cv2.copyMakeBorder(image, pad_size, pad_size, pad_size, pad_size, cv2.BORDER_CONSTANT, value=0)
    
    # Membuat hasil gambar kosong
    mean_filtered = np.zeros_like(image)
    
    # Melakukan mean filtering
    for i in range(h):
        for j in range(w):
            # Mengambil nilai dari kernel
            kernel = padded_image[i:i+kernel_size, j:j+kernel_size]
            mean_value = np.mean(kernel)
            mean_filtered[i, j] = mean_value
    
    return mean_filtered
```
mean_filter yang saya tulis adalah untuk melakukan proses mean filtering pada gambar grayscale dengan ukuran kernel yang ditentukan.
h dan w digunakan untuk menyimpan tinggi (height) dan lebar (width) gambar.
Padding (penambahan tepi) dilakukan pada gambar dengan ukuran kernel_size // 2. Hal ini dilakukan agar dapat melakukan operasi filtering pada piksel di pinggiran gambar tanpa terjadi out-of-bounds error. 
Fungsi cv2.copyMakeBorder digunakan untuk membuat padding dengan nilai piksel konstan.
mean_filtered dibuat sebagai array kosong dengan ukuran yang sama seperti gambar input (image), yang akan menyimpan hasil dari mean filtering.
(for i in range(h) dan for j in range(w)), dilakukan iterasi untuk setiap piksel dalam gambar. Pada setiap iterasi, sebuah kernel dengan ukuran kernel_size x kernel_size diambil dari gambar yang telah dipad. 
Nilai rata-rata dari kernel ini dihitung menggunakan np.mean dan disimpan ke dalam mean_filtered.
mean_filtered ini fungsinya mengambil gambar hasil mean filtering.
```
mean_filtered = mean_filter(gray_image, 5)
```
mean_filter untuk melakukan mean filtering pada gray_image dengan ukuran kernel 5x5.
```
# Menampilkan hasil
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1), plt.imshow(gray_image, cmap='gray'), plt.title('Original Image')
plt.subplot(1, 2, 2), plt.imshow(mean_filtered, cmap='gray'), plt.title('Mean Filtered')
plt.show()
```
plt.figure(figsize=(10, 5)) ini digunakan untuk membuat sebuah figure (gambar) dengan ukuran 10x5 inch.
plt.subplot(1, 2, 1) dan plt.subplot(1, 2, 2) digunakan untuk membuat dua subplot secara berdampingan (1 baris, 2 kolom).
plt.imshow(gray_image, cmap='gray') ini digunakan untuk menampilkan gambar asli dalam mode keabuan (grayscale).
plt.imshow(mean_filtered, cmap='gray') ini digunakan untuk menampilkan gambar hasil mean filtering juga dalam mode keabuan.
plt.title('Original Image') dan plt.title('Mean Filtered') ini digunakan untuk memberikan judul pada masing-masing subplot.

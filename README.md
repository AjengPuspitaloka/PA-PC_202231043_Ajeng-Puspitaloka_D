# PA-PC_202231043_Ajeng Puspitaloka_D
### Mengimpor Library
import cv2
import matplotlib.pyplot as plt
import numpy as np

Library `cv2` adalah OpenCV yang digunakan untuk pengolahan citra, `matplotlib.pyplot` digunakan untuk visualisasi data dalam bentuk grafis, dan `numpy` digunakan untuk komputasi numerik yang mendukung array besar dan matriks.

### Membaca Citra
image = cv2.imread('Ajeng.jpg')

Pada bagian ini, file gambar dengan nama 'Ajeng.jpg' dibaca menggunakan fungsi cv2.imread dari library OpenCV. Fungsi ini mengambil nama file gambar sebagai parameter dan mengembalikan citra dalam bentuk array numerik yang berisi data piksel. Hasil dari pembacaan gambar ini kemudian disimpan dalam variabel image untuk digunakan dalam pemrosesan lebih lanjut. 

### Fungsi untuk Menampilkan Citra
  def display_images(images, titles):
    plt.figure(figsize=(15, 10))
    for i in range(len(images)):
        plt.subplot(2, 3, i+1)
        plt.imshow(cv2.cvtColor(images[i], cv2.COLOR_BGR2RGB))
        plt.title(titles[i])
        plt.axis('off')
    plt.show()
    
Perintah `plt.figure(figsize=(15, 10))` digunakan untuk mengatur ukuran kanvas tempat citra akan ditampilkan, memastikan bahwa seluruh gambar akan terlihat dengan jelas pada kanvas yang lebih besar. Kemudian, perintah `plt.subplot(2, 3, i+1)` digunakan untuk membagi kanvas menjadi 2 baris dan 3 kolom, serta memilih posisi subplot berdasarkan indeks `i`. Hal ini memungkinkan untuk menampilkan beberapa gambar dalam satu kanvas dengan susunan yang rapi. Perintah `plt.imshow(cv2.cvtColor(images[i], cv2.COLOR_BGR2RGB))` menampilkan citra setelah mengubah warnanya dari format BGR (yang digunakan oleh OpenCV) ke format RGB (yang digunakan oleh Matplotlib), sehingga warna pada gambar terlihat seperti aslinya. Selanjutnya, perintah `plt.title(titles[i])` memberikan judul pada setiap subplot sesuai dengan daftar `titles`, membantu dalam mengidentifikasi setiap gambar. Perintah `plt.axis('off')` digunakan untuk menonaktifkan tampilan sumbu pada subplot, sehingga gambar terlihat lebih bersih tanpa gangguan garis sumbu. Akhirnya, perintah `plt.show()` digunakan untuk menampilkan semua subplot yang telah diatur, sehingga semua gambar dan judulnya muncul pada kanvas sesuai dengan yang telah diatur sebelumnya.

### Menyalin Citra Asli
original = image.copy()

Untuk membuat salinan dari citra asli dan menyimpannya dalam variabel `original`, dapat menggunakan metode copy() yang disediakan oleh pustaka pemrosesan citra seperti OpenCV. Pertama, memuat citra asli ke dalam memori menggunakan perintah seperti `cv2.imread('path_to_image')`, yang akan mengembalikan matriks piksel dari citra tersebut. Setelah citra asli berada dalam memori, dapat menggunakan metode `copy()` pada objek citra tersebut untuk membuat salinan yang terpisah. Ini berarti setiap perubahan yang dilakukan pada salinan tidak akan mempengaruhi citra asli. 

### Rotasi Citra
(h, w) = image.shape[:2]
center = (w // 2, h // 2)
M = cv2.getRotationMatrix2D(center, 45, 1.0)
rotated = cv2.warpAffine(image, M, (w, h))

Dalam proses rotasi citra menggunakan OpenCV Pertama, `image.shape[:2]` digunakan untuk mendapatkan tinggi (h) dan lebar (w) dari citra yang akan dirotasi. Kemudian, titik pusat rotasi ditentukan dengan `center = (w // 2, h // 2)`, yang menempatkan pusat rotasi di tengah-tengah citra. Selanjutnya, `cv2.getRotationMatrix2D(center, 45, 1.0)` digunakan untuk membuat matriks rotasi sebesar 45 derajat dengan faktor skala 1.0. Matriks rotasi ini akan digunakan oleh `cv2.warpAffine(image, M, (w, h))` untuk menerapkan transformasi rotasi pada citra. Dengan demikian, proses ini menghasilkan citra yang telah diputar sebesar 45 derajat dengan pusat rotasi di tengah-tengah citra, menggunakan matriks rotasi yang telah dibuat.

### Mengubah Ukuran Citra (Resize)
new_height = int(h * 1.5)
new_width = w
resized = cv2.resize(image, (new_width, new_height))

new_height = int(h * 1.5)` digunakan untuk menghitung tinggi baru (`new_height`) dari citra, yang diperbesar sebesar 1,5 kali dari tinggi aslinya (`h`). Ini memastikan bahwa citra akan memiliki tinggi yang lebih besar setelah diubah ukurannya. Kemudian, `new_width = w` menetapkan lebar baru (`new_width`) dari citra tetap sama dengan lebar aslinya (`w`), sehingga hanya tinggi citra yang berubah. Setelah itu, `cv2.resize(image, (new_width, new_height))` digunakan untuk mengubah ukuran citra (`image`) menjadi ukuran baru yang telah ditentukan `(new_width, new_height)`. Proses ini menghasilkan citra yang diperbesar secara proporsional sesuai dengan perhitungan tinggi baru yang telah ditentukan sebelumnya.

### Memotong Citra (Crop)
cropped = image[50:200, 50:200]

Operasi image[50:200, 50:200] pada citra untuk memproses pemotongan citra dari titik koordinat (50, 50) hingga (200, 200). Ini mengartikan hanya bagian citra yang terletak di dalam jangkauan baris 50 hingga 200 dan kolom 50 hingga 200 yang akan dipertahankan, sementara bagian lain dari citra akan dihapus atau diabaikan.

### Membalik Citra (Flip)
flipped = cv2.flip(image, 1)

Fungsi `cv2.flip(image, 1)` merupakan bagian dari pustaka OpenCV dalam bahasa Python yang digunakan untuk memproses gambar dan video. Ketika diterapkan pada suatu gambar (`image`), parameter kedua (`1`) menunjukkan bahwa operasi tersebut akan membalikkan citra secara horizontal. Hasilnya adalah citra yang akan diputar 180 derajat mengikuti sumbu vertikal tengahnya, menciptakan efek cermin dari kiri ke kanan. Operasi ini berguna dalam banyak aplikasi pengolahan gambar, termasuk augmentasi data dalam pembelajaran mesin atau pengolahan citra untuk analisis visual.

### Menggeser Citra (Translate)
M = np.float32([[1, 0, 50], [0, 1, 100]])
translated = cv2.warpAffine(image, M, (w, h))

Pertama, `np.float32([[1, 0, 50], [0, 1, 100]])` adalah kode yang menggunakan NumPy untuk membuat matriks translasi. Dalam matriks ini digunakan untuk menggeser citra sejauh 50 piksel ke kanan dan 100 piksel ke bawah. Angka 1 di diagonal utama menunjukkan bahwa tidak ada perubahan skala, sementara nilai 50 dan 100 pada kolom terakhir menunjukkan geseran horizontal dan vertikal yang diinginkan.

Kedua, `cv2.warpAffine(image, M, (w, h))` adalah fungsi dari OpenCV yang menerapkan transformasi geometris ke citra. Dalam hal ini, parameter `M` adalah matriks translasi yang telah dibuat sebelumnya, `image` adalah citra yang akan digeser, dan `(w, h)` adalah ukuran citra hasil. Dengan menggunakan matriks translasi yang sesuai, fungsi ini secara efektif menggeser citra sesuai dengan spesifikasi yang diinginkan, seperti dalam contoh untuk menggeser 50 piksel ke kanan dan 100 piksel ke bawah.

### Menampilkan Semua Citra yang Telah Diolah
images = [original, rotated, resized, cropped, flipped, translated]
titles = ['Citra Asli', 'After Rotated', 'After Resized', 'After Cropped', 'After Flipped', 'After Translated']
display_images(images, titles)

variabel `images` adalah sebuah daftar yang berisi citra-citra yang telah mengalami berbagai proses pengolahan seperti rotasi, perubahan ukuran, pemotongan, pembalikan, dan translasi. Sementara itu, variabel `titles` adalah daftar yang memuat judul untuk setiap citra dalam `images`. Ketika fungsi `display_images(images, titles)` dipanggil, ini menghasilkan tampilan visual dari semua citra dalam `images` dengan judul yang sesuai untuk masing-masing citra. Fungsi ini berguna untuk menampilkan hasil dari berbagai manipulasi citra dalam satu tampilan yang terstruktur, mempermudah untuk evaluasi dan analisis hasil pengolahan gambar secara bersamaan.

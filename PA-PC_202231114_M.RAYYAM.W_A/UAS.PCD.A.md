Teori Transformasi Geometris
- Transformasi geometris adalah manipulasi dasar yang diterapkan pada gambar digital untuk mengubah posisinya di dalam ruang gambar. Operasi seperti rotasi, translasi, pembesaran/pengurangan, dan pembalikan gambar adalah contoh dari transformasi geometris.

- Rotasi (Rotation): Memutar gambar sekitar suatu titik tertentu (biasanya pusat gambar). Rotasi memerlukan penggunaan matriks rotasi, yang didasarkan pada trigonometri (sudut rotasi).
- Translasi (Translation): Menggeser gambar dari satu posisi ke posisi lain tanpa mengubah orientasi atau ukuran gambar.
- Pembesaran/Pengurangan (Scaling): Mengubah ukuran gambar dengan faktor tertentu. Scaling dilakukan dengan mengalikan koordinat piksel dengan faktor skala.
- Pembalikan (Flipping): Membalik gambar secara horizontal atau vertikal.

Teori Resampling
- Resampling digunakan ketika mengubah ukuran gambar. Teknik resampling mengubah jumlah piksel dalam gambar. Dua metode utama resampling adalah:

- Nearest Neighbor: Metode paling sederhana yang memilih piksel terdekat. Cepat tetapi dapat menghasilkan gambar yang kasar.
- Bilinear Interpolation: Menggunakan nilai rata-rata dari piksel terdekat untuk memperhalus gambar yang diubah ukurannya.
- Bicubic Interpolation: Metode yang lebih canggih yang menggunakan piksel-piksel terdekat dalam radius 4x4 untuk menghasilkan gambar yang lebih halus.

Teori Warna dan Konversi Ruang Warna
- Gambar digital sering disimpan dalam format warna tertentu, seperti RGB (Red, Green, Blue). OpenCV menggunakan format BGR secara default. Saat menampilkan gambar dengan Matplotlib, konversi dari BGR ke RGB diperlukan karena Matplotlib menggunakan format RGB.

``` codingan ```

``` bash
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
Baris ini mengimpor tiga pustaka yang akan digunakan dalam kode:

- cv2 untuk operasi pengolahan citra menggunakan OpenCV.
- numpy (diimpor sebagai np) untuk operasi numerik.
- matplotlib.pyplot (diimpor sebagai plt) untuk menampilkan gambar.

```bash
image_original = cv2.imread('rayyan.jpeg')
```
Baris ini memuat gambar asli dari file rayyan.jpeg ke dalam variabel image_original menggunakan fungsi cv2.imread().

```bash
plt.subplot(2, 3, 1)
plt.imshow(cv2.cvtColor(image_original, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')
```
Bagian ini menampilkan gambar asli:

- plt.subplot(2, 3, 1) membuat subplot pada posisi pertama dari grid 2x3.
- plt.imshow(cv2.cvtColor(image_original, cv2.COLOR_BGR2RGB)) mengonversi gambar dari BGR (format default OpenCV) ke RGB (format yang digunakan Matplotlib) dan menampilkannya.
- plt.title('Original Image') memberi judul pada subplot.
- plt.axis('off') menghilangkan sumbu dari subplot.

```bash
# Rotate the image by 45 degrees
(h_rot, w_rot) = image_original.shape[:2]
center_rot = (w_rot // 2, h_rot // 2)
M_rot = cv2.getRotationMatrix2D(center_rot, 45, 1.0)
image_rotated = cv2.warpAffine(image_original, M_rot, (w_rot, h_rot))
plt.subplot(2, 3, 2)
plt.imshow(cv2.cvtColor(image_rotated, cv2.COLOR_BGR2RGB))
plt.title('Rotated Image')
plt.axis('off')
```
Bagian ini memutar gambar sebesar 45 derajat:

- (h_rot, w_rot) = image_original.shape[:2] mendapatkan tinggi dan lebar gambar.
- center_rot = (w_rot // 2, h_rot // 2) menentukan pusat rotasi.
- M_rot = cv2.getRotationMatrix2D(center_rot, 45, 1.0) membuat matriks rotasi untuk rotasi 45 derajat.
- image_rotated = cv2.warpAffine(image_original, M_rot, (w_rot, h_rot)) menerapkan matriks rotasi pada gambar asli.
- Subplot kedua dibuat dan gambar yang telah diputar ditampilkan dengan cara yang sama seperti sebelumnya.

```bash
# Resize the image to half its original size
image_resized = cv2.resize(image_original, (image_original.shape[1]//3, image_original.shape[0]//2))
plt.subplot(2, 3, 3)
plt.imshow(cv2.cvtColor(image_resized, cv2.COLOR_BGR2RGB))
plt.title('Resized Image')
plt.axis('off')
```
Bagian ini mengubah ukuran gambar menjadi setengah dari ukuran aslinya:

- image_resized = cv2.resize(image_original, (image_original.shape[1]//3, image_original.shape[0]//2)) mengubah ukuran gambar menggunakan fungsi cv2.resize().
- Subplot ketiga dibuat dan gambar yang telah diubah ukurannya ditampilkan.

```bash
# Crop the image to a specific region (e.g., top-left quarter)
image_cropped = image_original[0:image_original.shape[0]//2, 0:image_original.shape[1]//2]
plt.subplot(2, 3, 4)
plt.imshow(cv2.cvtColor(image_cropped, cv2.COLOR_BGR2RGB))
plt.title('Cropped Image')
plt.axis('off')
```
Bagian ini memotong gambar menjadi wilayah tertentu (kuartal kiri atas):

- image_cropped = image_original[0:image_original.shape[0]//2, 0:image_original.shape[1]//2] memotong gambar dari koordinat (0,0) hingga setengah tinggi dan lebar.
- Subplot keempat dibuat dan gambar yang telah dipotong ditampilkan.

```bash
# Flip the image horizontally
image_flipped = cv2.flip(image_original, 1)
plt.subplot(2, 3, 5)
plt.imshow(cv2.cvtColor(image_flipped, cv2.COLOR_BGR2RGB))
plt.title('Flipped Image')
plt.axis('off')
```
Bagian ini membalik gambar secara horizontal:

- image_flipped = cv2.flip(image_original, 1) membalik gambar secara horizontal.
- Subplot kelima dibuat dan gambar yang telah dibalik ditampilkan.

```bash
# Translate the image by 50 pixels to the right and 20 pixels down
rows_trans, cols_trans = image_original.shape[:2]
M_translate = np.float32([[1, 0, 250], [0, 1, 180]])
image_translated = cv2.warpAffine(image_original, M_translate, (cols_trans, rows_trans))
plt.subplot(2, 3, 6)
plt.imshow(cv2.cvtColor(image_translated, cv2.COLOR_BGR2RGB))
plt.title('Translated Image')
plt.axis('off')
```
Bagian ini mentranslasi (menggeser) gambar sebesar 250 piksel ke kanan dan 180 piksel ke bawah:

- rows_trans, cols_trans = image_original.shape[:2] mendapatkan tinggi dan lebar gambar.
- M_translate = np.float32([[1, 0, 250], [0, 1, 180]]) membuat matriks translasi untuk menggeser gambar.
- image_translated = cv2.warpAffine(image_original, M_translate, (cols_trans, rows_trans)) menerapkan matriks translasi pada gambar asli.
- Subplot keenam dibuat dan gambar yang telah ditranslasi ditampilkan.

```bash
plt.tight_layout()
plt.show()
```
- Fungsi plt.tight_layout() adalah fungsi dari pustaka Matplotlib yang digunakan untuk secara otomatis menyesuaikan subplots sehingga mereka tidak saling tumpang tindih
- Fungsi plt.show() adalah fungsi yang digunakan untuk menampilkan semua plot yang telah saya buat.
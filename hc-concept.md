# Clustering

Clustering merupakan salah satu metode yang termasuk kedalam unsupervised learning. Clustering bertujuan untuk melakukan pengelompokan pada suatu set data yang memiliki kemiripan berdasarkan jarak terdekatnya. Clustering memiliki karakteristik dimana anggota dalam satu cluster memiliki kemiripan yang sama atau jarak yang sangat dekat, namun anggota antar cluster memiliki kemiripan yang sangat berbeda atau jarak yang sangat jauh.

Menurut Tan,PN dalam bukunya yang berjudul *Introduction to Data Mining*, metode clustering dibagi menjadi dua jenis, yaitu Hierarchical Clustering dan Partitional Clustering[^1]. 

**Partitional Clustering** umumnya bertujuan untuk mengelompokkan data menjadi beberapa cluster yang lebih kecil[^2]. Pada prosesnya, setiap cluster akan memiliki titik pusat cluster (centroid) dan mencoba menghitung setiap data yang paling dekat dengan centroid tersebut. Metode dalam partitional clustering diantaranya k-means, fuzzy k-means, dan mixture modelling.

![](image/partitional.png)

Sedangkan dalam **Hierarchical Clustering**, pengelompokan data dilakukan dengan membuat suatu diagram hirarkis (*dendrogram*) dengan tujuan menunjukkan kemiripan antar data[^2]. Setiap data yang mirip akan memiliki hubungan hirarkis yang dekat, dan dendogram terus terbentuk hingga dihasilkan satu kelompok besar. Cluster dapat dihasilkan dengan memotong struktur hirarkis pada level tertentu. Beberapa metode dalam hierarchical clustering yaitu **single linkage**, **complete linkage**, **average linkage**, dan **ward's minimum variance**.

![](image/hc.png)

Pada kesempatan kali ini kita akan mendalami terkait Hierarchical Clustering serta aplikasinya untuk pengolahan data.

# Hierarchical Clustering

Secara umum, hierarchical clustering dibagi menjadi dua jenis yaitu *agglomerative* dan *divisive*[^3]. Kedua metode ini dibedakan berdasarkan cara dalam melakukan pengelompokkannya dalam bentuk bagan hirarki, menggunakan bottom-up atau top-down manner.

1. **Agglomerative clustering** 

Agglomerative clustering biasa disebut juga sebagai agglomerative nesting (AGNES) dimana cara kerja dalam melakukan pengelompokan hirarki menggunakan **bottom-up manner**. Prosesnya dimulai dengan menganggap setiap data sebagai 1 cluster kecil (leaf) yang hanya memiliki 1 anggota saja, lalu pada tahap selanjutnya dua cluster yang memiliki kemiripan akan dikelompokkan menjadi 1 cluster yang lebih besar (nodes). Proses ini akan dilakukan terus menerus hingga semua data menjadi satu cluster besar (root). 

2. **Divisive hierarchical clustering**

Divisive hierarchical clustering biasa disebut juga sebagai divisive analysis (DIANA) dimana cara kerja dalam mengelompokkan data menggunakan **top-down manner**. Prosesnya dimulai dengan menganggap satu set data sebagai satu cluster besar (root), lalu dalam setiap iterasinya setiap data yang memiliki karakteristik yang berbeda akan dipecah menjadi 2 cluster yang lebih kecil (nodes) dan proses akan terus berjalan hingga setiap data menjadi 1 cluster kecil (leaf) yang hanya memiliki 1 anggota saja.

Berikut ini perbedaan cara kerja agglomerative dan divisive clustering bekerja.

![](image/agnes-vs-diana.png)

Selain memahami proses pembuatan dendogramnya, mari coba memahami bagaimana node-node (tiap cluster) terbuat dan digabungkan.

Tujuan dari clustering secara umum, baik hierarchical maupun partitional clustering adalah untuk membuat cluster yang memiliki karakteristik yang sama dalam satu anggota cluster dan memiliki karakteristik yang berbeda antar clusternya. Konsep inilah yang mengharuskan proses pembuatan cluster untuk memperhatikan **(dis)similarity** / ukuran ketidakmiripan antar clusternya. 

Tingkat (dis)similarity antar anggota cluster dapat direpresentasikan dengan **jarak** (atau beberapa menyebutnya **distance matrix**). Terdapat beragam pilihan distance matrix yang pemakaiannya bergantung pada tipe data/topik analisis yang sedang digunakan (euclidean distance, manhattan, dst)[^3]. Bacaan lebih lanjut tentang beragam tipe distance matrix dapat dilihat [disini](https://people.revoledu.com/kardi/tutorial/Similarity/index.html).

Dalam hierarchical clustering, selain menghitung (dis)similarity antar observasi, diperlukan juga cara untuk menghitung (dis)similarity antar 2 cluster observasi sehingga dapat terbentuk dendogram dari cluster-cluster yang ada. Proses penggabungan cluster-cluster kecil menjadi satu dendogram utuh dilakukan menggunakan **linkage method**. Berikut ini beberapa jenis linkage method yang sering digunakan:

1. **Complete Linkage** / **Maximum Linkage**
2. **Single Linkage** / **Minimum Linkage**
3. **Average Linkage**
4. **Centroid Linkage**
5. **Ward's minimum Variance**

## Complete/Maximum Linkage

Pengukuran (dis)similarity atau jarak antar cluster dilakukan dengan mengukur terlebih dahulu jarak antar tiap observasi dari cluster yang berbeda (**pairwise distances**). Kemudian, jarak paling tinggi (maximum distance) akan menjadi ukuran (dis)similarity antar cluster. Hal ini membuat dendogram yang terbentuk menjadi lebih terpisah antar clusternya (terbentuk cluster yang "compact").

## Single/Minimum Linkage

Pengukuran (dis)similarity atau jarak antar cluster dilakukan dengan mengukur terlebih dahulu jarak antar tiap observasi dari cluster yang berbeda pairwise distances. Kemudian, jarak paling kecil (minimum distance) akan menjadi ukuran (dis)similarity antar cluster. Hal ini membuat dendogram yang terbentuk menjadi lebih "loose" atau berdekatan antar clusternya.

## Average Linkage

Pengukuran (dis)similarity atau jarak antar cluster dilakukan dengan mengukur terlebih dahulu jarak antar tiap observasi dari cluster yang berbeda pairwise distances. Kemudian, dihitung rata-rata jarak dari pairwise distance tersebut dan nilai tersebut akan menjadi ukuran (dis)similarity antar cluster.

Berikut adalah ilustrasi untuk kelima jenis linkage di atas[^4]:

![](image/linkage.png)

# Optimal Cluster

Setelah memahami bagaimana suatu hierarchical clustering dibuat, ada baiknya kita mengetahui parameter suatu hierarchical clustering dianggap baik, atau bagaiamana cara membuat cluster terbaik.

Pada kasus hierarchical clustering, kita dapat menentukan di level dendogram atau (dis)imilarity berapa akan dilakukan pemisahan sehingga terbentuk sebanyak `k` jumlah cluster.

Seperti halnya metode clustering lain, kebaikan cluster dapat dilihat dari seberapa mirip observasi yang berada dalam 1 cluster, dan seberapa berbeda observasi yang berasal dari clusster berbeda setelah percobaan beberapa nilai `k`. Secara umum terdapat 3 metode yang dapat digunakan:

1. **Elbow Method**
2. **Average Silhouette Method**
3. **Gap Statistic Method**

## Elbow Method

Nilai kemiripan data antar cluster dapat diwakilkan dengan nilai **total within-cluster sum of square** (Total WSS). Total WSS dapat diartikan sebagai jumlah dari jarak tiap observasi cluster ke nilai tengahnya (centroid). 

[Rumus/intuisi rumus?]

Nilai yang semakin rendah (mendekati nol) mengindikasikan antar data dalam satu cluster semakin mirip. Dapat dilakukan penghitungan total WSS untuk tiap jumlah cluster `k`. Kemudian ditentukan nilai `k` berdasarkan titik yang dimana ketika `k` ditambahkan, maka Total WSS tidak mengalami penurunan yang besar/cenderung landai.

[gambar]

## Average Silhouette Method

Nilai Silhouette adalah ukuran seberapa mirip suatu data dengan clusternya sendiri (kohesi) dibandingkan dengan cluster lain (separasi).

[Rumus/intuisi rumus?]

Nilai silhouette berkisar antara ???1 hingga +1. Nilai yang tinggi menunjukkan bahwa data-data sudah serupa dengan clusternya sendiri dan tidak mirip dengan cluster lain. Jika sebagian besar data memiliki nilai silhouette yang tinggi, maka konfigurasi pengelompokan sudah sesuai, bila banyak yang memiliki nilai rendah, maka konfigurasi pengelompokan belum sesuai (jumlah `k` terlalu banyak atau terlalu sedikit).

[gambar]

## Gap Statistic Method



Penjelasan lebih detail dapat dibaca [disini](https://uc-r.github.io/kmeans_clustering#optimal).

# Reference

[^1]: Tan, P.N., Steinbach, M., Kumar, V. (2006) Introduction to Data Mining. Boston: Pearson Education.

[^2]: Fred, A.L.N. dan Leitao, J.M.N. (2000) Partitional vs Hierarchical Clustering Using a Minimum Grammar Complexity Approach, di F.J. Ferri et al. (Eds.): SSPR&SPR 2000, LNCS 1876, hal. 193-202. Berlin: Springer-Verlag

[^3]: University of Cincinnati Business Analytics. UC Business Analytics R Programming Guide, Bab [Hierarchical Clustering](https://uc-r.github.io/hc_clustering)

[^4]: Rhys, H.I. (2020) [Machine Learning with R, the tidyverse, and mlr](https://livebook.manning.com/book/machine-learning-for-mortals-mere-and-otherwise/chapter-17/). USA: Manning Publications Co.


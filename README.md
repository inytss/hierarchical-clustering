# Hierarchical Clustering

Penjelasan terkait Introduction of Hierarchical Clustering dan contoh analisisnya di R.

Secara umum dalam hierarchical clustering dibagi menjadi 2 berdarkan cara membentuk bagan hirarkinya, yaitu :

1. **Agglomerative Clustering** atau **AGNES**
Agglomerative clustering menggunakan **bottom-up** manner dalam membentuk bagan hirarki (dendrogram).
2. **Divisive hierarchical clustering** atau **DIANA**
Divisive hierarchical clustering menggunakan **top-down** manner dalam membentuk bagan hirarki (dendrogram).

Pada artikel ini, akan lebih banyak dibahas mengenai beberapa metode dalam agglomerative clustering. Dalam membuat bagan hirarki, hierarchical clustering mencoba untuk menemukan (dis)similarity pada setiap observasinya. Selain itu, tujuan dalam analisis hierarchical clustering yaitu untuk menemukan kedekatan antar cluster dimana dalam mengetahui kedekatan antar cluster, terdapat metode yang digunakan yaitu **linkage method**. Berikut ini linkage method yang sering digunakan pada agglomerative approach:

1. **Complete Linkage** / **Maximum Linkage**
2. **Single Linkage** / **Minimum Linkage**
3. **Average Linkage**
4. **Centroid Linkage**
5. **Ward's minimum Variance**

![](image/linkage.png)

Happy learning ^^

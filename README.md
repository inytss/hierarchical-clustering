# Hierarchical Clustering

Secara umum dalam hierarchical clustering dibagi menjadi 2 berdarkan cara membentuk bagan hirarkinya, yaitu :

1. **Agglomerative Clustering** atau **AGNES**
Agglomerative clustering menggunakan **bottom-up** manner dalam membentuk bagan hirarki (dendrogram).
2. **Divisive hierarchical clustering** atau **DIANA**
Divisive hierarchical clustering menggunakan **top-down** manner dalam membentuk bagan hirarki (dendrogram).

Pada artikel ini, akan lebih banyak dibahas mengenai beberapa metode dalam agglomerative clustering. Dalam membuat bagan hirarki, hierarchical clustering mencoba untuk menemukan (dis)similarity pada setiap observasinya. Selain itu, dilakukan pula penentuan kedekatan antar cluster menggunakan **linkage method**. Berikut ini linkage method yang sering digunakan pada agglomerative approach:

1. **Complete Linkage** / **Maximum Linkage**
2. **Single Linkage** / **Minimum Linkage**
3. **Average Linkage**
4. **Centroid Linkage**
5. **Ward's minimum Variance**

<center> 
  
![](image/linkage.png)

</center>

Artikel konsep Hierarchical Clustering dapat diakses pada `hc-concept.md`, sedangkan artikel lengkap terkait konsep dan contoh aplikasi Hierarchical Clustering menggunakan R terdapat pada `hc-final.Rmd/.html`. 

Happy learning!

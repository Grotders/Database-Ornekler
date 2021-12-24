# Database-Ornekler
SQL, PostgreSQL, Relational Algebra

# CHAPTER 2

## VERİTABANI ŞEMASI
<pre>
Student (sid, name, did, noOfCourses, GPA)      // ogrenci(ogrenci-no, adi, bolum-no, dersSayisi)
Take (sid, cid, grade)                          // ders-al(ogrenci-no, ders-kodu, notu)
Course (cid, title, credits, did, noOfStudents) // ders(ders-kodu, adi, kredisi, bolum-no, ogrSayisi)
Department (did, name, noOfStudents)            // bolum(bolum-no, adi, ogrSayisi)
Teacher (tid, name, placeOfBirth, did)          // hoca(hoca-no, adi, dogum-yeri, bolum-no)
Teach (tid, cid)                                // ders-ver(hoca-no, ders-kodu)</pre>

### 1-) Tüm öğrencilerin ağırlıklı not ortalamalarını (GPA) bir alt sorguyla hesaplayıp güncelleyiniz.Açıklama: Şu komuttaki alt sorguyu yazmanız gerekecektir.  
UPDATE student SET GPA = (.....)  
GPA = SUM(grade x credits)/SUM(credits) formülüyle hesaplanır.

<pre>
UPDATE student SET GPA = (
								SELECT FORMAT(SUM(t.grade * c.credits) / SUM(c.credits), 2) AS GPA
								FROM take t INNER JOIN course c ON t.cid = c.cid
								WHERE t.sid = student.sid
								GROUP BY t.sid
);
</pre>

### 2-) Bölümlerin hepsinde ders veren hocaların kayıtlarını listeyeyiniz. Açıklama: Bu bir ilişkisel cebir bölme işlemidir. Bu soru şu sorgu kalıbıyla cevaplanabilir:
SELECT * FROM teacher t WHERE ((tüm dersler) – (t hocasının verdiği dersler) = φ)




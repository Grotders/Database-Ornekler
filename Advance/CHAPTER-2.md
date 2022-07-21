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


### 3-) Hocaların verdiği ders sayılarının ortalamasının altında ders veren hocaların "tid, name, verdiği ders sayısı ve derslerini alan öğrencilerin sayılarını" listeleyiniz. 
Not: Hocanın 2 dersini de alan öğrencileri 2 kere mi sayacağız belirsiz.
<pre>
WITH 
dersSayi(tid, dersSayisi, ogrenciSayisi) AS (
	SELECT t1.tid, COUNT(DISTINCT t1.cid), COUNT(t2.sid) 
	FROM teach t1, take t2
	WHERE t1.cid = t2.cid
	GROUP BY t1.tid
	),
ortalamaDers(ort) AS (
	SELECT FORMAT(AVG(d.dersSayisi), 2)
	FROM dersSayi d
	)
	
SELECT te.tid, te.name, d.dersSayisi, d.ogrenciSayisi
FROM dersSayi d, ortalamaDers o, teacher te
WHERE d.tid = te.tid AND d.dersSayisi > o.ort;
</pre>

### 4-) Kredisi > 3 olan ve en fazla 20 öğrencinin aldığı derslerin "cid, ogrenci sayısı, not ortalama"larını dersi alan öğrenci sayısına göre artan, dersteki notların ortalamasına göre azalan sırada listeleyiniz. Açıklama: Bu sorguda SELECT FROM WHERE GROUP BY HAVING ORDER BY cümleciklerinin hepsini kullanmanız gerekmektedir. 

<pre>
SELECT c.cid, COUNT(t.sid) AS ogrenci_sayısı, AVG(t.grade) AS not_ortalaması  
FROM course c, take t
WHERE c.credits > 3 AND t.cid = c.cid
GROUP BY c.cid
HAVING COUNT(t.sid) <= 20
ORDER BY ogrenci_sayısı, not_ortalaması DESC
</pre>

### 5-)

### 6-)  Bölümlerin "did, öğrenci sayılarını ve bölümdeki öğrencilerin notlarının ortalamalarını" listeleyiniz. Bu soruda öğrenci sayısı için SELECT cümleciğinde alt-sorgu kullanılacaktır. Açıklama: SELECT did, (alt sorgu) "ogrenci sayisi", (alt sorgu) ogrenciNotOrtalama FROM department d gibi yazılır.

<pre>
SELECT d.did, 
	(SELECT COUNT(*) FROM student s WHERE d.did = s.did) 'ogrenci_sayisi', 
	FORMAT((SELECT AVG(t.grade) FROM student s, take t WHERE d.did = s.did AND s.sid = t.sid), 2) ogrenciNotOrtalama
FROM department d;
</pre>

### 7-) En az iki farklı hocadan yada iki farklı bölümden ders alan öğrencilerin kayıtlarını listeleyiniz. Açıklama: "yada" dendiği için UNION kullanıp 2 alt sorgu yazılabilir.

<pre>
SELECT s.*
FROM take t1, teach t2, student s
WHERE t1.cid = t2.cid AND t1.sid = s.sid
GROUP BY t1.sid
HAVING COUNT(DISTINCT t2.tid) > 1

UNION

SELECT s.*
FROM take t1, course c, student s
WHERE t1.cid = c.cid AND t1.sid = s.sid
HAVING COUNT(DISTINCT c.did) > 1;
</pre>

### 8-) "Ali KURT" ve "Ayse KURT" adlı öğrencilerin aldığı derslerin kredilerinin toplamında daha fazla kredi alan öğrencilerin kayıtlarını listeleyiniz.
<pre>
WITH 
kredilerToplamı(sid, toplam) AS (
	SELECT t.sid, SUM(c.credits)
	FROM take t, course c
	WHERE t.cid = c.cid
	GROUP BY t.sid
),
aliVeAyseKredileri(toplam) AS (
	SELECT SUM(c.credits)
	FROM take t, course c, student s
	WHERE t.cid = c.cid AND t.sid = s.sid AND 
	(s.name = 'Ali KURT' OR s.name = 'Ayse KURT')
)

SELECT s.*
FROM kredilerToplamı k, aliVeAyseKredileri a, student s
WHERE k.toplam > a.toplam AND s.sid = k.sid
</pre>













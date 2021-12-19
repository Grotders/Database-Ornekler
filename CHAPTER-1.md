# Database-Ornekler
SQL, PostgreSQL, Relational Algebra


# CHAPTER 1
![1-0](https://user-images.githubusercontent.com/52275789/146642064-41161dcc-c75c-48d5-a40d-d0cf266df4b7.png)


### 1-) Türü ‘rock’ ve süresi 3 dakikadan uzun olan şarkıların adlarını tekrarsız olarak ve alfanümerik sırada artan sırada listeleyiniz. [Not: RA’da sıralama işlemi yoktur]

SQL:  
<pre>
SELECT DISTINCT ad  
FROM sarki  
WHERE tur LIKE '%rock%' AND sure > 180  
ORDER BY ad;  
</pre>
RA:  
![1-1](https://user-images.githubusercontent.com/52275789/146640580-e1466d8d-6ed6-4b34-b333-b90e0bdb5204.png)

Sonuç:  
![1-1Son](https://user-images.githubusercontent.com/52275789/146640639-070b7686-c4a7-42c1-9c9b-494c9b42cfe6.png)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 2-) Doğum yeri ‘London’ olan ya da albüme sahip olamayan şarkıcıların kayıtlarını listeleyiniz.	UNION kullanırken sarkicino kullanılarak UNION yapınız. Şarkıcı kayıtlarını getirmek için	UNION işleminin sonucunu sarkici tablosuyla join (kartezyen çarpım ve kayıt seçme işlemi) ediniz

SQL:  
<pre>
(SELECT *  
FROM sarkici  
WHERE dogumYer = 'London')  

UNION  

(SELECT *  
FROM sarkici  
WHERE sarkicino NOT IN (SELECT sarkicino FROM album)  
ORDER BY sarkicino);  
</pre>
RA:  
![2-1](https://user-images.githubusercontent.com/52275789/146641830-0524ef02-b700-473c-bb36-4b6784ff1b59.png)

Sonuç:  
![2-2](https://user-images.githubusercontent.com/52275789/146641833-b9c3b873-5ffe-455c-ad07-374a834de01c.png)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 3-) Şarkıcılar ve albümlerini şarkıcının adı, albümünün adı, album yılı şeklinde listeleyen sorguyu WHERE içinde sarkici.sarkicino=album.sarkicino koşuluyla, FROM içinde NATURAL JOIN cümleciğiyle, WHERE içinde IN ile, =SOME ile ve EXISTS kullanarak 5 farklı şekilde yazınız. (IN, SOME ve EXIST için sadece sanatci adı yeterli)

SQL:  
<pre>
SELECT s.ad, a.ad, a.yil  
FROM sarkici s, album a  
WHERE s.sarkicino=a.sarkicino;  </pre>

<pre>
SELECT s.ad, a.ad, a.yil  
FROM sarkici s INNER JOIN album a ON s.sarkicino=a.sarkicino;  </pre>

<pre>
SELECT s.ad  
FROM sarkici s  
WHERE s.sarkicino IN (SELECT sarkicino FROM album);  </pre>

<pre>
SELECT s.ad  
FROM sarkici s  
WHERE s.sarkicino = SOME (SELECT sarkicino FROM album);  </pre>
		
<pre>
SELECT s.ad  
FROM sarkici s  
WHERE EXISTS (SELECT sarkicino FROM album a WHERE s.sarkicino = a.sarkicino);  </pre>

RA:  
![3-1](https://user-images.githubusercontent.com/52275789/146642594-38cc3645-9f21-48c9-bd04-28697a7be797.png)

Sonuç:  
![3-3](https://user-images.githubusercontent.com/52275789/146642556-edf386b8-cbb7-43ab-8938-0bba71b7200d.png)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 4-) Hiç albümü olmayan şarkıcıların kayıtlarını küme farkı (MINUS/EXCEPT), NOT IN, != ALL ve NOT EXISTS kullanarak 4 farklı şekilde yazınız.

SQL: 
<pre>
(SELECT * FROM sarkici)  

EXCEPT  

(SELECT *  
FROM sarkici  
WHERE sarkicino IN (SELECT sarkicino FROM album));</pre>

<pre>
SELECT *  
FROM sarkici  
WHERE sarkicino NOT IN (SELECT sarkicino FROM album);</pre>

<pre>
SELECT *  
FROM sarkici  
WHERE sarkicino != ALL (SELECT sarkicino FROM album);</pre>

<pre>
SELECT *  
FROM sarkici s  
WHERE NOT EXISTS (SELECT * FROM album a WHERE a.sarkicino = s.sarkicino);</pre>

RA:  
![4-1](https://user-images.githubusercontent.com/52275789/146643155-9f28f584-25e6-41a3-84ee-2f24236ecf44.png)

Sonuç:  
![4-2](https://user-images.githubusercontent.com/52275789/146643214-1edc248e-6727-4603-a67d-e624f843100f.png)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 5-) [GROUP BY] Albümlerin numaraları, adı, şarkıcısının adı, fiyatı, içindeki şarkıların sayısı ve süre uzunlukları toplamını listeleyiniz.

SQL: 
<pre>
WITH 
toplamSarki AS (
		SELECT a.albumno, COUNT(asa.sarkino) AS toplamSarki
		FROM album a INNER JOIN albumdekisarki asa ON a.albumno = asa.albumno
		GROUP BY a.albumno
		),
toplamSure AS (
		SELECT asa.albumno, SUM(s.sure) AS toplamSure
		FROM albumdekisarki asa INNER JOIN sarki s ON s.sarkino = asa.sarkino
		GROUP BY asa.albumno 
		)
SELECT a.albumno, a.ad, sa.ad, a.fiyat,  ts.toplamSarki, t.toplamSure
FROM album a INNER JOIN sarkici sa ON a.sarkicino = sa.sarkicino, toplamSure t, toplamSarki ts
WHERE a.albumno = t.albumno AND a.albumno = ts.albumno;
</pre>

<pre>
SELECT a.albumno, a.ad, s.ad, a.fiyat, COUNT(asa.sarkino) AS toplamSarki, SUM(sa.sure) AS toplamSure
FROM album a, sarkici s, albumdekisarki asa, sarki sa
WHERE a.albumno = asa.albumno AND a.sarkicino = s.sarkicino AND sa.sarkino = asa.sarkino
GROUP BY a.albumno; </pre>


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 6-) [GROUP BY, HAVING] ‘rock’ türündeki bestecilerden 5 adetten çok şarkı besteleyenlerin besteci adı ve kaç şarkı bestelediklerini listeleyiniz. [

<pre>
SELECT b.ad, COUNT(sarkino) AS 'Toplam Sarki'  
FROM besteci b INNER JOIN sarki s ON b.bestecino = s.bestecino  
WHERE b.tur LIKE '%rock%'   
GROUP BY b.bestecino  
HAVING COUNT(sarkino) > 5;  </pre>

RA:  
![6-1](https://user-images.githubusercontent.com/52275789/146645997-27e050d4-770d-4acc-ac3b-856ad0182fe6.png)

Sonuç:  
![6-2](https://user-images.githubusercontent.com/52275789/146645999-33e3d458-480e-49b1-be76-3e63c3714df9.png)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 7-) En fazla albüme sahip şarkıcıların kayıtlarını listeleyiniz. (WITH kullanın)

<pre>
WITH 
albumSayilari AS(
		SELECT a.sarkicino, COUNT(*) AS 'album_sayisi'  
		FROM album a  
		GROUP BY a.sarkicino
		),  
enCokAlbum AS (
		SELECT MAX(album_sayisi) total 
		FROM albumSayilari
)  
SELECT s.*, asa.album_sayisi AS 'album sayisi'  
FROM sarkici s, enCokAlbum e,albumSayilari asa  
WHERE s.sarkicino = asa.sarkicino AND asa.album_sayisi = e.total;  </pre>

RA:  
![7-1](https://user-images.githubusercontent.com/52275789/146670630-24364488-971c-4bf6-b042-9aae72f7cc52.png)

Sonuç:  
![7-2](https://user-images.githubusercontent.com/52275789/146670688-4a17604a-047a-4918-82f1-f13889260264.png)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 8-) ‘grudge’ türündeki tüm şarkıların yazarlığını yapmış yazarların kayıtlarını listeleyiniz. [Not: İlişkisel cebirdeki bölme (÷) işlemi kullanılacak. İlk adımda yazarların numaraları bulunduktan sonra ikinci adımda yazar kayıtları bulunacak.]

<pre>
SELECT *  
FROM sozyazari so  
WHERE so.yazarno NOT IN (   
			(SELECT s.yazarno FROM sarki s )  
			EXCEPT  
			(SELECT s.yazarno FROM sarki s WHERE s.tur = 'grunge')  
);  </pre>
	
RA:  

Sonuç:  
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 9-) En çok şarkı sözü yazmış olan yazarların yazarno’larını bulunuz. [Her söz yazarının kaç tane şarkı sözü yazdığını GROUP BY ve COUNT kullanarak bulduktan sonra bunlar arasından en yükseğini GROUP BY ve MAX kullanmadan çözünüz]

<pre>
WITH   
X AS(  
	SELECT s.yazarno, COUNT(s.sarkino) AS toplam  
	FROM sarki s  
	GROUP BY s.yazarno  
)  
SELECT so.*, x.toplam  
FROM sozyazari so INNER JOIN x ON so.yazarno = x.yazarno  
ORDER BY x.toplam DESC LIMIT 1;  
</pre>
<pre>
WITH
x AS(
	SELECT yazarno, COUNT(sarkino) sayi
	FROM sarki s
	GROUP BY yazarno
	),
y AS (
	SELECT x1.sayi, x1.yazarno
	FROM x x1, x x2
	WHERE x1.sayi < x2.sayi
)
(SELECT yazarno FROM sozyazari)
EXCEPT
(SELECT yazarno FROM y)
</pre>

RA:  
![9-1](https://user-images.githubusercontent.com/52275789/146692435-ee5af99e-5b37-4642-8871-6684f2ac010b.png)

Sonuç:  
![9-2](https://user-images.githubusercontent.com/52275789/146692436-7b2dc9b5-4f1e-4780-8b6a-d6710779a0c2.png)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### 10-) En az iki şarkı bestelemiş olan bestecilerin bestecino’larını aynı tabloyu kendisi ile kartezyen çarpım yaparak çözünüz. 

<pre>
SELECT DISTINCT s1.bestecino, COUNT(s1.bestecino) AS Toplam  
FROM sarki s1, sarki s2  
WHERE s1.bestecino = s2.bestecino   
GROUP BY s1.sarkino  
HAVING COUNT(s1.bestecino = s2.bestecino) > 1;  </pre>

<pre>
SELECT DISTINCT s1.bestecino, COUNT(s1.bestecino) + 1 AS Toplam  
FROM sarki s1, sarki s2  
WHERE s1.sarkino != s2.sarkino and s1.bestecino=s2.bestecino  
GROUP BY s1.sarkino;  </pre>
<pre>
SELECT DISTINCT s1.bestecino
FROM sarki s1, sarki s2
WHERE s1.bestecino = s2.bestecino AND s1.sarkino != s2.sarkino;</pre>

RA: 
![10-1](https://user-images.githubusercontent.com/52275789/146692788-a1669b85-8f1f-4f42-8415-a90fa421794e.png)
 
Sonuç:  
![10-2](https://user-images.githubusercontent.com/52275789/146692797-8d3ea53d-57d3-4715-a1b8-6115a16b0b2f.png)


# Database-Ornekler
SQL, PostgreSQL, Relational Algebra


# CHAPTER 1
![1-0](https://user-images.githubusercontent.com/52275789/146642064-41161dcc-c75c-48d5-a40d-d0cf266df4b7.png)


### 1-) Türü ‘rock’ ve süresi 3 dakikadan uzun olan şarkıların adlarını tekrarsız olarak ve alfanümerik sırada artan sırada listeleyiniz. [Not: RA’da sıralama işlemi yoktur]

SQL:  
*SELECT DISTINCT ad  
FROM sarki  
WHERE tur LIKE '%rock%' AND sure > 180  
ORDER BY ad;*  

RA:  
![1-1](https://user-images.githubusercontent.com/52275789/146640580-e1466d8d-6ed6-4b34-b333-b90e0bdb5204.png)

Sonuç:  
![1-1Son](https://user-images.githubusercontent.com/52275789/146640639-070b7686-c4a7-42c1-9c9b-494c9b42cfe6.png)

### 2-) Doğum yeri ‘London’ olan ya da albüme sahip olamayan şarkıcıların kayıtlarını listeleyiniz.	UNION kullanırken sarkicino kullanılarak UNION yapınız. Şarkıcı kayıtlarını getirmek için	UNION işleminin sonucunu sarkici tablosuyla join (kartezyen çarpım ve kayıt seçme işlemi) ediniz

SQL:  
*(SELECT *  
FROM sarkici  
WHERE dogumYer = 'London')  
UNION  
(SELECT *  
FROM sarkici  
WHERE sarkicino NOT IN (SELECT sarkicino FROM album)  
ORDER BY sarkicino);*  

RA:  
![2-1](https://user-images.githubusercontent.com/52275789/146641830-0524ef02-b700-473c-bb36-4b6784ff1b59.png)

Sonuç:  
![2-2](https://user-images.githubusercontent.com/52275789/146641833-b9c3b873-5ffe-455c-ad07-374a834de01c.png)

### 3-) Şarkıcılar ve albümlerini şarkıcının adı, albümünün adı, album yılı şeklinde listeleyen sorguyu WHERE içinde sarkici.sarkicino=album.sarkicino koşuluyla, FROM içinde NATURAL JOIN cümleciğiyle, WHERE içinde IN ile, =SOME ile ve EXISTS kullanarak 5 farklı şekilde yazınız. (IN, SOME ve EXIST için sadece sanatci adı yeterli)

*SELECT s.ad, a.ad, a.yil  
FROM sarkici s, album a  
WHERE s.sarkicino=a.sarkicino;*  

*SELECT s.ad, a.ad, a.yil  
FROM sarkici s INNER JOIN album a ON s.sarkicino=a.sarkicino;*  

*SELECT s.ad  
FROM sarkici s  
WHERE s.sarkicino IN (SELECT sarkicino FROM album);*  

*SELECT s.ad  
FROM sarkici s  
WHERE s.sarkicino = SOME (SELECT sarkicino FROM album);*  
						
*SELECT s.ad  
FROM sarkici s  
WHERE EXISTS (SELECT sarkicino FROM album a WHERE s.sarkicino = a.sarkicino);*  

RA:  
![3-1](https://user-images.githubusercontent.com/52275789/146642594-38cc3645-9f21-48c9-bd04-28697a7be797.png)

Sonuç:  
![3-3](https://user-images.githubusercontent.com/52275789/146642556-edf386b8-cbb7-43ab-8938-0bba71b7200d.png)

### 4-) Hiç albümü olmayan şarkıcıların kayıtlarını küme farkı (MINUS/EXCEPT), NOT IN, != ALL ve NOT EXISTS kullanarak 4 farklı şekilde yazınız.

*(SELECT * FROM sarkici)  
EXCEPT  
(SELECT *  
FROM sarkici  
WHERE sarkicino IN (SELECT sarkicino FROM album));*

*SELECT *  
FROM sarkici  
WHERE sarkicino NOT IN (SELECT sarkicino FROM album);*

*SELECT *  
FROM sarkici  
WHERE sarkicino != ALL (SELECT sarkicino FROM album);*
								
*SELECT *  
FROM sarkici s  
WHERE NOT EXISTS (SELECT * FROM album a WHERE a.sarkicino = s.sarkicino);*

RA:  
![4-1](https://user-images.githubusercontent.com/52275789/146643155-9f28f584-25e6-41a3-84ee-2f24236ecf44.png)

Sonuç:  
![4-2](https://user-images.githubusercontent.com/52275789/146643214-1edc248e-6727-4603-a67d-e624f843100f.png)

### 5-) [GROUP BY] Albümlerin numaraları, adı, şarkıcısının adı, fiyatı, içindeki şarkıların sayısı ve süre uzunlukları toplamını listeleyiniz.





### 6-) [GROUP BY, HAVING] ‘rock’ türündeki bestecilerden 5 adetten çok şarkı besteleyenlerin besteci adı ve kaç şarkı bestelediklerini listeleyiniz. [

*SELECT b.ad, COUNT(sarkino) AS 'Toplam Sarki'  
FROM besteci b INNER JOIN sarki s ON b.bestecino = s.bestecino  
WHERE b.tur LIKE '%rock%'   
GROUP BY b.bestecino  
HAVING COUNT(sarkino) > 5;*  

RA:  
![6-1](https://user-images.githubusercontent.com/52275789/146645997-27e050d4-770d-4acc-ac3b-856ad0182fe6.png)

Sonuç:  
![6-2](https://user-images.githubusercontent.com/52275789/146645999-33e3d458-480e-49b1-be76-3e63c3714df9.png)

### 7-) En fazla albüme sahip şarkıcıların kayıtlarını listeleyiniz. (WITH kullanın)

WITH albumSayilari AS
(SELECT a.sarkicino, COUNT(*) AS 'album_sayisi'
FROM album a
GROUP BY a.sarkicino),

enCokAlbum AS (SELECT MAX(album_sayisi) total FROM albumSayilari)

SELECT s.*, asa.album_sayisi AS 'album sayisi'
FROM sarkici s, enCokAlbum e,albumSayilari asa
WHERE s.sarkicino = asa.sarkicino AND asa.album_sayisi = e.total;


### 8-) ‘grudge’ türündeki tüm şarkıların yazarlığını yapmış yazarların kayıtlarını listeleyiniz. [Not: İlişkisel cebirdeki bölme (÷) işlemi kullanılacak]

### 9-) En çok şarkı sözü yazmış olan yazarların yazarno’larını aggregate fonksiyon veya group by kullanmadan çözünüz.

### 10-) En az iki şarkı bestelemiş olan bestecilerin bestecino’larını aynı tabloyu kendisi ile kartezyen çarpım yaparak çözünüz.








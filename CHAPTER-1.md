# Database-rnekler
SQL, PostgreSQL, Relational Algebra


# CHAPTER 1

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
*SELECT *  
FROM sarkici  
WHERE dogumYer = 'London'*  

*UNION*  

*SELECT *  
FROM sarkici  
WHERE sarkicino NOT IN (  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;SELECT sarkicino  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;FROM album  
&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;&emsp;)  
ORDER BY sarkicino;*  

RA:  
![2-1](https://user-images.githubusercontent.com/52275789/146641830-0524ef02-b700-473c-bb36-4b6784ff1b59.png)

Sonuç:  
![2-2](https://user-images.githubusercontent.com/52275789/146641833-b9c3b873-5ffe-455c-ad07-374a834de01c.png)













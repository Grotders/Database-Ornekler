# ODEV 12
more [patika](https://app.patika.dev/courses/sql/Odev12)

### 1-) film tablosunda film uzunluğu length sütununda gösterilmektedir. Uzunluğu ortalama film uzunluğundan fazla kaç tane film vardır?
``` SQL
    SELECT COUNT(*) FROM film
    WHERE length >  
    (
        SELECT AVG(length) FROM film
    );
```
### 2-) film tablosunda en yüksek rental_rate değerine sahip kaç tane film vardır?
``` SQL
    SELECT COUNT(*) FROM film
    WHERE rental_rate >= ALL 
    (
        SELECT rental_rate FROM film
    );
```
### 3-) film tablosunda en düşük rental_rate ve en düşün replacement_cost değerlerine sahip filmleri sıralayınız.
``` SQL
    (
    SELECT * FROM film 
    WHERE rental_rate <= ALL 
        (SELECT rental_rate FROM film)
    )
    INTERSECT
    (
    SELECT * FROM film 
    WHERE replacement_cost <= ALL 
        (SELECT replacement_cost FROM film)
    );
``` 
### 4-) payment tablosunda en fazla sayıda alışveriş yapan müşterileri(customer) sıralayınız.
``` SQL
    SELECT * FROM customer
    WHERE customer_id = (
        SELECT customer_id FROM payment
        GROUP BY customer_id
        ORDER BY COUNT(*) DESC
        LIMIT 1
    )
```
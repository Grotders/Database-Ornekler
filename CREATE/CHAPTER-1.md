#CREATE DATABASE
<pre>
USE odev1;

DROP TABLE IF EXISTS albumdekiSarki;
DROP TABLE IF EXISTS album;
DROP TABLE IF EXISTS sarkici;
DROP TABLE IF EXISTS sarki;
DROP TABLE IF EXISTS sozyazari;
DROP TABLE IF EXISTS besteci;

CREATE TABLE sozyazari
 (yazarno INTEGER(5) NOT NULL,
 ad VARCHAR(30) NOT NULL,
 PRIMARY KEY(yazarno));
 
CREATE TABLE besteci
(bestecino INTEGER(5) NOT NULL,
ad VARCHAR(30) NOT NULL,
tur VARCHAR(15),
PRIMARY KEY(bestecino));
 
CREATE TABLE sarki
(sarkino INTEGER(5) NOT NULL,
ad VARCHAR(30) NOT NULL,
tur VARCHAR(20),
sure INTEGER(5),
bestecino INTEGER(5) NOT NULL,
yazarno INTEGER(5) NOT NULL,
FOREIGN KEY(bestecino) REFERENCES besteci(bestecino),
FOREIGN KEY(yazarno) REFERENCES sozyazari(yazarno),
PRIMARY KEY(sarkino));
 
CREATE TABLE sarkici
(sarkicino INTEGER(5) NOT NULL,
ad VARCHAR(30) NOT NULL,
tur VARCHAR(20),
dogumTarih DATE,
dogumYer VARCHAR(30),
PRIMARY KEY(sarkicino));

CREATE TABLE album
(albumno INTEGER(5) NOT NULL,
ad VARCHAR(30) NOT NULL,
yil INTEGER(5),
fiyat DECIMAL(5,2),
sarkicino INTEGER(5),
stokAdet INTEGER(10),
FOREIGN KEY(sarkicino) REFERENCES sarkici(sarkicino),
PRIMARY KEY(albumno));

CREATE TABLE albumdekiSarki
(albumno INTEGER(5) NOT NULL,
sarkino INTEGER(5) NOT NULL,
sira INTEGER(3),
FOREIGN KEY(sarkicino) REFERENCES sarkici(sarkicino),
PRIMARY KEY(albumno, sarkino)); </pre>


#INSERT
<pre>
DELETE FROM albumdekisarki;
DELETE FROM album;
DELETE FROM sarkici;
DELETE FROM sarki;
DELETE FROM besteci;
DELETE FROM sozyazari;


INSERT INTO sozyazari VALUES (1,	'Fiona Apple');
INSERT INTO sozyazari VALUES (2,	'Mete Özgencil');
INSERT INTO sozyazari VALUES (3,	'Marian Gold');
INSERT INTO sozyazari VALUES (4,	'Marvin Gaye');
INSERT INTO sozyazari VALUES (5,	'Richard Z. Kruspe');
INSERT INTO sozyazari VALUES (6,	'Gökhan Mandır');
INSERT INTO sozyazari VALUES (7,	'Helen Folasade Adu');
INSERT INTO sozyazari VALUES (8,	'Will Champion');
INSERT INTO sozyazari VALUES (9,	'Chris Cornell');
INSERT INTO sozyazari VALUES (10, 'Matthew Bellamy');


INSERT INTO besteci VALUES (1, 'Matthew Bellamy', 'opera');
INSERT INTO besteci VALUES (2, 'Gökhan Kırdar', 'pop');
INSERT INTO besteci VALUES (3, 'Wolfgang Loos', 'electronic');
INSERT INTO besteci VALUES (4, 'Marvin Gaye', 'r&b');
INSERT INTO besteci VALUES (5, 'Olsen Involtini', 'rock');
INSERT INTO besteci VALUES (6, 'Gökhan Mandır', 'rock');
INSERT INTO besteci VALUES (7, 'Robin Millar', 'pop');
INSERT INTO besteci VALUES (8, 'Ken Nelson', 'rock');
INSERT INTO besteci VALUES (9, 'Michael Beinhorn', 'rock');
INSERT INTO besteci VALUES (10, 'Muse', 'rock');


INSERT INTO sarki VALUES (1, 'Criminal', 'alternative rock', 263, 1, 1);
INSERT INTO sarki VALUES (2, 'Umrumda Degil', 'pop', 260, 2, 2);
INSERT INTO sarki VALUES (3, 'Big In Japan', 'synthpop', 238, 3, 3);
INSERT INTO sarki VALUES (4, 'Sexual Healing', 'r&b', 245, 4, 4);
INSERT INTO sarki VALUES (5, 'Deutschland', 'Neue Deutsche Härte', 562, 5, 5);
INSERT INTO sarki VALUES (6, 'Sensiz Ben', 'alternative rock', 271, 6, 6);
INSERT INTO sarki VALUES (7, 'Smooth Operator', 'sophisti pop', 257, 7, 7);
INSERT INTO sarki VALUES (8, 'The Scientist', 'alternative rock', 245, 8, 8);
INSERT INTO sarki VALUES (9, 'Black Hole Sun', 'grunge', 320, 9, 9);
INSERT INTO sarki VALUES (10, 'Uprising', 'electronic rock', 251, 10, 10);
INSERT INTO sarki VALUES (11, 'Knights Of Cydonia', 'electronic rock', 305, 10, 10);
INSERT INTO sarki VALUES (12, 'Hysteria', 'electronic rock', 226, 10, 10);
INSERT INTO sarki VALUES (13, 'Time Is Running Out', 'electronic rock', 241, 10, 10);
INSERT INTO sarki VALUES (14, 'Supermassive Black Hole', 'electronic rock', 210, 10, 10);
INSERT INTO sarki VALUES (15, 'Starlight', 'electronic rock', 245, 10, 10);
INSERT INTO sarki VALUES (15, 'What's Going On', 'soul', 231, 4, 4);


INSERT INTO sarkici VALUES (1, 'Fiona Apple', 'rock', '1977-09-13', 'new york city');
INSERT INTO sarkici VALUES (2, 'Candan Ercetin', 'pop folk', '1963-02-10', 'luleburgaz');
INSERT INTO sarkici VALUES (3, 'Alphaville', 'new wave', '1982-01-01', 'germany');
INSERT INTO sarkici VALUES (4, 'Marvin Gaye', 'r&b', '1939-05-02', 'washington');
INSERT INTO sarkici VALUES (5, 'Rammstein', 'industrial metal', '1994-01-01', 'berlin');
INSERT INTO sarkici VALUES (6, 'Pera', 'rock', '2008-01-01', 'turkey');
INSERT INTO sarkici VALUES (7, 'Sade', 'soul', '1982-01-01', 'london');
INSERT INTO sarkici VALUES (8, 'Coldplay', 'alternative rock', '1996-01-01', 'london');
INSERT INTO sarkici VALUES (9, 'Soundgarden', 'grunge', '1984-01-01', 'seattle');
INSERT INTO sarkici VALUES (10, 'Muse', 'alternative rock', '1994-01-01', 'devon');


INSERT INTO album VALUES (1, 'Tidal', 1997, 5.98, 1, 2900000);
INSERT INTO album VALUES (2, 'Hazırım', 1995, 3.85, 2, 30000);
INSERT INTO album VALUES (3, 'Forever Young', 1984, 7.47, 3, 500000);
INSERT INTO album VALUES (4, 'Midnight Love', 1982, 2.49, 4, 3900000);
INSERT INTO album VALUES (5, 'giz', 2013, 10, 6, 20000);
INSERT INTO album VALUES (6, 'Diamond Life', 1983, 16.94, 7, 10000000);
INSERT INTO album VALUES (7, 'A Rush of Blood to the Head', 2001, 8.31, 8, 15000000);
INSERT INTO album VALUES (8, 'Superunknown', 1993, 5.99, 9, 9000000);
INSERT INTO album VALUES (9, 'The Resistance', 2008, 9.99, 10, 45000000);
INSERT INTO album VALUES (10, 'What's Going On', 1971, 3.99, 4, 9900000);


INSERT INTO albumdekiSarki VALUES (1, 1, 1);
INSERT INTO albumdekiSarki VALUES (2, 2, 1);
INSERT INTO albumdekiSarki VALUES (3, 3, 1);
INSERT INTO albumdekiSarki VALUES (4, 4, 1);
INSERT INTO albumdekiSarki VALUES (5, 6, 1);
INSERT INTO albumdekiSarki VALUES (6, 7, 1);
INSERT INTO albumdekiSarki VALUES (7, 8, 1);
INSERT INTO albumdekiSarki VALUES (8, 9, 1);
INSERT INTO albumdekiSarki VALUES (9, 10, 1);
INSERT INTO albumdekiSarki VALUES (9, 11, 2);
INSERT INTO albumdekiSarki VALUES (9, 12, 3);
INSERT INTO albumdekiSarki VALUES (9, 13, 4);
INSERT INTO albumdekiSarki VALUES (9, 14, 5);
INSERT INTO albumdekiSarki VALUES (9, 15, 6);
INSERT INTO albumdekiSarki VALUES (10, 16, 1);
</pre>

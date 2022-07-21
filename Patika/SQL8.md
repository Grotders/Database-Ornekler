# ODEV 8
more [patika](https://app.patika.dev/courses/sql/Odev8)

### 1-) test veritabanınızda employee isimli sütun bilgileri id(INTEGER),        name VARCHAR(50),   birthday DATE,       email VARCHAR(100) olan bir tablo oluşturalım.
``` SQL
    CREATE TABLE employee (
        id INTEGER,     
        name VARCHAR(50),       
        birthday DATE,      
        email VARCHAR(100)
    );
```
### 2-) Oluşturduğumuz employee tablosuna 'Mockaroo' servisini kullanarak 50 adet veri ekleyelim.
``` SQL
    insert into employee (id, name, birthday, email) values (1, 'Sandra', '8/28/1995', 'spears0@businesswire.com');
insert into employee (id, name, birthday, email) values (2, 'Bekki', '10/29/1985', 'bhoofe1@tumblr.com');
insert into employee (id, name, birthday, email) values (3, 'Garnette', '3/16/1969', 'gleneham2@is.gd');
insert into employee (id, name, birthday, email) values (4, 'Fanya', '7/25/1974', 'flesser3@nps.gov');
insert into employee (id, name, birthday, email) values (5, 'Brooke', '9/18/2008', 'bswiffen4@canalblog.com');
insert into employee (id, name, birthday, email) values (6, 'Pat', '2/25/1991', 'pgrellier5@cbc.ca');
insert into employee (id, name, birthday, email) values (7, 'Julissa', '7/25/1983', 'jhully6@nytimes.com');
insert into employee (id, name, birthday, email) values (8, 'Norman', '11/5/1965', 'nlander7@europa.eu');
insert into employee (id, name, birthday, email) values (9, 'Gilberte', '10/20/1975', 'gfarnell8@yahoo.co.jp');
insert into employee (id, name, birthday, email) values (10, 'Sharl', '1/2/1978', 'sdally9@wordpress.org');
insert into employee (id, name, birthday, email) values (11, 'Imogene', '5/21/1989', 'ibiagia@dailymail.co.uk');
insert into employee (id, name, birthday, email) values (12, 'Ardeen', '2/27/1993', 'aapplewhiteb@nature.com');
insert into employee (id, name, birthday, email) values (13, 'Tristam', '3/11/1983', 'teighteenc@mlb.com');
insert into employee (id, name, birthday, email) values (14, 'Irwinn', '11/20/2011', 'imallettd@psu.edu');
insert into employee (id, name, birthday, email) values (15, 'Randall', '10/15/1968', 'rwilleye@usa.gov');
insert into employee (id, name, birthday, email) values (16, 'Gloria', '3/10/1980', 'gblaxterf@blinklist.com');
insert into employee (id, name, birthday, email) values (17, 'Dot', '9/14/1969', 'dpeasnoneg@woothemes.com');
insert into employee (id, name, birthday, email) values (18, 'Giordano', '2/26/1988', 'ghauggh@dion.ne.jp');
insert into employee (id, name, birthday, email) values (19, 'Germain', '1/21/2001', 'gswatei@loc.gov');
insert into employee (id, name, birthday, email) values (20, 'Shaine', '11/1/1983', 'soganj@hc360.com');
insert into employee (id, name, birthday, email) values (21, 'Gabey', '2/12/1987', 'gmiddlek@blogger.com');
insert into employee (id, name, birthday, email) values (22, 'Daria', '1/14/1977', 'dsumersl@chronoengine.com');
insert into employee (id, name, birthday, email) values (23, 'Nola', '5/28/2008', 'ncoffinm@ca.gov');
insert into employee (id, name, birthday, email) values (24, 'Anestassia', '4/11/2003', 'ahousen@alexa.com');
insert into employee (id, name, birthday, email) values (25, 'Tadd', '4/21/1990', 'tivattso@adobe.com');
insert into employee (id, name, birthday, email) values (26, 'Doug', '2/1/1997', 'dsharplessp@gizmodo.com');
insert into employee (id, name, birthday, email) values (27, 'Osmund', '1/11/1985', 'oclymerq@hatena.ne.jp');
insert into employee (id, name, birthday, email) values (28, 'Ellary', '5/25/1984', 'epeeterr@chicagotribune.com');
insert into employee (id, name, birthday, email) values (29, 'Belinda', '10/6/1993', 'bmoorhouses@smh.com.au');
insert into employee (id, name, birthday, email) values (30, 'Ethe', '1/9/1986', 'evatert@woothemes.com');
insert into employee (id, name, birthday, email) values (31, 'Cassie', '2/15/1995', 'ctweedyu@desdev.cn');
insert into employee (id, name, birthday, email) values (32, 'Margareta', '5/28/1960', 'mterzov@gizmodo.com');
insert into employee (id, name, birthday, email) values (33, 'Corby', '5/9/1981', 'chovingtonw@netvibes.com');
insert into employee (id, name, birthday, email) values (34, 'Aurora', '4/5/1987', 'amcfaellx@woothemes.com');
insert into employee (id, name, birthday, email) values (35, 'Sheffy', '3/24/1986', 'sgirodiasy@home.pl');
insert into employee (id, name, birthday, email) values (36, 'Jared', '10/31/2011', 'jdobrovolskiz@bravesites.com');
insert into employee (id, name, birthday, email) values (37, 'Reinold', '4/23/1985', 'rrowledge10@vimeo.com');
insert into employee (id, name, birthday, email) values (38, 'Ian', '11/12/1964', 'ilindblom11@newyorker.com');
insert into employee (id, name, birthday, email) values (39, 'Annissa', '1/1/2011', 'avowden12@paginegialle.it');
insert into employee (id, name, birthday, email) values (40, 'Darby', '10/28/2010', 'dpastor13@google.ru');
insert into employee (id, name, birthday, email) values (41, 'Bern', '8/30/1983', 'bmustin14@free.fr');
insert into employee (id, name, birthday, email) values (42, 'Dennet', '8/19/2011', 'dmarnane15@nps.gov');
insert into employee (id, name, birthday, email) values (43, 'Piotr', '4/30/1977', 'pdeclerq16@reuters.com');
insert into employee (id, name, birthday, email) values (44, 'Augusto', '8/15/1978', 'asetford17@360.cn');
insert into employee (id, name, birthday, email) values (45, 'Dore', '11/7/1997', 'dsavidge18@shop-pro.jp');
insert into employee (id, name, birthday, email) values (46, 'Simonne', '12/17/1975', 'sdossit19@ameblo.jp');
insert into employee (id, name, birthday, email) values (47, 'Lanie', '12/13/1972', 'ltaffley1a@ifeng.com');
insert into employee (id, name, birthday, email) values (48, 'Shirleen', '10/21/1960', 'slindwasser1b@bravesites.com');
insert into employee (id, name, birthday, email) values (49, 'Gianina', '6/10/1994', 'gdannel1c@youtu.be');
insert into employee (id, name, birthday, email) values (50, 'Kore', '6/13/1990', 'kdemangel1d@edublogs.org');
```
### 3-) Sütunların her birine göre diğer sütunları güncelleyecek 5 adet UPDATE işlemi yapalım.
``` SQL
    UPDATE employee SET id = 99 WHERE  name = 'Brooke';
    UPDATE employee SET name = 'Mehmet' WHERE id = 13;
    UPDATE employee SET birthday = '09/01/2000' WHERE email = 'kdemangel1d@edublogs.org';
    UPDATE employee SET email = 'Mehmet@gmail.com' WHERE birthday = '12/13/1972';
    UPDATE employee SET name = 'Ayse' WHERE id = 32;
```
### 4-) Sütunların her birine göre ilgili satırı silecek 5 adet DELETE işlemi yapalım.
``` SQL
    DELETE FROM employee WHERE id=21;
    DELETE FROM employee WHERE name='Dennet';
    DELETE FROM employee WHERE birthday='4/30/1977';
    DELETE FROM employee WHERE email='asetford17@360.cn';
    DELETE FROM employee WHERE id=11;
```
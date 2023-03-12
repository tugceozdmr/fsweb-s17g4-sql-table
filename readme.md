# SQL Sorgu Alıştırmaları

Bu hafta SQL sorguları üzerine çalışıyorsunuz. Bugünkü alıştırmada sıfırdan bir veritabanı oluşturacak ve aşağıda istenenleri SQL sorgu olarak oluşturacaksınız.

# Proje Kurulumu
Projeyi forklayın ve clonlayın. Tamamladığınızda da pushlayın.

## Görev 1: Kütüphane Bilgi Sistemi için Tablo Tasarımı

Bu veritabanı, bir okulun kütüphanesinden öğrencilerin aldıkları kitapların bilgisini barındıracak. 
Aşağıda tablolar ve şemaları verilmiş. 

[ ] Bu tabloların tasarımını online olarak veya bilgisayarınızda bir yazılım kullanarak dizayn ediniz. (örn: [drawsql.app](https://drawsql.app/)
[ ] Resim olarak proje dosyasına ekleyiniz.

-- Tablolar 

`ogrenci` tablosu öğrencilerin listesini tutar.

| field        | data type        | metadata                                           |
| :----------- | :--------------- | :------------------------------------------------- |
| id          | unsigned integer | primary key, auto-increments, generated by db      |
| ad 		      | string           | required                                           |
| soyad 	      | string           | required                                           |
| dtarih 	   | string           | required                                           |
| cinsiyet     | string           | required                                           |
| sinif        | string           | required                                           |
| puan         | unsigned integer | required                                           |


`islem` tablosu öğrencilerin kütüphaneden aldıkları kitapların bilgilerini tutar

| field        | data type        | metadata                                           |
| :----------- | :--------------- | :------------------------------------------------- |
| id      	   | unsigned integer | primary key, auto-increments, generated by db      |
| ogrenci_id   | unsigned integer | foreign key referencing ogrenci.id, required       |
| kitap_id     | unsigned integer | foreign key referencing kitap.id, required	       |
| atarih 	   | string           | required                                           |
| vtarih 	   | string           | required                                           |


`kitap` tablosu kütüphanedeki kitapların bilgisini tutar

| field        | data type        | metadata                                           |
| :----------- | :--------------- | :------------------------------------------------- |
| id      	   | unsigned integer | primary key, auto-increments, generated by db      |
| ad 		      | string           | required                                           |
| sayfasayisi  | unsigned integer | required                                           |
| puan         | unsigned integer | required                                           |
| yazar_id     | unsigned integer | foreign key referencing yazar.id, required 		   |
| tur_id       | unsigned integer | foreign key referencing tur.id, required 		   |


`yazar` tablosu kitapların yazarları bilgisini tutar

| field        | data type        | metadata                                           |
| :----------- | :--------------- | :------------------------------------------------- |
| id      	   | unsigned integer | primary key, auto-increments, generated by db      |
| ad 		      | string           | required                                           |
| soyad 	      | string           | required                                           |


`tur` tablosu kitapların türlerini tutar.

| field        | data type        | metadata                                           |
| :----------- | :--------------- | :------------------------------------------------- |
| id      	   | unsigned integer | primary key, auto-increments, generated by db      |
| ad 		      | string           | required                                           |




### Görev 2: SQL İfadeleri

[ ] Görev 1'de tasarımını yaptığınız tabloları DB'de oluşturan komutları kutuphane_bilgi_sistemi.sql dosyasında oluşturunuz.


#### Görev 3: 

[ ] veriler.sql içindeki hataları düzelterek, verileri veritabanınıza ekleyiniz.


##### Görev 4: 

[ ] Aşağıda istenen değişiklikleri tablolarda yapacak SQL ifadeleri yazınız.

   1- öğrenci tablosuna 'sehir' alanı ekleyiniz.

   ALTER TABLE [ogrenci] ADD sehir VARCHAR(50) ;

   2- tablolarda veri olarak tarih geçen alanlarda veri tipini string yerine DateTime olarak ayarlayınız.

   ALTER TABLE `ogrenci` CHANGE COLUMN `dtarih` `dtarih` DateTime NULL DEFAULT NULL ;


   3- öğrenci tablosuna 'dogum_yeri' alanı ekleyiniz ve default değerini 'Türkiye' yapınız.

    ALTER TABLE [ogrenci] ADD COLUMN dogum_yeri DEFAULT 'Türkiye' ;


   4- öğrenci tablosundan 'puan' alanını siliniz.


   ALTER TABLE ogrenci DROP puan;
 

   5- öğrenciler tablosundaki kiz öğrencileri alarak kiz_ogrenciler tablosu oluşturunuz.
   

   CREATE TABLE kız_ogrenciLer AS( SELECT * FROM ogrenci WHERE cinsiyet='K');

   
   6- kiz_ogrenciler tablosunu siliniz.

    
    DELETE FROM kız_ogrenciler


   7- kiz_yurdu tablosu oluşturunuz(sadece 'ad' alanı olsun). 1 kayıt ekleyiniz.
      öğrenci tablosundaki kız öğrencileri kullanarak kiz_yurdunda_kalanlar tablosu oluşturunuz


    CREATE TABLE kiz_yurdu_ogrenciler AS(
    SELECT "1" AS yurtId, ogrno AS ogrenciID FROM ogrenci WHERE cinsiyet='K');


   8- kiz_ogrenciler tablosunun adını kogrenciler olarak değiştiriniz
   
    SELECT * FROM ogrenci
    inner join kiz_yurdu_ogrenciler on ogrenci.ID = kiz_yurdu_ogrenciler.ogrenciID
    inner join kiz_yurdu on kiz_yurdu.ID = kiz_yurdu_ogrenciler.yurtID;

   /9- yazar tablosundaki 'ad' alanının adını 'name' olarak güncelleyiniz.


   /10- yazar tablosuna 'ulke' ve 'universite' alanları ekleyiniz 'ulke'nin default değeri 'Türkiye' olsun.


   /11- tablo ilişkilerine 5'er tane örnek veriniz (1-1, 1-n, n-n)  




# Tugas Praktikum 7

|**Nama**|**NIM**|**Kelas**|**Matkul**|
|----|---|-----|------|
|Muhammad Arif Mulyanto|312310395|TI.23.A5|Basis Data|

# Soal Latihan Praktikum

## Data Model Mapping

```
Mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)
Dosen (kd_ds, nama)
Matakuliah (kd_mk, nama, sks)
JadwalMengajar (kd_ds, kd_mk, hari, jam, ruang)
KRSMahasiswa (nim, kd_mk, kd_ds, semester, nilai)
```
- Buat DDL Script berdasarkan skema ERD tersebut diatas. 
- Jalankan script DDL tersebut pada DBMS MySQL.

**Langkah-langkahnya :**

**1. Buat dulu script untuk table Mahasiswa :**

```
create table Mahasiswa (
    nim varchar(10) PRIMARY KEY,
    nama varchar(25) NOT NULL,
    jenis_kelamin ENUM('Laki-Laki', 'Perempuan'),
    tgl_lahir DATE,
    jalan varchar(15) NOT NULL,
    kota varchar(15) NOT NULL,
    kodepos varchar(5) NOT NULL,
    no_hp varchar(15) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );
```

![oke1](https://github.com/MuhArifyanto/MySQL2/assets/147913440/050cdd40-93b7-45fa-8ead-53d6d44195a2)


**Tampilkan hasil table :**

`desc Mahasiswa;`

![oke2](https://github.com/MuhArifyanto/MySQL2/assets/147913440/67dc1154-8e3b-4a86-901d-9d3deff7bf78)


**2. Buat script untuk table Dosen :**
```
create table Dosen (
    kd_ds varchar(10) PRIMARY KEY,
    nama varchar(35) NOT NULL
    );
```

![oke3](https://github.com/MuhArifyanto/MySQL2/assets/147913440/7db9c7ce-1979-44ea-8951-632e18747997)


**Tampilkan tabel :**

`desc Dosen;`

![oke4](https://github.com/MuhArifyanto/MySQL2/assets/147913440/7c9dc715-7199-4f9e-9847-8cdde31683ed)


**3. Buat script untuk Mata kuliah :**
```
create table Matakuliah (
    kd_mk varchar(10) PRIMARY KEY,
    nama varchar(30) NOT NULL,
    sks INT NOT NULL
    );
```

![oke5](https://github.com/MuhArifyanto/MySQL2/assets/147913440/098b92ec-2c92-4d51-8773-2197b8e695a4)



**Tampilkan table :**

`desc Matakuliah;`

![oke6](https://github.com/MuhArifyanto/MySQL2/assets/147913440/6698c7d6-f99a-49c6-9e2f-42fb601f99a5)


**4. Buat script untuk jadwal mengajar :**
```
create table JadwalMengajar (
    kd_ds varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    hari ENUM('Senin', 'Selasa', 'Rabu', 'Kamis', 'Jumat', 'Sabtu', 'Minggu') NOT NULL,
    jam TIME NOT NULL,
    ruang varchar(555) NOT NULL,
    PRIMARY KEY (kd_ds, kd_mk, hari, jam),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk)
    ); 
```

![oke7](https://github.com/MuhArifyanto/MySQL2/assets/147913440/b7e7239b-9241-4f58-b3d8-a2e71aa43683)


**Tampilkan table :**

`desc JadwalMengajar;`

![oke8](https://github.com/MuhArifyanto/MySQL2/assets/147913440/9e0ec140-5575-47d3-8953-2b7c54172a3f)


**5. Buat script untuk KRSMahasiswa :**
```
CREATE TABLE KRSMahasiswa (
    nim varchar(10) NOT NULL,
    kd_mk varchar(10) NOT NULL,
    kd_ds varchar(10) NOT NULL,
    semester varchar(10) NOT NULL,
    nilai FLOAT NOT NULL,
    PRIMARY KEY (nim, kd_mk),
    FOREIGN KEY (nim) REFERENCES Mahasiswa(nim),
    FOREIGN KEY (kd_mk) REFERENCES Matakuliah(kd_mk),
    FOREIGN KEY (kd_ds) REFERENCES Dosen(kd_ds)
    );
```

![oke9](https://github.com/MuhArifyanto/MySQL2/assets/147913440/4243d3eb-d05a-4e1b-a6aa-b6c8a579bd77)


**Tampilkan table :**

`desc KRSMahasiswa;`

![oke10](https://github.com/MuhArifyanto/MySQL2/assets/147913440/cb3e59ec-0012-4bd2-a23a-9e3a314e6a7f)


# Soal Latihan Praktikum

Berdasarkan table Mahasiswa pada praktikum sebelumnya: (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds)

***Isi data pada table tersebut sebanyak minimal 5 record data. Tampilkan semua isi/record tabel!***

- Ubah data tanggal lahir mahasiswa yang bernama Ari menjadi: 1979-08-31!

- Tampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja!

- Hapus Mahasiswa yang bernama Dina!

- Tampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2!

- Tampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan!

- Tampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita!

- Tampilkan data nama dan alamat mahasiswa saja dari tabel tersebut

- Tampilkan data mahasiswa terurut berdasarkan nama.

**1. Mengisi tabel dengan minimal 5 record data :**
```
insert into mahasiswa (nim, nama, jenis_kelamin, tgl_lahir, jalan, kota, kodepos, no_hp, kd_ds) values 
-> (11223344,"ari santoso","Laki-laki","1998-10-12","","Bekasi","","",""), 
-> (11223345,"ario talib","Laki-laki","1999-11-16","","Cikarang","","",""), 
-> (11223346,"dina marlina","Perempuan","1997-12-01","","Karawang","","",""), 
-> (11223347,"lisa ayu","perempuan","1996-01-02","","Bekasi","","",""), 
-> (11223348,"tiara wahidah","perempuan","1980-02-05","","Bekasi","","",""), 
-> (11223349,"anton sinaga","laki-laki","1988-03-10","","Cikarang","","","");
```

![oke11](https://github.com/MuhArifyanto/MySQL2/assets/147913440/1feab3b0-cebf-4b71-bcde-d8004bfc7812)



**2. Menampilkan semua isi/record pada tabel bisa menggunakan kode berikut :**

`select*from mahasiswa;`

![oke12](https://github.com/MuhArifyanto/MySQL2/assets/147913440/36d6e67d-6510-4526-b165-72f37bfc1758)

**3. Mengubah data tanggal lahir mahasiswa yang bernama Ari menjadi : 1979-08-31 menggunakan kode berikut :**

`update mahasiswa set tgl_lahir='1979-08-31' where nim=11223344;`

![oke13](https://github.com/MuhArifyanto/MySQL2/assets/147913440/3d111223-42b7-4623-877f-4001f8856af8)


**4. Menampilkan satu baris / record data yang telah diubah tadi yaitu record dengan nama Ari saja dengan cara sebagai berikut :**

`select*from mahasiswa where nim=11223344;`

![oke14](https://github.com/MuhArifyanto/MySQL2/assets/147913440/26d81f8a-98d0-47a9-9332-3e4cb35d01af)


**5. Menghapus Mahasiswa yang bernama Dina dengan cara sebagai berikut:**

`delete from mahasiswa where nim=11223346;`

![oke15](https://github.com/MuhArifyanto/MySQL2/assets/147913440/431db044-d414-4e10-b1cd-3d96ce92d7aa)


**6. Menampilkan record atau data yang tanggal kelahirannya lebih dari atau sama dengan 1996-1-2 dengan cara sebagai berikut :**

`select*from mahasiswa where tgl_lahir<='1996-1-2';`

![oke16](https://github.com/MuhArifyanto/MySQL2/assets/147913440/997e5ed5-8fed-49b2-9127-4166bdb64208)

**7. Menampilkan semua Mahasiswa yang berasal dari Bekasi dan berjenis kelamin perempuan dengan cara sebagai berikut :**

`select*from Mahasiswa where kota='bekasi' and jenis_kelamin='Perempuan';`

![oke17](https://github.com/MuhArifyanto/MySQL2/assets/147913440/68bc106e-cccf-424e-af8a-34aa40c1ce97)


**8. Menampilkan semua Mahasiswa yang berasal dari Bekasi dengan kelamin laki-laki atau Mahasiswa yang berumur lebih dari 22 tahun dengan kelamin wanita dengan cara sebagai berikut :**
```
select * from mahasiswa where kota='Bekasi' and jenis_kelamin='Laki-laki' 
or tgl_lahir<='2002-4-22' 
and jenis_kelamin='Perempuan';
```

![oke18](https://github.com/MuhArifyanto/MySQL2/assets/147913440/cc6511ff-7690-4824-ac34-74df5620c3c7)


**9. Menampilkan data nama dan jalan mahasiswa saja dari tabel tersebut dengan cara sebagai berikut :**

`select nama, jalan from mahasiswa;`

![oke19](https://github.com/MuhArifyanto/MySQL2/assets/147913440/03f1ba7c-2383-4856-b493-deea748d34f4)


**10. Menampilkan data mahasiswa terurut berdasarkan nama dengan cara sebagai berikut :**

`select*from mahasiswa -> order by nama asc;`

![oke20](https://github.com/MuhArifyanto/MySQL2/assets/147913440/22c21f2a-a005-4057-9aee-c343bc3b9df5)


# Evaluasi dan Pertanyaan 
***Tulis semua perintah-perintah SQL percobaan di atas beserta outputnyan!***

***Menambah Data***

`INSERT INTO <table> (field1, ..., fieldn) VALUE (value1, ..., valuen)`

*Contoh :*

`INSERT INTO biodata (nim, nama, alamat) VALUE ('1234','Agus','Cikarang');`

***Tulis semua perintah-perintah SQL percobaan di atas beserta outputnya!***

**1. Menambah data :**

`INSERT INTO <table> (field1, ..., fieldn) VALUE (value1, ..., valuen)`

*Contoh :*

`INSERT INTO biodata (nim, nama, alamat) VALUE ('1234','Agus','Cikarang');`

![agus1](https://github.com/MuhArifyanto/MySQL2/assets/147913440/e878fad2-f75f-46b8-9834-43be86e9f631)


**2. Menampilkan data :**

`SELECT * FROM <table> SELECT [field1, ..., fieldn] FROM <table>`

*Contoh :*

`SELECT*FROM biodata;`

![agus2](https://github.com/MuhArifyanto/MySQL2/assets/147913440/7f26a329-de05-4b12-bcfc-2fb1d3289813)

**3. Mengubah data :**

`UPDATE <table> SET field1=val1, ..., fieldn=valn WHERE <kondisi>;`

*Contoh :*

`UPDATE biodata SET nama='Arif', alamat='Klaten' WHERE nim='1234';`

![agus6](https://github.com/MuhArifyanto/MySQL2/assets/147913440/e204887f-e6f6-4d0e-9026-ef95c9630ecb)


**4. Menghapus data :**

`DELETE FROM <table> WHERE <kondisi>`

*Contoh :*

`DELETE FROM biodata WHERE nim=‘12334’`

![agus5](https://github.com/MuhArifyanto/MySQL2/assets/147913440/37d04cb6-995a-4b42-a5f3-1e4b533451aa)

***Apa bedanya penggunaan BETWEEN dan penggunaan operator >= dan <= ?***

- (misal: tgl_lahir BETWEEN '1990-10-10' AND '1992-10-11')

- (misal: tgl_lahir >= '1990-10-10' AND tgl_lahir <= '1992-10-11')

**Jawaban nya :**

* Penggunaan BETWEEN dalam SQL digunakan untuk menentukan apakah nilai tertentu berada dalam rentang nilai yang ditentukan. Misalnya, tgl_lahir BETWEEN '1990-10-10' AND '1992-10-11' akan menghasilkan true jika tgl_lahir berada di antara tanggal '1990-10-10' dan '1992-10-11', termasuk kedua tanggal tersebut. Sedangkan 
* Penggunaan operator >= (greater than or equal to) dan <= (less than or equal to) dalam SQL digunakan untuk memeriksa apakah nilai tertentu lebih besar dari atau sama dengan (untuk >=) atau kurang dari atau sama dengan (untuk <=) nilai yang diberikan. Misalnya, tgl_lahir >= '1990-10-10' AND tgl_lahir <= '1992-10-11' akan menghasilkan true jika tgl_lahir lebih besar dari atau sama dengan '1990-10-10' dan kurang dari atau sama dengan '1992-10-11'.

***Berikan kesimpulan anda!***
* DML (Data Manipulation Language) adalah bahasa pemrograman yang digunakan untuk mengatur dan memanipulasi data pada database. DML adalah bagian dari SQL (Structured Query Language) yang digunakan untuk memasukkan, memperbarui, menghapus, atau menerima data dari database. DML memberikan beberapa keuntungan, seperti fleksibilitas dalam memanipulasi data, menjaga integritas data, dan meningkatkan efisiensi. DML terdiri dari beberapa perintah, seperti INSERT, UPDATE, DELETE, dan SELECT, dan digunakan untuk melakukan operasi CRUD pada data di dalam database.

***Buat laporan praktikum yang berisi, langkah-langkah praktikum beserta screenshot yang sudah dilakukan dalam bentuk dokumen.***

https://drive.google.com/file/d/16xlWux0ceo04mYxfeZMhE_fe65EuUtrf/view?usp=drivesdk

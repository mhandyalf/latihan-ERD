use data_karyawan;

-- Tabel Departemen
CREATE TABLE Departemen (
  Departemen_ID INT PRIMARY KEY,
  Nama_Departemen VARCHAR(100),
  Manager_ID INT
);

-- Tabel Karyawan
CREATE TABLE Karyawan (
  NIK INT PRIMARY KEY,
  Nama_Depan VARCHAR(50),
  Nama_Belakang VARCHAR(50),
  Jenis_Kelamin VARCHAR(10),
  Email VARCHAR(100),
  Phone_Number VARCHAR(15),
  Departemen_ID INT,
  FOREIGN KEY (Departemen_ID) REFERENCES Departemen(Departemen_ID)
);

-- Tabel Projek
CREATE TABLE Project (
  Project_ID INT PRIMARY KEY,
  Nama_Project VARCHAR(100)
);

-- Tabel Project_Karyawan
CREATE TABLE Project_Karyawan (
  Karyawan_NIK INT,
  Project_ID INT,
  FOREIGN KEY (Karyawan_NIK) REFERENCES Karyawan(NIK),
  FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID),
  PRIMARY KEY (Karyawan_NIK, Project_ID)
);

-- Memasukkan data ke tabel Departemen
INSERT INTO Departemen (Departemen_ID, Nama_Departemen, Manager_ID) VALUES
(1, 'Departemen Sales', 123),
(2, 'Departemen Production', 456),
(3, 'Departemen Maintance', 789);

-- Memasukkan data ke tabel Karyawan
INSERT INTO Karyawan (NIK, Nama_Depan, Nama_Belakang, Jenis_Kelamin, Email, Phone_Number, Departemen_ID) VALUES
(1001, 'Handy', 'Sieghart', 'Laki-Laki', 'handysieghart@example.com', '123456789', 1),
(1002, 'Jane', 'Foster', 'Perempuan', 'jane.fofterh@example.com', '987654321', 2),
(1003, 'David', 'Googins', 'Laki-Laki', 'david.googins@example.com', '555555555', 3);

-- Memasukkan data ke tabel Project
INSERT INTO Project (Project_ID, Nama_Project) VALUES
(1, 'Project Tresholding'),
(2, 'Project Chinatown'),
(3, 'Project Ghost');

-- Memasukkan data ke tabel Project_Karyawan
INSERT INTO Project_Karyawan (Karyawan_NIK, Project_ID) VALUES
(1001, 1),
(1002, 1),
(1002, 2),
(1003, 2),
(1003, 3);

-- Query select semua karyawan
SELECT * FROM Karyawan;

-- Query select semua departemen beserta dengan jumlah karyawan yg berada di departemen tersebut.
SELECT Departemen.Departemen_ID, Departemen.Nama_Departemen, COUNT(Karyawan.NIK) AS Jumlah_Karyawan
FROM Departemen
LEFT JOIN Karyawan ON Departemen.Departemen_ID = Karyawan.Departemen_ID
GROUP BY Departemen.Departemen_ID, Departemen.Nama_Departemen;

-- Query nama karyawan yg mengerjakan proyek tertentu berdasarkan proyek id
SELECT Karyawan.Nama_Depan, Karyawan.Nama_Belakang
FROM Karyawan
JOIN Project_Karyawan ON Karyawan.NIK = Project_Karyawan.Karyawan_NIK
WHERE Project_Karyawan.Project_ID = 3;


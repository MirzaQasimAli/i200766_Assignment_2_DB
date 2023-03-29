# i200766_Assignment_2_DB

create database AirportDatabase

CREATE TABLE Airplane (
    RegNum VARCHAR(20) PRIMARY KEY,
    OfType VARCHAR(20) NOT NULL,
    StoredIn VARCHAR(20) NOT NULL,
    FOREIGN KEY (OfType) REFERENCES PlaneType(Model),
    FOREIGN KEY (StoredIn) REFERENCES Hangar(Number)
);

CREATE TABLE PlaneType (
    Model VARCHAR(20) PRIMARY KEY,
    Capacity INT NOT NULL,
    Weight INT NOT NULL
);

CREATE TABLE Hangar (
    Number VARCHAR(20) PRIMARY KEY,
    Capacity INT NOT NULL,
    Location VARCHAR(50) NOT NULL
);

CREATE TABLE Owner (
    Ssn VARCHAR(20) PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Address VARCHAR(100) NOT NULL,
    Phone VARCHAR(20) NOT NULL,
    Category VARCHAR(20) NOT NULL
);

CREATE TABLE Employee (
    Ssn VARCHAR(20) PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Address VARCHAR(100) NOT NULL,
    Phone VARCHAR(20) NOT NULL,
    Salary DECIMAL(10, 2) NOT NULL,
    Shift VARCHAR(20) NOT NULL
);

CREATE TABLE Pilot (
    LicNum VARCHAR(20) PRIMARY KEY,
    Ssn VARCHAR(20) NOT NULL,
    Restrictions VARCHAR(50) NOT NULL,
    FOREIGN KEY (Ssn) REFERENCES Employee(Ssn)
);

CREATE TABLE Service (
    Id INT PRIMARY KEY,
    Date DATE NOT NULL,
    Hours INT NOT NULL,
    WorkCode VARCHAR(20) NOT NULL
);

CREATE TABLE Owns (
    AirplaneRegNum VARCHAR(20) NOT NULL,
    OwnerSsn VARCHAR(20) NOT NULL,
    Pdate DATE NOT NULL,
    PRIMARY KEY (AirplaneRegNum, OwnerSsn),
    FOREIGN KEY (AirplaneRegNum) REFERENCES Airplane(RegNum),
    FOREIGN KEY (OwnerSsn) REFERENCES Owner(Ssn)
);

CREATE TABLE Maintain (
    EmployeeSsn VARCHAR(20) NOT NULL,
    ServiceId INT NOT NULL,
    PRIMARY KEY (EmployeeSsn, ServiceId),
    FOREIGN KEY (EmployeeSsn) REFERENCES Employee(Ssn),
    FOREIGN KEY (ServiceId) REFERENCES Service(Id)
);

CREATE TABLE Plane_Service (
    AirplaneRegNum VARCHAR(20) NOT NULL,
    ServiceId INT NOT NULL,
    PRIMARY KEY (AirplaneRegNum, ServiceId),
    FOREIGN KEY (AirplaneRegNum) REFERENCES Airplane(RegNum),
    FOREIGN KEY (ServiceId) REFERENCES Service(Id)
);

CREATE TABLE Flies (
    PilotLicNum VARCHAR(20) NOT NULL,
    Model VARCHAR(20) NOT NULL,
    PRIMARY KEY (PilotLicNum, Model),
    FOREIGN KEY (PilotLicNum) REFERENCES Pilot(LicNum),
    FOREIGN KEY (Model) REFERENCES PlaneType(Model)
);

CREATE TABLE Works_On (
    EmployeeSsn VARCHAR(20) NOT NULL,
    Model VARCHAR(20) NOT NULL,
    PRIMARY KEY (EmployeeSsn, Model),
    FOREIGN KEY (EmployeeSsn) REFERENCES Employee(Ssn),
    FOREIGN KEY (Model) REFERENCES PlaneType(Model)
);



INSERT INTO Airplane (RegNum, OfType, StoredIn) VALUES
('N101AB', 'Boeing 747', 'H1'),
('N202BC', 'Cessna 172', 'H2'),
('N303CD', 'Piper PA-28', 'H3'),
('N404DE', 'Cessna 182', 'H4'),
('N505EF', 'Beechcraft Bonanza', 'H5'),
('N606FG', 'Mooney M20', 'H6'),
('N707GH', 'Cirrus SR22', 'H7'),
('N808HI', 'Diamond DA40', 'H8'),
('N909IJ', 'Piper PA-34', 'H9'),
('N1010JK', 'Cessna 210', 'H10'),
('N1111KL', 'Piper PA-32', 'H11'),
('N1212LM', 'Beechcraft King Air', 'H12'),
('N1313MN', 'Cessna 150', 'H13'),
('N1414NO', 'Piper PA-38', 'H14'),
('N1515OP', 'Cessna 172', 'H15'),
('N1616PQ', 'Cessna 182', 'H16'),
('N1717QR', 'Piper PA-28', 'H17'),
('N1818RS', 'Mooney M20', 'H18'),
('N1919ST', 'Cirrus SR22', 'H19'),
('N2020TU', 'Diamond DA40', 'H20');




INSERT INTO PlaneType (Model, Capacity, Weight) VALUES
('Boeing 747', 100, 987000),
('Cessna 172', 400, 2300),
('Piper PA-28', 40, 1500),
('Cessna 182', 4, 3100),
('Beechcraft Bonanza', 6, 3400),
('Mooney M20', 4, 2500),
('Cirrus SR22', 4, 3000),
('Diamond DA40', 4, 2700),
('Piper PA-34', 600, 4000),
('Cessna 210', 6, 3100),
('Piper PA-32', 6, 2800),
('Beechcraft King Air', 8, 12000),
('Cessna 150', 2, 1500),
('Piper PA-38', 2, 900),
('Piper PA-24', 6, 2800),
('Cessna 152', 200, 1300),
('Cessna 206', 6, 3350),
('Cessna 208', 90, 8750),
('Piper PA-44', 4, 3800),
('Beechcraft Baron', 6, 3600);


INSERT INTO Hangar (Number, Capacity, Location)
VALUES 
  ('H1', 10, 'North'),
  ('H2', 15, 'South'),
  ('H3', 12, 'East'),
  ('H4', 8, 'West'),
  ('H5', 20, 'Central'),
  ('H6', 6, 'North'),
  ('H7', 14, 'South'),
  ('H8', 18, 'East'),
  ('H9', 7, 'West'),
  ('H10', 22, 'Central'),
  ('H11', 9, 'North'),
  ('H12', 16, 'South'),
  ('H13', 11, 'East'),
  ('H14', 13, 'West'),
  ('H15', 25, 'Central'),
  ('H16', 5, 'North'),
  ('H17', 17, 'South'),
  ('H18', 21, 'East'),
  ('H19', 10, 'West'),
  ('H20', 30, 'Central');

    

  INSERT INTO Owner (Ssn, Name, Address, Phone, Category)
VALUES 
  ('111-11-1111', 'Ali', '123 Main St', '555-555-1111', 'Individual'),
  ('222-22-2222', 'Ahmad', '456 Elm St', '555-555-2222', 'Individual'),
  ('333-33-3333', 'Asad', '789 Oak St', '555-555-3333', 'Corporation'),
  ('444-44-4444', 'Shaheer', '321 Maple St', '555-555-4444', 'Individual'),
  ('555-55-5555', 'Qasim', '654 Pine St', '555-555-5555', 'Individual'),
  ('666-66-6666', 'Usman', '987 Cedar St', '555-555-6666', 'Corporation'),
  ('777-77-7777', 'Shaf', '246 Birch St', '555-555-7777', 'Individual'),
  ('888-88-8888', 'Abdullah', '135 Walnut St', '555-555-8888', 'Individual'),
  ('999-99-9999', 'Asad', '864 Chestnut St', '555-555-9999', 'Corporation'),
  ('111-22-3333', 'Umer', '975 Elm St', '555-555-1212', 'Individual'),
  ('222-33-4444', 'Ahsan', '214 Pine St', '555-555-2323', 'Individual'),
  ('333-44-5555', 'Hamza', '753 Maple St', '555-555-3434', 'Corporation'),
  ('444-55-6666', 'Iqbal', '621 Birch St', '555-555-4545', 'Individual'),
  ('555-66-7777', 'Noman', '369 Walnut St', '555-555-5656', 'Individual'),
  ('666-77-8888', 'Waqar', '963 Chestnut St', '555-555-6767', 'Corporation'),
  ('777-88-9999', 'Ali', '468 Cedar St', '555-555-7878', 'Individual'),
  ('888-99-0000', 'Kamal', '852 Oak St', '555-555-8989', 'Individual'),
  ('999-00-1111', 'M Umer', '147 Pine St', '555-555-9090', 'Corporation'),
  ('123-45-6789', 'M Abdullah', '369 Maple St', '555-555-1010', 'Individual'),
  ('234-56-7890', 'Waseem', '951 Elm St', '555-555-2020', 'Individual');


  INSERT INTO Employee (Ssn, Name, Address, Phone, Salary, Shift)
VALUES
  ('123-45-6788', 'Ali', '123 Main St, Anytown USA', '555-1234', 50000, 'Day'),
  ('234-56-7891', 'Noman', '456 Oak St, Anytown USA', '555-2345', 45000, 'Night'),
  ('345-67-8900', 'M Ali', '789 Maple St, Anytown USA', '555-3456', 55000, 'Day'),
  ('456-78-9010', 'Muhammad', '321 Elm St, Anytown USA', '555-4567', 60000, 'Night'),
  ('567-89-0122', 'Ali Ahmad', '654 Cedar St, Anytown USA', '555-5678', 48000, 'Day'),
  ('678-90-1233', 'M Waseem', '987 Pine St, Anytown USA', '555-6789', 52000, 'Night'),
  ('789-01-2344', 'Babar', '246 Birch St, Anytown USA', '555-7890', 58000, 'Day'),
  ('890-12-3455', 'Shaheen', '369 Spruce St, Anytown USA', '555-8901', 53000, 'Night'),
  ('901-23-4565', 'Rizwan', '159 Oak St, Anytown USA', '555-9012', 57000, 'Day'),
  ('012-34-5676', 'Haris', '753 Maple St, Anytown USA', '555-0123', 51000, 'Night'),
  ('123-45-6789', 'M Haris', '369 Cedar St, Anytown USA', '555-1234', 49000, 'Day'),
  ('234-56-7890', 'Shadab', '852 Pine St, Anytown USA', '555-2345', 62000, 'Night'),
  ('345-67-8901', 'Abdullah', '741 Birch St, Anytown USA', '555-3456', 54000, 'Day'),
  ('456-78-9012', 'M Abdullah', '963 Spruce St, Anytown USA', '555-4567', 59000, 'Night'),
  ('567-89-0123', 'Shahzad', '258 Elm St, Anytown USA', '555-5678', 51000, 'Day'),
  ('678-90-1234', 'Hassan', '147 Oak St, Anytown USA', '555-6789', 56000, 'Night'),
  ('789-01-2345', 'Saad', '369 Cedar St, Anytown USA', '555-7890', 53000, 'Day'),
  ('890-12-3456', 'M Hassan', '852 Pine St, Anytown USA', '555-8901', 60000, 'Night'),
  ('901-23-4567', 'M Saad', '741 Birch St, Anytown USA', '555-9012', 57000, 'Day'),
  ('012-34-5678', 'M Noman', '963 Spruce St, Anytown USA', '555-0123', 52000, 'Night');


  INSERT INTO Pilot (Ssn, Licnum, Restrictions)
VALUES 
	   ('123-45-6788', 'P086423', 'None'),
       ('234-56-7891', 'P876545', 'Glasses'),
       ('345-67-8900', 'P365432', 'Contacts'),
       ('456-78-9010', 'P687099', 'None'),
       ('567-89-0122', 'P567899', 'Glasses'),
       ('678-90-1233', 'P678900', 'None'),
       ('789-01-2344', 'P789011', 'Contacts'),
       ('890-12-3455', 'P890123', 'None'),
       ('901-23-4565', 'P901234', 'Glasses'),
       ('012-34-5676', 'P012345', 'Contacts'),
       ('123-45-6789', 'P123456', 'None'),
       ('234-56-7890', 'P234567', 'Glasses'),
       ('345-67-8901', 'P345678', 'Contacts'),
       ('456-78-9012', 'P456789', 'None'),
       ('567-89-0123', 'P567890', 'Glasses'),
       ('678-90-1234', 'P678901', 'None'),
	   ('789-01-2345', 'P543545', 'Contacts'),
	   ('890-12-3456', 'P245643', 'Glasses'),
	   ('901-23-4567', 'P343532', 'None' ),
		('012-34-5678','P324443', 'Glasses' );



INSERT INTO Service (Id, Date, Hours, WorkCode)
VALUES
(1, '2023-01-05', 2.5, 'Oil Change'),
(2, '2023-03-12', 1.75, 'Tire Rotation'),
(3, '2023-03-25', 3.25, 'Brake Check'),
(4, '2023-01-12', 4.0, 'Engine Overhaul'),
(5, '2023-01-15', 2.0, 'Inspection'),
(6, '2023-01-17', 1.5, 'Oil Change'),
(7, '2023-01-20', 3.0, 'Tire Change'),
(8, '2023-01-22', 2.75, 'Electrical Repair'),
(9, '2022-01-25', 1.0, 'Battery Replacement'),
(10, '2022-01-27', 4.5, 'Engine Repair'),
(11, '2022-02-01', 2.0, 'Inspection'),
(12, '2022-02-05', 3.25, 'Brake Repair'),
(13, '2022-02-07', 1.75, 'Oil Change'),
(14, '2022-02-10', 2.5, 'Tire Rotation'),
(15, '2022-02-12', 4.0, 'Engine Overhaul'),
(16, '2022-02-15', 2.0, 'Inspection'),
(17, '2022-02-17', 1.5, 'Oil Change'),
(18, '2022-02-20', 3.0, 'Tire Change'),
(19, '2022-02-22', 2.75, 'Electrical Repair'),
(20, '2022-02-25', 1.0, 'Battery Replacement');


INSERT INTO owns (AirplaneRegNum, OwnerSsn, pdate)
VALUES
('N303CD', '111-11-1111', '2023-03-13'),
('N202BC', '222-22-2222', '2021-05-23'),
('N101AB', '333-33-3333', '2021-10-15'),
('N404DE', '444-44-4444', '2022-03-12'),
('N505EF', '555-55-5555', '2023-03-26'),
('N606FG', '666-66-6666', '2022-01-20'),
('N707GH', '333-33-3333', '2021-06-14'),
('N808HI', '888-88-8888', '2021-11-29'),
('N909IJ', '999-99-9999', '2022-02-28'),
('N1010JK', '111-22-3333', '2021-08-11'),
('N1111KL', '222-33-4444', '2021-12-05'),
('N1212LM', '333-44-5555', '2022-03-16'),
('N1313MN', '444-55-6666', '2021-07-02'),
('N1414NO', '555-66-7777', '2021-09-30'),
('N1515OP', '666-77-8888', '2021-11-07'),
('N1616PQ', '777-88-9999', '2022-01-11'),
('N1717QR', '888-99-0000', '2021-06-02'),
('N1818RS', '999-00-1111', '2021-10-18'),
('N1919ST', '123-45-6789', '2021-12-20'),
('N2020TU', '234-56-7890', '2022-03-22');



INSERT INTO Maintain (EmployeeSsn, ServiceId)
VALUES ('123-45-6789', 1),
       ('234-56-7890', 2),
       ('345-67-8901', 3),
       ('456-78-9012', 4),
       ('567-89-0123', 5),
       ('678-90-1234', 6),
       ('789-01-2345', 7),
       ('890-12-3456', 8),
       ('901-23-4567', 9),
       ('012-34-5678', 10),
       ('123-45-6789', 11),
       ('234-56-7890', 12),
       ('345-67-8901', 13),
       ('456-78-9012', 14),
       ('567-89-0123', 15),
       ('678-90-1234', 16),
       ('789-01-2345', 17),
       ('890-12-3456', 18),
       ('901-23-4567', 19),
       ('012-34-5678', 20);


INSERT INTO Plane_Service (AirplaneRegNum, ServiceId) VALUES
('N101AB', 1),
('N202BC', 2),
('N303CD', 3),
('N404DE', 4),
('N505EF', 5),
('N606FG', 6),
('N707GH', 7),
('N808HI', 8),
('N909IJ', 9),
('N1010JK', 10),
('N1111KL', 11),
('N1212LM', 12),
('N1313MN', 13),
('N1414NO', 14),
('N1515OP', 15),
('N1616PQ', 16),
('N1717QR', 17),
('N1818RS', 18),
('N1919ST', 19);



INSERT INTO Flies (PilotLicNum, Model)
VALUES 
    ('P086423', 'Boeing 747'),
    ('P876545', 'Piper PA-28'),
    ('P365432', 'Cessna 172'),
    ('P687099', 'Cessna 182'),
    ('P567899', 'Beechcraft Bonanza'),
    ('P678900', 'Mooney M20'),
    ('P789011', 'Cirrus SR22'),
    ('P890123', 'Diamond DA40'),
    ('P901234', 'Piper PA-34'),
    ('P012345', 'Cessna 210'),
    ('P123456', 'Piper PA-32'),
    ('P234567', 'Beechcraft King Air'),
    ('P345678', 'Cessna 150'),
    ('P456789', 'Piper PA-38'),
    ('P567890', 'Piper PA-24'),
    ('P678901', 'Cessna 152'),
    ('P543545', 'Cessna 206'),
    ('P245643', 'Cessna 208'),
    ('P343532', 'Piper PA-44'),
    ('P324443', 'Beechcraft Baron');



INSERT INTO Works_On (EmployeeSsn, Model)
VALUES
('123-45-6789', 'Boeing 747'),
('234-56-7890', 'Piper PA-28'),
('345-67-8901', 'Cessna 172'),
('456-78-9012', 'Cessna 182'),
('567-89-0123', 'Beechcraft Bonanza'),
('678-90-1234', 'Mooney M20'),
('789-01-2345', 'Cirrus SR22'),
('890-12-3456', 'Diamond DA40'),
('901-23-4567', 'Piper PA-34'),
('012-34-5678', 'Cessna 210'),
('123-45-6789', 'Piper PA-32'),
('234-56-7890', 'Beechcraft King Air'),
('345-67-8901', 'Cessna 150'),
('456-78-9012', 'Piper PA-38'),
('567-89-0123', 'Piper PA-24'),
('678-90-1234', 'Cessna 152'),
('789-01-2345', 'Cessna 206'),
('890-12-3456', 'Cessna 208'),
('901-23-4567', 'Piper PA-44'),
('012-34-5678', 'Beechcraft Baron');




/*Queries*/


/*3*/
SELECT Airplane.RegNum
FROM Airplane
LEFT OUTER JOIN Plane_Service ON Airplane.RegNum = Plane_Service.AirplaneRegNum
WHERE Plane_Service.AirplaneRegNum IS NULL;
/*EXPLAINATION: This SQL query is using a left outer join to match all records from the Airplane table with matching records from the Plane_Service table based on the RegNum column.*/


/*4*/
SELECT DISTINCT o.Name, o.Address
FROM Owner o
JOIN Owns ON o.Ssn = Owns.OwnerSsn
JOIN Airplane ON Owns.AirplaneRegNum = Airplane.RegNum
JOIN PlaneType ON Airplane.OfType = PlaneType.Model
WHERE o.Category = 'corporation' AND PlaneType.Capacity > 200;
/*EXPLAINATION:This SQL query retrieves the names and addresses of all corporations that own airplanes with a capacity greater than 200, by joining the Owner, Owns, Airplane,
and PlaneType tables and filtering the results based on the given conditions.*/

/*5*/
SELECT AVG(Salary) as AverageSalary
FROM Employee
WHERE Shift = 'night'; 
/*EXPLAINATION: This SQL query calculates the average salary of employees who work the night shift from the Employee table
and returns the result as a single value under the alias "AverageSalary". */

/*6 */

SELECT TOP 5 Employee.Name, SUM(Service.Hours) AS TotalMaintenanceHours
FROM Employee
JOIN Maintain ON Employee.Ssn = Maintain.EmployeeSsn
JOIN Service ON Maintain.ServiceId = Service.Id
GROUP BY Employee.Name
ORDER BY TotalMaintenanceHours DESC;
/*EXPLAINATION:This SQL query retrieves the top 5 employee names and the total maintenance hours they have worked on services 
 ordered by the descending order of total maintenance hours. */

/*7 */

SELECT Airplane.RegNum, PlaneType.Model
FROM Airplane
INNER JOIN Plane_Service ON Airplane.RegNum = Plane_Service.AirplaneRegNum
INNER JOIN Service ON Plane_Service.ServiceId = Service.Id
INNER JOIN PlaneType ON Airplane.OfType = PlaneType.Model
WHERE Service.Date >= DATEADD(day, -7, GETDATE());
/* Explaination: This SQL query returns the registration numbers and plane models of airplanes that received a service within the last seven days */

/* 8 */

SELECT o.Name, o.Phone
FROM Owner o
INNER JOIN Owns p ON o.Ssn = p.OwnerSsn
WHERE p.Pdate BETWEEN DATEADD(month, -1, GETDATE()) AND GETDATE();
/*EXPLAINATION:This SQL query retrieves the names and phone numbers of owners who purchased an airplane within the last month,
by joining the Owner and Owns tables and filtering the results based on the given condition.*/

/* 9 */

SELECT Pilot.Ssn, COUNT(DISTINCT Airplane.RegNum) AS NumAuthorizedPlanes
FROM Pilot
JOIN Flies ON Pilot.LicNum = Flies.PilotLicNum
JOIN Airplane ON Flies.Model = Airplane.OfType
GROUP BY Pilot.Ssn;
/*EXPLAINATION:This SQL query selects the Social Security Number (Ssn) of each pilot and counts the number of distinct airplanes they are authorized to fly */
/* 10  */

SELECT TOP 1 Location, Capacity - COUNT(RegNum) AS AvailableSpace
FROM Hangar
LEFT JOIN Airplane ON Hangar.Number = Airplane.StoredIn
GROUP BY Hangar.Number, Location, Capacity
ORDER BY AvailableSpace DESC;
/*EXPLAINATION:This SQL query selects the hangar location and available space by subtracting the count of airplanes stored in the hangar from its capacity */

/* 11 */
SELECT o.Category, COUNT(*) AS NumOfPlanes
FROM Airplane a
INNER JOIN Owns ow ON a.RegNum = ow.AirplaneRegNum
INNER JOIN Owner o ON ow.OwnerSsn = o.Ssn
GROUP BY o.Category
ORDER BY NumOfPlanes DESC;
/*EXPLAINATION:This SQL query counts the number of airplanes owned by each owner category and displays the result in descending order
, by joining the Airplane, Owns, and Owner tables and grouping the results by Owner category.*/


/*12 */
SELECT Airplane.OfType AS PlaneType, AVG(Service.Hours) AS AvgMaintenanceHours
FROM Airplane
JOIN Plane_Service ON Airplane.RegNum = Plane_Service.AirplaneRegNum
JOIN Service ON Plane_Service.ServiceId = Service.Id
GROUP BY Airplane.OfType;
/*EXPLAINATION:This SQL query selects the airplane type and average maintenance hours for each type
by joining the Airplane, Plane_Service, and Service tables, grouping the results by airplane type. */

/* 13  */

SELECT DISTINCT o.Name
FROM Owner o
JOIN Owns ON o.Ssn = Owns.OwnerSsn
JOIN Airplane ON Owns.AirplaneRegNum = Airplane.RegNum
JOIN PlaneType ON Airplane.OfType = PlaneType.Model
JOIN Plane_Service ON Airplane.RegNum = Plane_Service.AirplaneRegNum
JOIN Service ON Plane_Service.ServiceId = Service.Id
JOIN Maintain ON Service.Id = Maintain.ServiceId
JOIN Employee ON Maintain.EmployeeSsn = Employee.Ssn
WHERE NOT EXISTS (
    SELECT *
    FROM Works_On
    WHERE Works_On.EmployeeSsn = Employee.Ssn
    AND Works_On.Model = PlaneType.Model
);
/*EXPLAINATION:This SQL query selects the name of owners whose planes have been serviced by maintenance employees who have not worked on the same type of plane for another airline */

/* 14 */
SELECT o.Name, o.Phone
FROM Owner o
INNER JOIN Owns ow ON o.Ssn = ow.OwnerSsn
INNER JOIN Airplane a ON ow.AirplaneRegNum = a.RegNum
INNER JOIN Hangar h ON a.StoredIn = h.Number
INNER JOIN Owner corp ON corp.Category = 'corporation' AND h.Location = corp.Address
WHERE o.Address = corp.Address;
/*EXPLAINATION:This SQL query selects the name and phone number of owners whose planes are stored in a hangar owned by a corporation at the same address as the owner */

/* 15 */
SELECT DISTINCT e.Name
FROM Pilot p
JOIN Flies f ON p.LicNum = f.PilotLicNum
JOIN Plane_Service ps ON f.Model = ps.AirplaneRegNum
JOIN PlaneType pt ON f.Model = pt.Model
JOIN Maintain m ON ps.ServiceId = m.ServiceId
JOIN Employee e ON p.Ssn = e.Ssn
/*EXPLAINATION:This SQL query selects the distinct names of employees who have worked on the maintenance of planes flown */

/* 16 */
SELECT Employee.Name, SUM(Service.Hours) AS TotalHours
FROM Employee
JOIN Maintain ON Employee.Ssn = Maintain.EmployeeSsn
JOIN Service ON Maintain.ServiceId = Service.Id
JOIN Plane_Service ON Service.Id = Plane_Service.ServiceId
JOIN Airplane ON Plane_Service.AirplaneRegNum = Airplane.RegNum
JOIN Owns ON Airplane.RegNum = Owns.AirplaneRegNum
JOIN Owner ON Owns.OwnerSsn = Owner.Ssn
WHERE Owner.Ssn = 'corporation_ssn'
GROUP BY Employee.Name
ORDER BY TotalHours DESC;
/*EXPLAINATION: This SQL query selects the names of employees who have worked on the maintenance of airplanes owned by a specific corporation
  and calculates the total maintenance hours for each employee */
/* 17 */

SELECT Airplane.RegNum
FROM Airplane
LEFT JOIN Plane_Service ON Airplane.RegNum = Plane_Service.AirplaneRegNum
LEFT JOIN Service ON Plane_Service.ServiceId = Service.Id
LEFT JOIN Maintain ON Service.Id = Maintain.ServiceId
WHERE Maintain.EmployeeSsn IS NULL;
/*EXPLAINATION:This SQL query selects the registration numbers of airplanes that have not been serviced by any maintenance employee */

/* 18 */
SELECT DISTINCT o.Name, o.Address 
FROM Owner o
JOIN Owns o1 ON o.Ssn = o1.OwnerSsn
JOIN Airplane a ON a.RegNum = o1.AirplaneRegNum
JOIN PlaneType pt ON pt.Model = a.OfType
JOIN Owns o2 ON o2.AirplaneRegNum = a.RegNum
JOIN Owner o3 ON o3.Ssn = o2.OwnerSsn
WHERE o.Category = 'corporation'
AND o3.Category = 'corporation'
AND o1.Pdate BETWEEN DATEADD(month, -1, GETDATE()) AND GETDATE()
AND o2.Pdate BETWEEN DATEADD(month, -1, GETDATE()) AND GETDATE()
AND o1.OwnerSsn <> o2.OwnerSsn
AND EXISTS (
    SELECT 1 FROM Owns o4
    JOIN Airplane a2 ON a2.RegNum = o4.AirplaneRegNum
    WHERE o4.OwnerSsn = o3.Ssn
    AND a2.OfType = pt.Model
    AND o4.Pdate BETWEEN DATEADD(month, -1, GETDATE()) AND GETDATE()
)
/*EXPLAINATION: This SQL query selects the names and addresses of corporations that have owned airplanes of the same plane type as another corporation*/
/* 19 */

SELECT Hangar.Number, COUNT(Airplane.RegNum) AS TotalPlanes
FROM Hangar 
LEFT JOIN Airplane ON Hangar.Number = Airplane.StoredIn
GROUP BY Hangar.Number;
/*EXPLAINATION: This query counts the number of planes in each hangar by performing a left join between the "Hangar" and "Airplane" tables
on the "Number" and "StoredIn" columns, respectively and grouping the result by the hangar number. */

/* 20 */

SELECT OfType AS PlaneType, COUNT(*) AS NumPlanes
FROM Airplane
GROUP BY OfType
ORDER BY NumPlanes DESC;
/*EXPLAINATION: This query counts the number of planes for each plane type and sorts them in descending order. */

/* 21*/

SELECT Airplane.RegNum, COUNT(*) AS TotalServices
FROM Airplane
JOIN Plane_Service ON Airplane.RegNum = Plane_Service.AirplaneRegNum
GROUP BY Airplane.RegNum;
/*EXPLAINATION: This SQL statement selects the registration number of airplanes and the total number of services they have received by joining the "Airplane" and "Plane_Service" tables
and grouping the results by the registration number.*/

/* 22 */

SELECT Shift, AVG(Salary) AS AverageSalary
FROM Employee
GROUP BY Shift;
/*EXPLAINATION:This SQL query retrieves the number of planes owned by each owner by joining the "Owner" and "Owns" tables and grouping the results by owner name. */

/* 23 */

SELECT o.Name, COUNT(*) AS NumPlanes
FROM Owner o
JOIN Owns p ON o.Ssn = p.OwnerSsn
GROUP BY o.Name;
/*EXPLAINATION: This SQL query retrieves the number of planes owned by each owner by joining the "Owner" and "Owns" tables and grouping the results by owner name.*/

/* 24 */

SELECT 
  Pilot.LicNum AS PilotLicenseNumber, 
  COUNT(PlaneType.Model) AS NumberOfPlanesAuthorized 
FROM 
  Pilot 
  JOIN Flies ON Pilot.LicNum = Flies.PilotLicNum 
  JOIN PlaneType ON Flies.Model = PlaneType.Model 
GROUP BY 
  Pilot.LicNum;
  /*EXPLAINATION:This SQL query counts the number of planes each pilot is authorized to fly based on their license number by joining the "Pilot", "Flies",
    and "PlaneType" tables and grouping the results by pilot license number. */


/* 25 */

/*Query 1*/
SELECT Airplane.OfType, SUM(Service.Hours * Employee.Salary) AS TotalRevenue
FROM Airplane
JOIN Plane_Service ON Airplane.RegNum = Plane_Service.AirplaneRegNum
JOIN Service ON Plane_Service.ServiceId = Service.Id
JOIN Maintain ON Service.Id = Maintain.ServiceId
JOIN Employee ON Maintain.EmployeeSsn = Employee.Ssn
GROUP BY Airplane.OfType;

/*EXPLAINATION: This query is important because it can help in identifying the most profitable airplane models for the airline.
It can be used by the finance or business departments to make strategic decisions regarding fleet management and investment. */


/*Query 2*/
SELECT OfType, COUNT(*) AS Total FROM Airplane GROUP BY OfType

/* EXPLAINATION:This query groups all airplanes by their type and returns the total count of airplanes for each type.
This query could be used to determine which airplane types are the most commonly used or to identify any imbalances in the distribution of airplane types. */


/*Query 3*/
SELECT Hangar.Number, Hangar.Capacity - COUNT(*) AS Available
FROM Hangar LEFT JOIN Airplane ON Hangar.Number = Airplane.StoredIn
GROUP BY Hangar.Number, Hangar.Capacity
/* EXPLAINATION:This query selects the number and available capacity of all hangars. 
It does this by joining the Hangar table with the Airplane table and grouping the results by the hangar number and capacity. */


/*Query 4*/
SELECT Employee.Ssn, Employee.Name, SUM(Service.Hours) AS TotalHours
FROM Employee
JOIN Maintain ON Employee.Ssn = Maintain.EmployeeSsn
JOIN Service ON Maintain.ServiceId = Service.Id
GROUP BY Employee.Ssn, Employee.Name;
 /* EXPLAINATION: This query is important because it can help in identifying the most productive employees in terms of airplane maintenance
 which can be useful for performance evaluation and reward systems.
 It can be used by maintenance departments or human resources departments in airlines.  */


# ST10441604_INSY6112_exam
q.3.1
CREATE TABLE Patient (
    PatientID INT AUTO_INCREMENT PRIMARY KEY, -- Surrogate Primary Key
    FirstName VARCHAR(100) NOT NULL,
    LastName VARCHAR(100) NOT NULL,
    DateOfBirth DATE,
    Gender ENUM('Male', 'Female', 'Other'),
    PhoneNumber VARCHAR(15),
    Email VARCHAR(100) UNIQUE,
    Address VARCHAR(255),
    RegistrationDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

q3.2
CREATE TABLE Doctor (
    DoctorID INT AUTO_INCREMENT PRIMARY KEY, -- Surrogate Primary Key
    FirstName VARCHAR(100) NOT NULL,
    LastName VARCHAR(100) NOT NULL,
    Specialty VARCHAR(100),
    PhoneNumber VARCHAR(15),
    Email VARCHAR(100) UNIQUE,
    HireDate DATE
);
q3.3
CREATE TABLE Appointment (
    AppointmentID INT AUTO_INCREMENT PRIMARY KEY, -- Surrogate Primary Key
    PatientID INT NOT NULL, -- Foreign Key to Patient table
    DoctorID INT NOT NULL, -- Foreign Key to Doctor table
    AppointmentDateTime DATETIME NOT NULL,
    Reason VARCHAR(255),
    Status ENUM('Scheduled', 'Completed', 'Cancelled') DEFAULT 'Scheduled',

    -- Define Foreign Key Constraints
    FOREIGN KEY (PatientID) REFERENCES Patient(PatientID),
    FOREIGN KEY (DoctorID) REFERENCES Doctor(DoctorID)
);

q3.4
-- 1. Clean up previous tables in reverse dependency order
DROP TABLE IF EXISTS Appointment;
DROP TABLE IF EXISTS Patient;
DROP TABLE IF EXISTS Doctor;

-- 2. CREATE TABLE statements

-- Question: Write an SQL statement to create the Patient Table
CREATE TABLE Patient (
    PatientID INT PRIMARY KEY, -- Using INT for explicit ID setting
    FirstName VARCHAR(100) NOT NULL,
    LastName VARCHAR(100) NOT NULL,
    DateOfBirth DATE,
    Gender ENUM('Male', 'Female', 'Other') DEFAULT 'Other',
    PhoneNumber VARCHAR(15) DEFAULT 'N/A',
    Email VARCHAR(100) UNIQUE,
    Address VARCHAR(255),
    RegistrationDate TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Question: Write an SQL statement to create the Doctor table
CREATE TABLE Doctor (
    DoctorID INT PRIMARY KEY, -- Using INT for explicit ID setting
    FirstName VARCHAR(100) NOT NULL,
    LastName VARCHAR(100) NOT NULL,
    Specialty VARCHAR(100) DEFAULT 'General Practice',
    PhoneNumber VARCHAR(15) DEFAULT 'N/A',
    Email VARCHAR(100) UNIQUE,
    HireDate DATE DEFAULT (CURRENT_DATE())
);

-- Question: Write an SQL statement to create the Appointment table
CREATE TABLE Appointment (
    AppointmentID INT PRIMARY KEY, -- Using INT for explicit ID setting
    PatientID INT NOT NULL,
    DoctorID INT NOT NULL,
    AppointmentDateTime DATETIME NOT NULL,
    Reason VARCHAR(255) DEFAULT 'Consultation',
    Status ENUM('Scheduled', 'Completed', 'Cancelled') DEFAULT 'Scheduled',

    -- Define Foreign Key Constraints
    FOREIGN KEY (PatientID) REFERENCES Patient(PatientID),
    FOREIGN KEY (DoctorID) REFERENCES Doctor(DoctorID)
);

-- 3. INSERT statements for the requested data

-- Question: write SQL statements to insert the following data:
-- Table: Patient
-- 1. Debbie Theart 1980-03-17 (PatientID 1)
-- 2. Thomas Duncan 1976-08-12 (PatientID 2)

INSERT INTO Patient (PatientID, FirstName, LastName, DateOfBirth, Email) VALUES
(1, 'Debbie', 'Theart', '1980-03-17', 'd.theart@example.com'),
(2, 'Thomas', 'Duncan', '1976-08-12', 't.duncan@example.com');


-- Table: Doctor
-- 1. Zintle Nukani (DoctorID 1)
-- 2. Ravi Maharaj (DoctorID 2)

INSERT INTO Doctor (DoctorID, FirstName, LastName, Email) VALUES
(1, 'Zintle', 'Nukani', 'z.nukani@clinic.com'),
(2, 'Ravi', 'Maharaj', 'r.maharaj@clinic.com');


-- Table: Appointments
-- AppointmentID1 Date: 2025-01-15 Time: 9:00 Duration: 15 DoctorID2 PatientID1
-- AppointmentID2 Date: 2025-01-18 Time: 15:00 Duration: 30 DoctorID2 PatientID2
-- AppointmentID3 Date: 2025-01-20 Time: 10:00 Duration: 15 DoctorID1 PatientID1
-- AppointmentID4 Date: 2025-01-21 Time: 11:00 Duration: 15 DoctorID2 PatientID1

INSERT INTO Appointment (AppointmentID, AppointmentDateTime, DoctorID, PatientID, Reason) VALUES
(1, '2025-01-15 09:00:00', 2, 1, 'Consultation (Duration: 15 min)'),
(2, '2025-01-18 15:00:00', 2, 2, 'Consultation (Duration: 30 min)'),
(3, '2025-01-20 10:00:00', 1, 1, 'Consultation (Duration: 15 min)'),
(4, '2025-01-21 11:00:00', 2, 1, 'Consultation (Duration: 15 min)');

-- 4. Final SELECT statements to verify data

SELECT '--- Patient Data ---' AS TableName;
SELECT * FROM Patient;

SELECT '--- Doctor Data ---' AS TableName;
SELECT * FROM Doctor;

SELECT '--- Appointment Data ---' AS TableName;
SELECT * FROM Appointment;




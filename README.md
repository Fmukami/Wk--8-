# Wk--8-
Assignment for week 8
-- Create the database
CREATE DATABASE IF NOT EXISTS ClinicDB;
USE ClinicDB;

-- Table: Specializations
CREATE TABLE Specializations (
    specializationID INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL UNIQUE
);

-- Table: Doctors
CREATE TABLE Doctors (
    doctorID INT AUTO_INCREMENT PRIMARY KEY,
    fullName VARCHAR(100) NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    phone VARCHAR(15) NOT NULL UNIQUE,
    specializationID INT,
    FOREIGN KEY (specializationID) REFERENCES Specializations(specializationID)
);

-- Table: Patients
CREATE TABLE Patients (
    patientID INT AUTO_INCREMENT PRIMARY KEY,
    fullName VARCHAR(100) NOT NULL,
    dateOfBirth DATE NOT NULL,
    email VARCHAR(100) NOT NULL UNIQUE,
    phone VARCHAR(15) NOT NULL UNIQUE
);

-- Table: Appointments
CREATE TABLE Appointments (
    appointmentID INT AUTO_INCREMENT PRIMARY KEY,
    patientID INT NOT NULL,
    doctorID INT NOT NULL,
    appointmentDate DATETIME NOT NULL,
    reason TEXT,
    FOREIGN KEY (patientID) REFERENCES Patients(patientID),
    FOREIGN KEY (doctorID) REFERENCES Doctors(doctorID),
    UNIQUE (doctorID, appointmentDate) -- Prevent double-booking
);

-- Table: DoctorAvailability (optional but practical)
-- Shows when doctors are available, supports scheduling logic
CREATE TABLE DoctorAvailability (
    availabilityID INT AUTO_INCREMENT PRIMARY KEY,
    doctorID INT NOT NULL,
    availableDate DATE NOT NULL,
    startTime TIME NOT NULL,
    endTime TIME NOT NULL,
    FOREIGN KEY (doctorID) REFERENCES Doctors(doctorID)
);

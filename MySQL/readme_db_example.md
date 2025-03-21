```sql

-- Step 1: Create Database
CREATE DATABASE Latihan;
USE Latihan;

-- Step 2: Create Tables
CREATE TABLE Students (
    StudentID INT PRIMARY KEY AUTO_INCREMENT,
    Name VARCHAR(100),
    Age INT,
    Email VARCHAR(100) UNIQUE
);

CREATE TABLE Classes (
    ClassID INT PRIMARY KEY AUTO_INCREMENT,
    ClassName VARCHAR(100) NOT NULL
);

CREATE TABLE StudentClasses (
    StudentID INT,
    ClassID INT,
    PRIMARY KEY (StudentID, ClassID),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (ClassID) REFERENCES Classes(ClassID)
);

CREATE TABLE Subjects (
    SubjectID INT PRIMARY KEY AUTO_INCREMENT,
    SubjectName VARCHAR(100) NOT NULL
);

CREATE TABLE Exams (
    ExamID INT PRIMARY KEY AUTO_INCREMENT,
    SubjectID INT,
    ExamDate DATE,
    TotalMarks INT,
    FOREIGN KEY (SubjectID) REFERENCES Subjects(SubjectID)
);

CREATE TABLE Results (
    ResultID INT PRIMARY KEY AUTO_INCREMENT,
    StudentID INT,
    ExamID INT,
    MarksObtained INT,
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (ExamID) REFERENCES Exams(ExamID)
);

-- Step 3: Insert Realistic Dummy Data
INSERT INTO Students (Name, Age, Email) VALUES 
('Alice Johnson', 18, 'alice.johnson@example.com'),
('Bob Smith', 19, 'bob.smith@example.com'),
('Charlie Brown', 20, 'charlie.brown@example.com'),
('David Williams', 21, 'david.williams@example.com'),
('Emma Davis', 22, 'emma.davis@example.com'),
('Franklin Harris', 18, 'franklin.harris@example.com'),
('Grace White', 19, 'grace.white@example.com'),
('Henry Martin', 20, 'henry.martin@example.com'),
('Ivy Thompson', 21, 'ivy.thompson@example.com'),
('Jack Robinson', 22, 'jack.robinson@example.com'),
('Kelly Clark', 18, 'kelly.clark@example.com'),
('Liam Lewis', 19, 'liam.lewis@example.com'),
('Mia Walker', 20, 'mia.walker@example.com'),
('Nathan Hall', 21, 'nathan.hall@example.com'),
('Olivia Allen', 22, 'olivia.allen@example.com'),
('Paul Young', 18, 'paul.young@example.com'),
('Quinn King', 19, 'quinn.king@example.com'),
('Rachel Scott', 20, 'rachel.scott@example.com'),
('Samuel Green', 21, 'samuel.green@example.com'),
('Tina Baker', 22, 'tina.baker@example.com');

-- Insert Classes
INSERT INTO Classes (ClassName) VALUES 
('Mathematics'),
('Science'),
('History'),
('English Literature'),
('Computer Science'),
('Biology'),
('Chemistry'),
('Physics'),
('Economics'),
('Geography');

-- Assign Students to Classes
INSERT INTO StudentClasses (StudentID, ClassID) VALUES 
(1, 1), (1, 2),
(2, 3), (2, 4),
(3, 1), (3, 5),
(4, 2), (4, 6),
(5, 3), (5, 7),
(6, 4), (6, 8),
(7, 5), (7, 9),
(8, 6), (8, 10),
(9, 7), (9, 1),
(10, 8), (10, 2),
(11, 9), (11, 3),
(12, 10), (12, 4),
(13, 1), (13, 5),
(14, 2), (14, 6),
(15, 3), (15, 7),
(16, 4), (16, 8),
(17, 5), (17, 9),
(18, 6), (18, 10),
(19, 7), (19, 1),
(20, 8), (20, 2);

-- Insert Subjects
INSERT INTO Subjects (SubjectName) VALUES 
('Algebra'),
('Physics'),
('World History'),
('Shakespearean Literature'),
('Programming in Python'),
('Organic Chemistry'),
('Microeconomics'),
('Human Geography'),
('Astronomy'),
('Statistics');

-- Insert Exams
INSERT INTO Exams (SubjectID, ExamDate, TotalMarks) VALUES 
(1, '2024-06-10', 100),
(2, '2024-06-12', 100),
(3, '2024-06-15', 100),
(4, '2024-06-18', 100),
(5, '2024-06-20', 100),
(6, '2024-06-22', 100),
(7, '2024-06-25', 100),
(8, '2024-06-27', 100),
(9, '2024-06-30', 100),
(10, '2024-07-02', 100);

-- Insert Results
INSERT INTO Results (StudentID, ExamID, MarksObtained) VALUES 
(1, 1, 85), (1, 2, 78),
(2, 3, 92), (2, 4, 88),
(3, 5, 74), (3, 6, 90),
(4, 7, 81), (4, 8, 77),
(5, 9, 69), (5, 10, 95),
(6, 1, 80), (6, 2, 85),
(7, 3, 75), (7, 4, 91),
(8, 5, 82), (8, 6, 89),
(9, 7, 87), (9, 8, 90),
(10, 9, 73), (10, 10, 84),
(11, 1, 70), (11, 2, 79),
(12, 3, 95), (12, 4, 89),
(13, 5, 77), (13, 6, 92),
(14, 7, 85), (14, 8, 80),
(15, 9, 76), (15, 10, 88),
(16, 1, 94), (16, 2, 90),
(17, 3, 81), (17, 4, 87),
(18, 5, 73), (18, 6, 79),
(19, 7, 78), (19, 8, 84),
(20, 9, 88), (20, 10, 92);
,,,

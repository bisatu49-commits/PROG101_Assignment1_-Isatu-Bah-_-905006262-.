# Pseudocode: Student Attendance and Performance Management System

**Course:** PROG101 Assignment 1
**Purpose:** Register students, mark attendance, record scores and generate a performance report that flags students who need support.
**Author:** Isatu Bah

---

## 3. Pseudocode

### 3.1 Constants, Variables and Data Types

```
 1  CONSTANTS
 2      PASS_MARK = 50
 3      MIN_ATTENDANCE = 75
 4      MAX_SCORE = 100
 5      MAX_STUDENTS = 80
 6      GRADE_A_MIN = 80
 7      GRADE_B_MIN = 70
 8      GRADE_C_MIN = 60

 1  RECORD Student
 2      studentID : String
 3      studentName : String
 4      daysPresent : Integer
 5      totalDays : Integer
 6      totalScore : Real
 7      scoreCount : Integer
 8  END RECORD

 1  VARIABLES
 2      students : Array[MAX_STUDENTS] of Student
 3      studentID : String
 4      studentName : String
 5      attendanceStatus : String
 6      score : Real
 7      attendancePct : Real
 8      averageScore : Real
 9      grade : String
10      status : String
11      studentCount : Integer
12      atRiskCount : Integer
13      choice : Integer
14      index : Integer
```

---

### 3.2 Main Module

```
 1  MODULE Main
 2      studentCount = 0
 3      DO
 4          CALL DisplayMenu()
 5          READ choice
 6          IF choice = 1 THEN
 7              CALL RegisterStudent()
 8          ELSE IF choice = 2 THEN
 9              CALL MarkAttendance()
10          ELSE IF choice = 3 THEN
11              CALL RecordScores()
12          ELSE IF choice = 4 THEN
13              CALL GenerateReport()
14          ELSE IF choice = 5 THEN
15              DISPLAY "Exiting system"
16          ELSE
17              DISPLAY "Invalid choice"
18          END IF
19      WHILE choice != 5
20  END MODULE
```

---

### 3.3 Display Menu Module

```
 1  MODULE DisplayMenu
 2      DISPLAY "STUDENT ATTENDANCE AND PERFORMANCE SYSTEM"
 3      DISPLAY "1. Register Student"
 4      DISPLAY "2. Mark Attendance"
 5      DISPLAY "3. Record Scores"
 6      DISPLAY "4. Generate Report"
 7      DISPLAY "5. Exit"
 8      DISPLAY "Enter your choice: "
 9  END MODULE
```

---

### 3.4 Register Student Module

```
 1  MODULE RegisterStudent
 2      IF studentCount >= MAX_STUDENTS THEN
 3          DISPLAY "Class is full"
 4          RETURN
 5      END IF
 6      READ studentID, studentName
 7      IF studentID = "" OR studentName = "" THEN
 8          DISPLAY "All fields required"
 9          RETURN
10      END IF
11      IF StudentExists(studentID) = TRUE THEN
12          DISPLAY "Student already registered"
13      ELSE
14          CALL SaveStudent(studentID, studentName)
15          DISPLAY "Student registered successfully"
16      END IF
17  END MODULE
```

---

### 3.5 Student Exists Function

```
 1  FUNCTION StudentExists(studentID) RETURNS Boolean
 2      FOR index = 1 TO studentCount
 3          IF students[index].studentID = studentID THEN
 4              RETURN TRUE
 5          END IF
 6      END FOR
 7      RETURN FALSE
 8  END FUNCTION
```

---

### 3.6 Save Student Module

```
 1  MODULE SaveStudent(studentID, studentName)
 2      studentCount = studentCount + 1
 3      students[studentCount].studentID = studentID
 4      students[studentCount].studentName = studentName
 5      students[studentCount].daysPresent = 0
 6      students[studentCount].totalDays = 0
 7      students[studentCount].totalScore = 0
 8      students[studentCount].scoreCount = 0
 9  END MODULE
```

---

### 3.7 Mark Attendance Module

```
 1  MODULE MarkAttendance
 2      IF studentCount = 0 THEN
 3          DISPLAY "No students registered"
 4          RETURN
 5      END IF
 6      FOR index = 1 TO studentCount
 7          DISPLAY students[index].studentName
 8          READ attendanceStatus
 9          WHILE attendanceStatus != "P" AND attendanceStatus != "A" DO
10              DISPLAY "Invalid input. Enter P for Present or A for Absent"
11              READ attendanceStatus
12          END WHILE
13          students[index].totalDays = students[index].totalDays + 1
14          IF attendanceStatus = "P" THEN
15              students[index].daysPresent = students[index].daysPresent + 1
16          END IF
17      END FOR
18  END MODULE
```

---

### 3.8 Record Scores Module

```
 1  MODULE RecordScores
 2      IF studentCount = 0 THEN
 3          DISPLAY "No students registered"
 4          RETURN
 5      END IF
 6      FOR index = 1 TO studentCount
 7          DISPLAY students[index].studentName
 8          READ score
 9          WHILE score < 0 OR score > MAX_SCORE DO
10              DISPLAY "Invalid score. Enter 0 to 100"
11              READ score
12          END WHILE
13          students[index].totalScore = students[index].totalScore + score
14          students[index].scoreCount = students[index].scoreCount + 1
15      END FOR
16  END MODULE
```

---

### 3.9 Functions

```
 1  FUNCTION CalculateAttendance(daysPresent, totalDays) RETURNS Real
 2      IF totalDays = 0 THEN
 3          RETURN 0
 4      END IF
 5      RETURN (daysPresent / totalDays) * 100
 6  END FUNCTION

 1  FUNCTION CalculateAverage(totalScore, scoreCount) RETURNS Real
 2      IF scoreCount = 0 THEN
 3          RETURN 0
 4      END IF
 5      RETURN totalScore / scoreCount
 6  END FUNCTION

 1  FUNCTION DetermineGrade(averageScore) RETURNS String
 2      IF averageScore >= GRADE_A_MIN THEN
 3          RETURN "A"
 4      ELSE IF averageScore >= GRADE_B_MIN THEN
 5          RETURN "B"
 6      ELSE IF averageScore >= GRADE_C_MIN THEN
 7          RETURN "C"
 8      ELSE IF averageScore >= PASS_MARK THEN
 9          RETURN "D"
10      ELSE
11          RETURN "F"
12      END IF
13  END FUNCTION

 1  FUNCTION CheckRisk(attendancePct, averageScore) RETURNS String
 2      IF attendancePct < MIN_ATTENDANCE AND averageScore < PASS_MARK THEN
 3          RETURN "HIGH RISK"
 4      ELSE IF attendancePct < MIN_ATTENDANCE OR averageScore < PASS_MARK THEN
 5          RETURN "AT RISK"
 6      ELSE
 7          RETURN "GOOD STANDING"
 8      END IF
 9  END FUNCTION
```

---

### 3.10 Generate Report Module

```
 1  MODULE GenerateReport
 2      IF studentCount = 0 THEN
 3          DISPLAY "No students registered"
 4          RETURN
 5      END IF
 6      atRiskCount = 0
 7      DISPLAY "Student Performance Report"
 8      FOR index = 1 TO studentCount
 9          attendancePct = CalculateAttendance(students[index].daysPresent, students[index].totalDays)
10          averageScore = CalculateAverage(students[index].totalScore, students[index].scoreCount)
11          grade = DetermineGrade(averageScore)
12          status = CheckRisk(attendancePct, averageScore)
13          IF status != "GOOD STANDING" THEN
14              atRiskCount = atRiskCount + 1
15          END IF
16          DISPLAY students[index].studentName, attendancePct, averageScore, grade, status
17      END FOR
18      DISPLAY "Total students needing attention: ", atRiskCount
19  END MODULE
```

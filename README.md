# PROG101 Assignment 1: Student Attendance and Performance Management System

**Course:** PROG101, Principles of Programming Logic and Design

## About the Project

This repository contains the pseudocode design for a Student Attendance and Performance Management System. The system helps a lecturer register students, mark attendance, record scores, and generate a performance report that flags students who need support.

## What the System Does

1. **Register students** (up to 80 per class, no duplicate IDs)
2. **Mark attendance** (P for Present, A for Absent, with input validation)
3. **Record scores** (0 to 100, with input validation)
4. **Generate a report** showing attendance percentage, average score, grade and risk status

## Key Rules

| Rule | Value |
|------|-------|
| Pass mark | 50 |
| Minimum attendance | 75% |
| Maximum score | 100 |
| Maximum students | 80 |

**Grading scale:** A (80+), B (70-79), C (60-69), D (50-59), F (below 50)

**Risk status:**
- **HIGH RISK**: attendance below 75% and average below 50
- **AT RISK**: attendance below 75% or average below 50
- **GOOD STANDING**: meets both requirements

## Files

| File | Description |
|------|-------------|
| `pseudocode.md` | Full pseudocode: constants, variables, main module, sub-modules and functions |

## Author

Isatu Bah
GitHub: [bisatu49-commits](https://github.com/bisatu49-commits)

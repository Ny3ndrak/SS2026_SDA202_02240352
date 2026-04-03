# Practical 3: Class Diagram & Object Diagram

## 1. Class Diagram

The class diagram shows the static structure of the Automated Grading System. It defines eight classes: Student, Professor, Admin, Assignment, Submission, GradeRecord, PlagiarismReport, and AuditReport, along with their attributes, operations, and associations.

Key relationships:
- Student (1) makes (0) Submission
- Professor (1) creates (1) Assignment
- Submission (1) produces (1) GradeRecord
- Submission (1) generates (1) PlagiarismReport
- AuditReport (1) contains (0) GradeRecord

---

## 2. Object Diagram

The object diagram represents a snapshot of a system at a particular time, consisting of actual instances related to each other. It validates a class diagram as it maps instances to their classes and links to their associations.

| Object | Notable Values |
|---|---|
| karma : Student | attemptNumber = 2 |
| norbu : Professor | department = SWE |
| yeshi : Admin | generatedAt = 2026-04-01 |
| asgn1 : Assignment | dueDate = 2026-03-24 23:59 |
| sub1 : Submission | status = submitted |
| grade1 : GradeRecord | score = 85.0 |
| plagReport1 : PlagiarismReport | similarityScore = 12.5% |
| auditRpt1 : AuditReport | reportId = AUD001 |

Links use plain association lines (no arrowheads) as per UML object diagram notation.
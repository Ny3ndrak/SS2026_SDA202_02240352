# Practical 2
## Scenario
A university has expanded its Software Engineering course and needs an automated way to grade simple programming assignments. At present, students submit through GitHub, and professors manually clone repositories, run code in the terminal, and inspect results in VS Code.

## Business Outcome
The main goal is to make grading faster, fairer, and easier to track, while also checking plagiarism and sending final grades to the LMS.

## Step 1: Actor-to-Actor IoD
The first diagram focuses on how actors interact to achieve the outcome before any system detail is introduced.

In this interaction:

- The professor publishes the assignment, grading criteria, and submission deadline to the student.
- The student submits an assignment attempt to the professor.
- The professor returns the grade and feedback to the student.
- The professor sends grading records to the admin.
- The admin provides audit evidence to the regulatory body.

### Reflection on Step 1
This first diagram helped me focus on the people involved before thinking about the software. It made it clear that the process is not only about students and professors. Admin staff and the regulatory body also matter because grading records must be checked and audited. This step helped me understand the bigger picture behind the assignment.

## Step 2: Functional Use Case Diagram
Using the actor interactions above, the next step is to define what the system must do to support them.

The system needs to support these main functions:

- Students must be able to submit assignments.
- The system must run and execute the submitted code.
- The system must detect plagiarism by checking other submissions and external tools like TurnItIn.
- Students must be able to view grades and feedback.
- Students must be able to resubmit if another attempt is allowed.
- Grades must be synchronized to the university LMS.
- Professors must be able to set due dates.
- Professors must be able to define grading criteria.
- Admin staff must be able to generate audit reports when needed.

These functions are connected. For example, a submission leads to code execution, code execution leads to plagiarism checking, and final results lead to grade syncing and audit reporting.

### Reflection on Step 2
The use case diagram helped me move from people and interactions to system functions. I could clearly see what the system needs to do, such as accept submissions, run code, detect plagiarism, store results, and send grades to the LMS. It also showed that features like deadlines, resubmissions, and audit reports are just as important as the grading itself.

## Step 3: IoD Based on the Use Cases
The final diagram shows how actors interact with each other with the support of the system to achieve the outcome.

The full process works like this:

1. The professor sets the grading criteria and the submission deadline.
2. The student uploads assignment code to the system.
3. The system checks whether the deadline has passed.
4. If the deadline has passed, the system rejects the submission.
5. If the submission is still allowed, the system compares it with other submissions for plagiarism.
6. The system sends the submission to TurnItIn and receives a plagiarism report.
7. The system runs the code against the grading criteria.
8. The system stores the grade record.
9. The system pushes the grade to the LMS.
10. The student views the grade and feedback.
11. If allowed, the student can resubmit and repeat the process.
12. The admin can request an audit report, which is then provided to the regulatory body.

### Reflection on Step 3
This final diagram brought everything together. It showed the full flow from setting the criteria, to student submission, to plagiarism checking, grading, LMS update, and audit reporting. I found this step useful because it showed how the actors and the system support each other to reach the final outcome. It also made the decision points easier to understand, especially late submission rejection and resubmission.

## Overall Reflection
This practical showed me that it is easier to model a system step by step rather than trying to do everything in one diagram.

1. The actor-to-actor IoD shows who is involved and what they are trying to achieve.
2. The use case diagram shows what the system must be able to do.
3. The final IoD shows how the whole process works from start to finish.

I also learned that real systems are affected by practical issues like audits, an old LMS, and budget limits. These things may not be part of the core grading logic, but they still strongly affect how the system should be designed.

## AI Assistance Disclosure
I used DeepSeek Chat to help improve some of the wording and structure of this reflection. I reviewed the output and adjusted it so it matched the assignment scenario and my final report.

## References
DeepSeek AI. (2026). DeepSeek Chat (Large language model) [AI assistant]. https://chat.deepseek.com/
##  AWS Lambda Function for Amazon Lex Quiz

This Lambda function powers the **Amazon S3 Knowledge Quiz Chatbot** built with Amazon Lex.  
It handles user input, tracks quiz progress, provides immediate feedback, and calculates final scores.

---

### Key Features
- **Session Management**: Tracks answered questions using session attributes.  
- **Dynamic Feedback**: Provides instant feedback after each answer with explanations.  
- **Branching Logic**: Prompts users to continue or exit after every 3 questions.  
- **Score Calculation**: Computes quiz results with percentage and performance rating.  
- **Personalization**: Greets users by name and tailors responses.  

---

###  Workflow
1. **UserName Slot** → Prompts for learner’s name.  
2. **ReadyToStart Slot** → Confirms readiness before beginning the quiz.  
3. **Question Slots (1–10)** → Presents multiple-choice and true/false questions about Amazon S3.  
4. **Feedback** → Provides immediate correctness feedback with explanations.  
5. **ContinueQuiz Slot** → Offers option to continue or end early after 3, 6, or 9 questions.  
6. **Final Score** → Displays results, percentage, and performance rating at completion.  

---

###  Example Output
- Correct Answer:  
  `✓ Correct! S3 stands for Simple Storage Service, Amazon's object storage service.`  

- Incorrect Answer:  
  `✗ Incorrect. The correct answer is A. S3 stands for Simple Storage Service.`  

- Final Score:  
Quiz Complete, Ayabonga!
YOUR SCORE: 8/10 (80%)

Performance Rating:  Excellent! You have strong S3 knowledge!

# AWS S3 Knowledge Quiz Bot

Built an interactive quiz chatbot using AWS Lambda and Amazon Lex that tests users' knowledge of Amazon S3. The bot guides users through a 10-question quiz with personalized feedback and scoring.

# Features

# User Experience
- Personalized greeting with name collection
- Confirmation prompt before starting the quiz
- 10 multiple-choice and true/false questions about S3
- Progress check-ins after every 3 questions
- Option to exit early and see partial results
- Detailed score breakdown with performance rating

# Quiz Content
- S3 fundamentals and terminology
- Storage classes and features
- Bucket configuration and limits
- Object management concepts
- Durability and availability topics

# Scoring System
- Real-time answer validation
- Automatic score calculation
- Performance ratings based on percentage
- Shows correct answers for missed questions
- Supports both full completion and early exit

# Technical Implementation

# AWS Services Used
- AWS Lambda for backend logic
- Amazon Lex for conversational interface
- Session management for tracking progress

# Key Functionality
- Answer normalization for flexible input handling
- Slot-based conversation flow
- Session attributes for state management
- Dynamic question progression
- Conditional prompts based on progress

# Quiz Structure

The bot asks 10 questions covering S3 topics with automatic grading and feedback. Users can complete the full quiz or exit after questions 3, 6, or 9 to receive a partial score.

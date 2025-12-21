import json

def lambda_handler(event, context):
    # Extract sessionId from event
    session_id = event['sessionId']
    intent_name = event['sessionState']['intent']['name']
    slots = event['sessionState']['intent']['slots']
    
    # Get session attributes (for tracking state across invocations)
    session_attributes = event['sessionState'].get('sessionAttributes', {})
    
    # Question texts
    questions_text = {
        'Question1': "Question 1 of 10: What does S3 stand for? A) Simple Storage Service B) Secure Server Storage C) Smart Storage System. Please answer A, B, or C.",
        'Question2': "Question 2 of 10: What is Amazon S3 mainly used for? A) Cloud storage B) Database management C) Virtual machines. Please answer A, B, or C.",
        'Question3': "Question 3 of 10: S3 objects are stored in what? A) Databases B) Buckets C) Folders. Please answer A, B, or C.",
        'Question4': "Question 4 of 10: What is the maximum size of a single S3 object? A) 5 TB B) 1 TB C) 10 TB. Please answer A, B, or C.",
        'Question5': "Question 5 of 10: Is S3 a regional or global service? A) Regional B) Global C) Both regional and global. Please answer A, B, or C.",
        'Question6': "Question 6 of 10: Which storage class is most cost-effective for infrequent access? A) S3 Standard B) S3 Glacier C) S3 Intelligent-Tiering. Please answer A, B, or C.",
        'Question7': "Question 7 of 10: Can S3 host static websites? Please answer True or False.",
        'Question8': "Question 8 of 10: What does S3 use to organize and identify objects? A) Keys B) Tags C) Indexes. Please answer A, B, or C.",
        'Question9': "Question 9 of 10: True or False: S3 supports versioning. Please answer True or False.",
        'Question10': "Question 10 of 10: S3 provides how many 9's of durability? A) 9 nines (99.999999999%) B) 11 nines (99.999999999%) C) 5 nines (99.999%). Please answer A, B, or C."
    }
    
    # Correct answers
    correct_answers = {
        'Question1': 'A', 'Question2': 'A', 'Question3': 'B', 'Question4': 'A',
        'Question5': 'A', 'Question6': 'B', 'Question7': 'True', 'Question8': 'A',
        'Question9': 'True', 'Question10': 'B'
    }
    
    # Detailed explanations for each question
    explanations = {
        'Question1': "S3 stands for Simple Storage Service, Amazon's object storage service.",
        'Question2': "Amazon S3 is primarily used for cloud storage of objects and files.",
        'Question3': "S3 objects are stored in buckets, which are containers for objects.",
        'Question4': "The maximum size of a single S3 object is 5 TB.",
        'Question5': "S3 is a regional service - buckets are created in specific AWS regions.",
        'Question6': "S3 Glacier is the most cost-effective storage class for infrequent access and archival.",
        'Question7': "True! S3 can host static websites with HTML, CSS, and JavaScript files.",
        'Question8': "S3 uses keys (unique identifiers) to organize and identify objects within buckets.",
        'Question9': "True! S3 supports versioning to keep multiple versions of an object.",
        'Question10': "S3 provides 11 nines (99.999999999%) of durability for stored objects."
    }

    # --- Step 1: Handle UserName slot ---
    user_name_slot = slots.get('UserName', {})
    
    # Try to get the name from interpretedValue or originalValue
    user_name = None
    if user_name_slot and user_name_slot.get('value'):
        user_name = user_name_slot.get('value', {}).get('interpretedValue', '').strip()
        if not user_name:
            user_name = user_name_slot.get('value', {}).get('originalValue', '').strip()
    
    # If we still don't have a name, prompt for it
    if not user_name or len(user_name) < 1:
        return {
            'sessionId': session_id,
            'sessionState': {
                'dialogAction': {
                    'type': 'ElicitSlot',
                    'slotToElicit': 'UserName'
                },
                'intent': {
                    'name': intent_name,
                    'slots': slots,
                    'state': 'InProgress'
                }
            },
            'messages': [{'contentType': 'PlainText', 'content': "Hello! Welcome to the AWS S3 Knowledge Quiz. What's your name?"}]
        }

    # --- Step 2: Handle ReadyToStart slot ---
    ready_slot = slots.get('ReadyToStart', {})
    
    if ready_slot and ready_slot.get('value'):
        ready_value = ready_slot.get('value', {}).get('interpretedValue', '').lower().strip()
        
        if ready_value in ['no', 'false', 'nope', 'not ready', 'n', 'nah', 'stop']:
            return {
                'sessionId': session_id,
                'sessionState': {
                    'dialogAction': {'type': 'Close'},
                    'intent': {
                        'name': intent_name,
                        'state': 'Fulfilled',
                        'slots': slots
                    }
                },
                'messages': [{'contentType': 'PlainText', 'content': f"No problem, {user_name}! Come back when you're ready to take the quiz. Good luck with your studies!"}]
            }
    else:
        return {
            'sessionId': session_id,
            'sessionState': {
                'dialogAction': {
                    'type': 'ElicitSlot',
                    'slotToElicit': 'ReadyToStart'
                },
                'intent': {
                    'name': intent_name,
                    'slots': slots,
                    'state': 'InProgress'
                }
            },
            'messages': [{'contentType': 'PlainText', 'content': f"Welcome, {user_name}! Are you ready to start the S3 quiz? This will take approximately 5-7 minutes and contains 10 questions. Say yes when you're ready, or say no to exit."}]
        }

    # --- Step 3: Count answered questions and detect just-answered question ---
    answered_count = 0
    last_answered_question = None
    last_question_index = 0
    
    # Get previously answered questions from session
    previously_answered = session_attributes.get('answered_questions', '').split(',') if session_attributes.get('answered_questions') else []
    currently_answered = []
    
    for i in range(1, 11):
        q = f'Question{i}'
        if slots.get(q) and slots[q].get('value'):
            answered_count += 1
            currently_answered.append(q)
            # If this question wasn't in the previous list, it's the newly answered one
            if q not in previously_answered:
                last_answered_question = q
                last_question_index = i

    # Update session attributes with current answered questions
    session_attributes['answered_questions'] = ','.join(currently_answered)

    # --- Step 4: Provide immediate feedback for just-answered question ---
    feedback_to_show = ""
    if last_answered_question:
        user_answer = normalize_answer(slots[last_answered_question].get('value', {}).get('interpretedValue', ''))
        correct_answer = correct_answers[last_answered_question]
        explanation = explanations[last_answered_question]
        
        if user_answer == correct_answer:
            feedback_to_show = f"✓ Correct! {explanation}"
        else:
            feedback_to_show = f"✗ Incorrect. The correct answer is {correct_answer}. {explanation}"

    # --- Step 5: Check ContinueQuiz slot (asked every 3 questions) ---
    continue_slot = slots.get('ContinueQuiz', {})
    
    # Check if we need to ask about continuing
    needs_continue_prompt = answered_count in [3, 6, 9] and answered_count < 10
    
    # Check if continue was just handled
    continue_just_handled = session_attributes.get('continue_handled', '') == str(answered_count)
    
    if needs_continue_prompt and not continue_just_handled:
        if continue_slot and continue_slot.get('value'):
            continue_value = continue_slot.get('value', {}).get('interpretedValue', '').lower().strip()
            
            if continue_value in ['no', 'false', 'nope', 'stop', 'quit', 'exit', 'n', 'nah']:
                # User wants to stop
                return calculate_score(session_id, intent_name, slots, user_name, answered_count, partial=True, session_attributes=session_attributes)
            else:
                # User wants to continue - mark as handled and proceed
                slots['ContinueQuiz'] = None
                session_attributes['continue_handled'] = str(answered_count)
                # Fall through to next question
        else:
            # Need to ask if they want to continue
            continue_message = ""
            if feedback_to_show:
                continue_message = f"{feedback_to_show}\n\n"
            continue_message += f"You've completed {answered_count} questions so far! Would you like to continue with the remaining questions? Say yes to continue or no to see your score now."
            
            return {
                'sessionId': session_id,
                'sessionState': {
                    'dialogAction': {
                        'type': 'ElicitSlot',
                        'slotToElicit': 'ContinueQuiz'
                    },
                    'intent': {
                        'name': intent_name,
                        'slots': slots,
                        'state': 'InProgress'
                    },
                    'sessionAttributes': session_attributes
                },
                'messages': [{'contentType': 'PlainText', 'content': continue_message}]
            }

    # --- Step 6: If not all questions answered, ask next question ---
    if answered_count < 10:
        next_question_slot = None
        for i in range(1, 11):
            q = f'Question{i}'
            if not slots.get(q) or not slots[q].get('value'):
                next_question_slot = q
                break

        if next_question_slot:
            # Build message with feedback
            if answered_count == 0:
                message = f"Great! Let's begin.\n\n{questions_text[next_question_slot]}"
            else:
                message = ""
                if feedback_to_show:
                    message = f"{feedback_to_show}\n\nWould you like the next question?\n\n"
                message += questions_text[next_question_slot]
            
            return {
                'sessionId': session_id,
                'sessionState': {
                    'dialogAction': {
                        'type': 'ElicitSlot',
                        'slotToElicit': next_question_slot
                    },
                    'intent': {
                        'name': intent_name,
                        'slots': slots,
                        'state': 'InProgress'
                    },
                    'sessionAttributes': session_attributes
                },
                'messages': [{'contentType': 'PlainText', 'content': message}]
            }

    # --- Step 7: All questions answered - Show feedback for last question, then calculate score ---
    if feedback_to_show and answered_count == 10:
        # Show feedback for the last answer before showing final score
        session_attributes['final_feedback_shown'] = 'true'
        
        # Check if we already showed final feedback
        if session_attributes.get('final_feedback_shown') != 'done':
            session_attributes['final_feedback_shown'] = 'done'
            # Ask if they want to see their final score
            message = f"{feedback_to_show}\n\nYou've completed all 10 questions! Would you like to see your final score?"
            
            return {
                'sessionId': session_id,
                'sessionState': {
                    'dialogAction': {
                        'type': 'ConfirmIntent'
                    },
                    'intent': {
                        'name': intent_name,
                        'slots': slots,
                        'state': 'InProgress'
                    },
                    'sessionAttributes': session_attributes
                },
                'messages': [{'contentType': 'PlainText', 'content': message}]
            }
    
    # Calculate and show final score
    return calculate_score(session_id, intent_name, slots, user_name, 10, partial=False, session_attributes=session_attributes)


def normalize_answer(answer):
    """Normalize answer to handle variations in True/False and A/B/C"""
    if not answer:
        return "No answer"
    
    answer = str(answer).strip().lower()
    
    # Handle True/False variations
    if answer in ['true', 't', 'yes', 'y']:
        return 'True'
    elif answer in ['false', 'f', 'no', 'n']:
        return 'False'
    # Handle A/B/C answers
    elif answer in ['a', 'b', 'c']:
        return answer.upper()
    else:
        return answer.upper() if len(answer) == 1 else answer


def calculate_score(session_id, intent_name, slots, user_name, questions_answered, partial=False, session_attributes=None):
    """Calculate and return the quiz score"""
    
    if session_attributes is None:
        session_attributes = {}
    
    correct_answers = {
        'Question1': 'A', 'Question2': 'A', 'Question3': 'B', 'Question4': 'A',
        'Question5': 'A', 'Question6': 'B', 'Question7': 'True', 'Question8': 'A',
        'Question9': 'True', 'Question10': 'B'
    }
    
    answers = {}
    for i in range(1, questions_answered + 1):
        q = f'Question{i}'
        raw_ans = slots.get(q, {}).get('value', {}).get('interpretedValue', '')
        answers[q] = normalize_answer(raw_ans)

    score = 0
    results = []

    for i in range(1, questions_answered + 1):
        q = f'Question{i}'
        user_ans = answers.get(q, "No answer")
        correct_ans = correct_answers[q]
        if user_ans == correct_ans:
            score += 1
            results.append(f"{i}. {user_ans} ✓ Correct")
        else:
            results.append(f"{i}. {user_ans} ✗ (Correct answer: {correct_ans})")

    percentage = (score / questions_answered) * 100 if questions_answered > 0 else 0
    results_text = "\n".join(results)

    if partial:
        final_message = f"""Quiz Ended Early, {user_name}!

You answered {questions_answered} out of 10 questions.

📊 YOUR SCORE: {score}/{questions_answered} ({percentage:.0f}%)

Your Answers:
{results_text}

Performance Rating:
"""
    else:
        final_message = f"""Quiz Complete, {user_name}!

📊 YOUR SCORE: {score}/{questions_answered} ({percentage:.0f}%)

Your Answers:
{results_text}

Performance Rating:
"""
    
    if percentage >= 90:
        final_message += "🌟 Outstanding! You're an S3 expert!"
    elif percentage >= 80:
        final_message += "🎯 Excellent! You have strong S3 knowledge!"
    elif percentage >= 70:
        final_message += "👍 Good job! You have solid understanding of S3!"
    elif percentage >= 60:
        final_message += "✓ Passing! Review the topics you missed for improvement."
    else:
        final_message += "📚 Keep learning! Review AWS S3 documentation to strengthen your knowledge."

    final_message += f"\n\nThank you for taking the quiz, {user_name}!"

    return {
        'sessionId': session_id,
        'sessionState': {
            'dialogAction': {'type': 'Close'},
            'intent': {
                'name': intent_name,
                'state': 'Fulfilled',
                'slots': slots
            },
            'sessionAttributes': session_attributes
        },
        'messages': [{'contentType': 'PlainText', 'content': final_message}]
    }

# Chatlish 
# Word of the Day WhatsApp Bot with n8n

This project is an automated WhatsApp bot that sends a daily "Word of the Day" to a specified WhatsApp number. The bot fetches new English words, generates conversation topics, and quizzes , stores the data in Google Sheets, and handles incoming messages for grammar correction using AI.

---

## Features

* Fetches a new English word daily that hasn’t been used before.
* Generates:

  * Word meaning
  * Plural form
  * Example sentence
  * Conversation topic
  * Multiple-choice quiz questions
* Stores all word information in Google Sheets.
* Sends the word and related info via WhatsApp using Twilio.
* Handles incoming WhatsApp messages:

  * Corrects grammar, spelling, and punctuation.
  * Provides polite and clear AI-generated answers.
* Maintains context memory for ongoing conversations.

---

## Technologies Used

* n8n – Workflow automation platform
* Twilio API – Sending and receiving WhatsApp messages
* Google Sheets API – Storing word data
* OpenRouter / Mistral-7B-Instruct – AI model for generating words, quizzes, and conversation topics
* JavaScript – Data manipulation and message formatting

---

## Workflow Overview

1. Schedule Trigger – Fires every day at 10 AM.
2. Get Row(s) from Google Sheets – Fetches all previously used words.
3. Generate Word List – Creates a comma-separated list of used words.
4. Fetch New Word (AI) – Uses OpenRouter/Mistral to generate a new word not in the list, with all required info.
5. Extract Word Info – Parses AI response into structured data (word, meaning, plural, example, conversation topic, quiz).
6. Append Row in Google Sheets – Saves the new word and its details.
7. Slice Message – Splits long messages for WhatsApp character limit.
8. Send WhatsApp Message (Twilio) – Sends the daily word info to the target number.
9. Incoming WhatsApp Webhook – Receives user messages, passes them to AI Agent for grammar correction and reply generation.
10. Memory Buffer – Maintains context of conversations for personalized responses.

---

## Setup

1. open n8n
2. Create Google Sheet – Include columns: Word, Meaning, Plural, Exemple Sentence.
3. Twilio Setup – Configure WhatsApp sandbox or production number.
4. OpenRouter AI – Create API key and set up credentials in n8n.
5. Import n8n Workflow – Use the provided JSON file in n8n.
6. Configure Credentials – For Google Sheets, Twilio, and OpenRouter.

---

## How to Use

* The bot will automatically send the daily word to the configured WhatsApp number(put your phone number in from in twilio).
* Users can reply to the bot for grammar correction and explanations.
* Check Google Sheets to see all words sent so far.

---

## Notes

* Messages are split into multiple parts if they exceed WhatsApp limits.
* The AI ensures words are not repeated by checking the Google Sheet.
* The workflow can be extended to add more language features or quizzes.

---

## License

This project is open source and available under the MIT License.

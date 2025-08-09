📚 SSC Exam Auto-Reply Telegram Bot (n8n + Gemini AI)
📌 Project Overview
This project is an AI-powered Telegram bot built with n8n and Google Gemini AI, designed to instantly answer SSC (Staff Selection Commission) exam-related questions.

💡 Whether it’s General Knowledge, Mathematics, Reasoning, or English, the bot provides:

Direct answers

Step-by-step explanations

Preparation tips

Motivational messages

If the question is not SSC-related, the bot politely asks the user to stay on topic.

🚀 Features
SSC-only Filtering → Uses keyword detection to ensure responses are exam-specific.

AI-Generated Answers → Integrates Google Gemini API for rich, detailed responses.

Telegram Integration → Works directly inside Telegram chats.

Clean Message Formatting → Removes messy Markdown and escapes special characters.

Auto-Splitting Long Responses → Handles Telegram’s 4096-character limit automatically.

Two-Way Logic:

SSC questions → Answer with AI

Non-SSC questions → Send default guidance message

🛠 Tech Stack
n8n – No-code/low-code automation platform

Google Gemini AI API – Natural language responses

Telegram Bot API – Message sending and receiving

JavaScript (inside n8n Function Nodes) – Logic, formatting, and text processing

📂 Workflow Structure
Telegram Trigger

Captures incoming messages from Telegram users.

Filter Node

Ensures the message contains text and is longer than 1 character.

Code Node (SSC Detection)

Checks if the message contains SSC-related keywords.

Builds the AI system prompt.

IF Node

True branch → Sends to Gemini API for answer generation.

False branch → Sends a default “SSC only” message.

Gemini API Node

Processes the SSC question and returns the answer.

Code Node (Formatting & Cleaning)

Cleans text (removes unwanted slashes/Markdown).

Escapes characters for Telegram MarkdownV2.

Splits long messages into chunks ≤ 4096 chars.

Telegram Send Message Node

Sends final cleaned and formatted messages to the user.

⚙️ How It Works
User sends a question to the bot.

Workflow checks if it’s SSC-related.

If SSC → Query Gemini API → Format & send answer.
If not SSC → Send friendly redirection message.

Long answers are automatically split into multiple Telegram messages.

📷 Workflow Screenshot<img width="877" height="319" alt="image" src="https://github.com/user-attachments/assets/ced15614-06f7-42c8-95f5-dd9b97bbb00e" />
Key Code Snippet – Cleaning & Splitting AI Response
javascript
Copy
Edit
function cleanTextForUser(text) {
  return text
    .replace(/\*\*(.*?)\*\*/g, '$1') // Remove **bold**
    .replace(/\\/g, '')              // Remove backslashes
    .replace(/ +/g, ' ')             // Remove extra spaces
    .replace(/\n{3,}/g, '\n\n')      // Limit blank lines
    .trim();
}

function escapeMarkdownV2(text) {
  return text
    .replace(/_/g, '\\_')
    .replace(/\*/g, '\\*')
    .replace(/\[/g, '\\[')
    .replace(/\]/g, '\\]')
    .replace(/\(/g, '\\(')
    .replace(/\)/g, '\\)')
    .replace(/~/g, '\\~')
    .replace(/`/g, '\\`')
    .replace(/>/g, '\\>')
    .replace(/#/g, '\\#')
    .replace(/\+/g, '\\+')
    .replace(/-/g, '\\-')
    .replace(/=/g, '\\=')
    .replace(/\|/g, '\\|')
    .replace(/{/g, '\\{')
    .replace(/}/g, '\\}')
    .replace(/\./g, '\\.')
    .replace(/!/g, '\\!');
}
📦 Installation & Setup
Create a Telegram Bot

Talk to @BotFather and get your bot token.

Get Google Gemini API Key

Sign up at Google AI Studio.

Install n8n

bash
Copy
Edit
npm install -g n8n
n8n start
Import Workflow

In n8n UI → “Import from File” → Select the provided JSON workflow.

Configure Credentials

Add Telegram API credentials with your bot token.

Add Google Gemini API credentials with your API key.

Activate Workflow

Turn on the workflow and start chatting with your bot!

🎯 Example Interaction
User:

swift
Copy
Edit
What is the full form of SSC CGL?
Bot:

rust
Copy
Edit
SSC CGL stands for Staff Selection Commission Combined Graduate Level Examination.

📌 Staff Selection Commission (SSC): Government body for recruitment.
📌 Combined Graduate Level (CGL): Exam for graduates for multiple posts.
📌 Examination: The competitive test itself.
💡 Future Enhancements
Add support for subject-wise practice questions.

Include image-based reasoning questions with OCR.

Multi-language support for Hindi & regional languages.

Store user history for personalized learning.

👨‍💻 Author
Mohamed Irfan
💼 Java Full Stack Developer | React Enthusiast | AI Workflow Builder
linkedin.com/in/mohamed-irfan-762527252

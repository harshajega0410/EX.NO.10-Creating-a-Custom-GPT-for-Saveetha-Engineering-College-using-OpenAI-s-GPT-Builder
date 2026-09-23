# EX.NO.10-Creating-a-Custom-GPT-for-Saveetha-Engineering-College-using-OpenAI-s-GPT-Builder
## AIM
To understand the concept of a Custom GPT and to design, build, configure, and publish a Custom GPT chatbot for Saveetha Engineering College (www.saveetha.ac.in) using OpenAI's GPT Builder, so that it can answer student and visitor questions about the college's courses, admissions, fees, facilities, and placements.
## WHAT IS A CUSTOM GPT?
A Custom GPT is a personalised version of ChatGPT that can be built without writing any code. It is created by giving the GPT Builder three things: a name, a set of Instructions that describe how it should behave, and (optionally) reference files called Knowledge that it reads before answering. Once published, the Custom GPT behaves like a specialised chatbot — for example, a “Saveetha Engineering College Assistant” that always answers using the college's own information instead of general internet knowledge.
### TOOLS REQUIRED
•	Web browser – Google Chrome or Microsoft Edge
•	A ChatGPT account with a Plus, Team, Enterprise, or Edu subscription (the GPT Builder is not available on the free plan)
•	OpenAI's GPT Builder – built into ChatGPT, opened from chatgpt.com/create
•	Reference material about Saveetha Engineering College, collected from www.saveetha.ac.in (About, Courses, Admission, Placement, and Contact pages)
•	MS Word / Google Docs – to organise the collected information into clean Knowledge files (PDF/DOCX) before uploading
•	(Optional) Canva or the built-in DALL·E image generator – to design a profile picture/logo for the GPT
## PROCEDURE
### Step 1: Collecting College Information (Knowledge Preparation)
Before building the GPT, gather accurate information about Saveetha Engineering College from its official website www.saveetha.ac.in. Visit and note down content from pages such as About Us, Departments/Courses Offered, Admission Procedure, Fee Structure, Placements, Facilities, and Contact Details. Paste this content into a Word document and save it as a PDF. This file becomes the “Knowledge” for the GPT, so that it answers only with correct, college-specific information instead of guessing.
### Step 2: Signing in to ChatGPT
Open a web browser and go to chatgpt.com. Sign in using an existing OpenAI account, or create a new one. Make sure the account is upgraded to a ChatGPT Plus, Team, Enterprise, or Edu plan, since the GPT Builder is a paid-plan feature and is not available on the free version.
### Step 3: Opening the GPT Builder
On the left sidebar, click “Explore GPTs” and then click the “+ Create” button (or go directly to chatgpt.com/create). This opens the GPT Builder, which has two tabs: Create and Configure.
### Step 4: Building the GPT Conversationally (Create Tab)
In the Create tab, type a plain-English description of the required GPT in the message box, for example:
“Create a GPT for Saveetha Engineering College that answers questions about admissions, courses, fees, placements, and campus facilities in a friendly and professional tone.”
The Builder chats back and automatically suggests a name, a short description, and a profile picture for the GPT based on this description.
### Step 5: Fine-Tuning with the Configure Tab
Switch to the Configure tab for full manual control over the GPT, and fill in the following fields:
•	Name: e.g., “Saveetha Engineering College Assistant”
•	Description: a one-line summary, e.g., “Your guide to admissions, courses, fees, and placements at Saveetha Engineering College.”
•	Instructions: a detailed system prompt describing the GPT's role, tone, and rules (see the sample instructions given later in this report).
•	Conversation starters: four sample questions users can click to begin the chat, for example:
1.	What B.Tech courses does Saveetha Engineering College offer?
2.	How do I apply for admission?
3.	What is the placement record of the college?
4.	Where is the campus located?
### Step 6: Uploading Knowledge Files
In the Knowledge section of the Configure tab, click “Upload files” and add the PDF/DOCX file prepared in Step 1. This lets the GPT search and quote from the actual college content instead of guessing, which keeps its answers accurate and trustworthy. As a best practice, upload 2 to 5 well-organised files rather than many small ones, since retrieval accuracy drops once too many files are added.
### Step 7: Enabling Capabilities
In the Capabilities section, select the tools the GPT is allowed to use:
•	Web Browsing – to fetch live information if the uploaded knowledge file becomes outdated
•	Code Interpreter & Data Analysis – not usually needed for a college-information bot, so it can be left off
•	Image Generation (DALL·E) – optional, for generating a campus or course-related illustration
For a simple college-information GPT, enabling Web Browsing along with the uploaded Knowledge is generally enough.
### Step 8: Setting Up Actions (Optional, Advanced)
Actions allow the GPT to call an external API — for example, to check live seat availability or fetch the latest fee notification from a college server. This requires an API endpoint and an OpenAPI schema, so it is optional for a basic informational GPT and can be skipped by beginners.
### Step 9: Testing the GPT
Use the Preview panel on the right side of the Builder to chat with the GPT before publishing it. Ask sample questions such as “What courses are offered?” or “How do I apply for admission?” and check whether the answers are correct, polite, and based on the uploaded knowledge. If any answer is wrong or incomplete, edit the Instructions or Knowledge files and test again until the responses are accurate.
### Step 10: Publishing and Sharing
Click the “Create” (or “Save”) button in the top-right corner of the Builder. Choose who can access the GPT:
•	Only me – for personal testing
•	Anyone with the link – to share with students and faculty of the department
•	GPT Store (Public) – to make the GPT visible to all ChatGPT users
Click “Publish”/“Update” to finish. Copy the generated link and share it with students through the college portal, WhatsApp group, or LMS.
### PROGRAM
```
import re
import random


knowledge_base = {

    "greeting": {
        "patterns": [
            r"\bhi\b",
            r"\bhello\b",
            r"\bhey\b",
            r"\bgood morning\b",
            r"\bgood afternoon\b",
            r"\bgood evening\b"
        ],
        "responses": [
            "Hello! Welcome to the Saveetha Engineering College Admission Help Desk.",
            "Hi! How can I help you with Saveetha Engineering College admissions?",
            "Welcome! I can help you with courses, admissions, fees, placements and facilities."
        ]
    },

    "courses": {
        "patterns": [
            r"\bcourses\b",
            r"\bcourse\b",
            r"\bb\.?tech\b",
            r"\bprograms\b",
            r"\bbranches\b",
            r"\bdepartments\b"
        ],
        "responses": [
            "Saveetha Engineering College offers B.Tech/B.E programmes in areas such as "
            "Computer Science and Engineering, Information Technology, Electronics and "
            "Communication Engineering, Electrical and Electronics Engineering and Mechanical Engineering.",
            "The college offers undergraduate and postgraduate engineering programmes."
        ]
    },

    "admission": {
        "patterns": [
            r"\badmission\b",
            r"\bapply\b",
            r"\bapplication\b",
            r"\bhow.*join\b",
            r"\bhow.*admission\b",
            r"\bentrance\b"
        ],
        "responses": [
            "You can apply for admission through the official Saveetha Engineering College "
            "admission process. Visit www.saveetha.ac.in for the latest admission details.",
            "For admission, check the eligibility requirements, complete the application "
            "form, submit the required documents and follow the admission instructions "
            "provided by the college."
        ]
    },

    "eligibility": {
        "patterns": [
            r"\beligibility\b",
            r"\bqualification\b",
            r"\b12th\b",
            r"\bhigher secondary\b",
            r"\bmarks\b"
        ],
        "responses": [
            "Eligibility requirements depend on the programme. For B.Tech/B.E admission, "
            "students generally need to satisfy the required higher-secondary academic "
            "qualifications. Please check the official college website for the latest criteria."
        ]
    },

    "fees": {
        "patterns": [
            r"\bfees\b",
            r"\bfee\b",
            r"\bcost\b",
            r"\btuition\b",
            r"\bfee structure\b"
        ],
        "responses": [
            "The fee structure varies depending on the course and admission category. "
            "Please check the official Saveetha Engineering College website or contact "
            "the admission office for the current fee details."
        ]
    },

    "placements": {
        "patterns": [
            r"\bplacement\b",
            r"\bplacements\b",
            r"\bjob\b",
            r"\bjobs\b",
            r"\bcareer\b",
            r"\bcompanies\b"
        ],
        "responses": [
            "Saveetha Engineering College provides placement and career-support activities "
            "for students. Placement opportunities depend on the department, eligibility "
            "and recruitment company.",
            "For the latest placement statistics and recruiting companies, please refer "
            "to the official placement information of the college."
        ]
    },

    "facilities": {
        "patterns": [
            r"\bfacilities\b",
            r"\blibrary\b",
            r"\blab\b",
            r"\blaboratory\b",
            r"\bhostel\b",
            r"\bcampus\b"
        ],
        "responses": [
            "The college provides facilities such as laboratories, library, classrooms, "
            "campus infrastructure and student-support facilities.",
            "Hostel and other campus facilities are available subject to the college rules "
            "and availability."
        ]
    },

    "location": {
        "patterns": [
            r"\bwhere\b",
            r"\blocation\b",
            r"\baddress\b",
            r"\bcampus.*located\b",
            r"\bcollege.*located\b"
        ],
        "responses": [
            "Saveetha Engineering College is located in Chennai, Tamil Nadu. "
            "For the exact address and directions, please visit www.saveetha.ac.in."
        ]
    },

    "contact": {
        "patterns": [
            r"\bcontact\b",
            r"\bphone\b",
            r"\bemail\b",
            r"\badmission office\b",
            r"\bcontact details\b"
        ],
        "responses": [
            "For the latest contact number, email address and admission-office details, "
            "please visit the official website: www.saveetha.ac.in."
        ]
    },

    "thanks": {
        "patterns": [
            r"\bthank you\b",
            r"\bthanks\b",
            r"\bthank\b"
        ],
        "responses": [
            "You're welcome! Feel free to ask if you have more questions.",
            "You're welcome! Have a great day."
        ]
    },

    "goodbye": {
        "patterns": [
            r"\bbye\b",
            r"\bgoodbye\b",
            r"\bexit\b",
            r"\bquit\b"
        ],
        "responses": [
            "Thank you for using the Saveetha Engineering College Admission Chatbot. Goodbye!",
            "Goodbye! Visit www.saveetha.ac.in for more information."
        ]
    }
}



def get_response(user_input):

    user_input = user_input.lower().strip()

    for category, data in knowledge_base.items():

        for pattern in data["patterns"]:

            if re.search(pattern, user_input):
                return random.choice(data["responses"])

    return (
        "Sorry, I don't have information about that. "
        "Please ask about courses, admission, eligibility, fees, "
        "placements, facilities, location or contact details."
    )



print("=" * 60)
print("   SAVEETHA ENGINEERING COLLEGE ADMISSION CHATBOT")
print("=" * 60)

print("\nBot: Hello! Welcome to the Saveetha Engineering College")
print("     Admission Help Desk.")
print("     I can help you with courses, admissions, fees,")
print("     placements, facilities and contact details.")
print("     Type 'bye' to exit.\n")


while True:

    user_input = input("You: ")

    response = get_response(user_input)

    print("Bot:", response)

    if re.search(r"\b(bye|goodbye|exit|quit)\b",
                 user_input.lower()):
        break
```

## OUTPUT
<img width="1691" height="682" alt="image" src="https://github.com/user-attachments/assets/be5a5471-2805-41fc-9263-ef6bcfb53259" />

## RESULT
Thus, a Custom GPT chatbot for Saveetha Engineering College was successfully designed, configured with knowledge files and instructions, tested, and published using OpenAI's GPT
Builder.

## CONCLUSION

### In conclusion, building a Custom GPT shows how modern generative AI tools let anyone — even without programming knowledge — create a specialised, organisation-branded chatbot in a few simple steps. By combining clear instructions, focused knowledge files, and the right capabilities, Saveetha Engineering College can offer students and visitors instant, accurate answers to their questions, saving time for both the institution and its users.


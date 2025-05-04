# uAgent-Based-Medical-Trial-Matching
A Fetch.ai AgentVerse application using two uAgents — one representing doctors and the other representing patients/volunteers — to automate and simplify the matching process for medical and drug trials.

## Overview
This system is built around two autonomous agents:

FindAPatient: Acts as a doctor agent searching for suitable patients for a medical or drug trial.

iVolunteer: Acts as a patient/volunteer agent that registers interest and availability for trials based on category.

The agents communicate via uAgents and leverage ASI-1 MINI (ASI-MINI), a powerful AI model, to intelligently analyze patient data and handle natural language queries from doctors.

## Core Functionality
1. Patient Registration (iVolunteer.py)
Registers patient/volunteer details such as name, age, gender, contact info, and trial category.

Responds to doctor trial matching requests.

Sends registration data to the doctor agent upon startup.

2. Doctor Query & Matching (FindAPatient.py)
Receives volunteer registry from iVolunteer.

Accepts chat-based queries from doctors using natural language (e.g., "Find patients under 30").

Processes queries via ASI-MINI, returning relevant matches based on age, category, etc.

Sends trial invitations to matching patients.

3. Authentication & Security
Doctor agent requires a keyword (e.g., "fetch") to start a session before processing queries.

## How It Works
Startup:

iVolunteer sends a registry of patients to the FindAPatient agent.

FindAPatient stores this registry for later filtering.

Chat Protocol:

A doctor communicates using natural language (e.g., "find a covid-19 patient").

If authenticated, the message is processed using the ASI-1 MINI LLM.

The model analyzes the patient data and returns a natural language response.

Trial Matching:

FindAPatient can periodically contact potential patients matching the query.

Patients can accept/decline the offer.

Doctors are notified of match status.

## How to Use
### Prerequisites
Python 3.9+

uAgents

openai Python client (used for ASI-1)

### Installation
```bash
Copy
Edit
pip install uagents openai
🔑 ASI-1 API Key
Replace the placeholder in FindAPatient.py with your actual ASI-1 API key:

python
Copy
Edit
client = OpenAI(
    base_url='https://api.asi1.ai/v1',
    api_key='your_asi1_api_key_here'
)
```
### Running the Agents
In one terminal:

```bash
Copy
Edit
python iVolunteer.py
```
In another terminal:

```bash
Copy
Edit
python FindAPatient.py

### Chatting with the Doctor Agent
Once running, you can initiate a session and send queries using the chat protocol:

Send the password (e.g., "fetch") to authenticate.

Then send natural language queries like:

"Find patients over 60 years old"

"I need female patients for a cancer trial"

The system responds with matches and initiates contact with patients if available.

## File Structure
bash
Copy
Edit
.
├── FindAPatient.py       # Doctor agent handling queries and matching
├── iVolunteer.py         # Volunteer agent for patient data registration
└── README.md             # Project documentation

## Function Summary
FindAPatient.py
start: Initializes storage variables.

handle_chat: Manages authentication and processes doctor queries using ASI-1.

send_offer: Periodically attempts to contact uncontacted patients.

response_handler: Handles responses from patients.

handle_registry: Receives patient registry from volunteer.

handle_ack: Resets authentication when chat session ends.

iVolunteer.py
start: Loads patient data and sends it to the doctor.

handle_request: Responds to a doctor’s request based on category match.

## Powered By
Fetch.ai AgentVerse

uAgents framework

ASI-1 MINI LLM

## icense
This project is licensed under the MIT License.

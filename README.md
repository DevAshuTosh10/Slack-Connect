🚀 Slack Connect – Refold Intern Assignment
Slack Connect is a full-stack application that allows users to:

🔒 Securely connect to their Slack workspace using OAuth 2.0

✉️ Send immediate messages to channels

⏰ Schedule messages to be sent later

🗑️ View and manage (cancel) scheduled messages

📂 Project Structure
arduino
Copy
Edit
slack-connect/
├── backend/          // Node.js + Express + TypeScript
├── frontend/         // React + TypeScript
└── README.md
📦 Technology Stack
Layer	Tech Used
Frontend	React, TypeScript, Axios, React Router
Backend	Node.js, Express.js, TypeScript
OAuth	Slack OAuth 2.0
DB	SQLite / MongoDB (choose one)
Scheduler	node-cron
Deployment	(optional) Vercel, Render, Heroku

🛠️ Setup Instructions
1. Clone the Repository
bash
Copy
Edit
git clone https://github.com/yourusername/slack-connect.git
cd slack-connect
2. Backend Setup (/backend)
🔧 Install Dependencies
bash
Copy
Edit
cd backend
npm install
📁 Create .env file
env
Copy
Edit
SLACK_CLIENT_ID=your_slack_client_id
SLACK_CLIENT_SECRET=your_slack_client_secret
SLACK_REDIRECT_URI=http://localhost:5000/auth/callback
PORT=5000
▶️ Run Backend Server
bash
Copy
Edit
npm run dev
3. Frontend Setup (/frontend)
🔧 Install Dependencies
bash
Copy
Edit
cd frontend
npm install
📁 Create .env file
env
Copy
Edit
REACT_APP_API_BASE=http://localhost:5000
▶️ Run Frontend Server
bash
Copy
Edit
npm start
🔐 Slack App Configuration
Go to Slack API Dashboard

Create a new app from scratch

Enable OAuth & Permissions

Add redirect URI: http://localhost:5000/auth/callback

Add scopes:

chat:write

channels:read

Copy Client ID and Client Secret into .env

🧱 Architectural Overview
➤ OAuth Flow
Users click "Connect to Slack"

Redirected to Slack OAuth screen

Backend handles code and exchanges it for access_token and refresh_token

Tokens stored securely in database (along with team/user identifiers)

➤ Token Management
access_token is used to send messages

When expired, backend uses refresh_token to get a new token

Automatically refreshed before use via middleware or scheduled job

➤ Message Handling
Messages can be sent immediately or scheduled

Scheduled messages stored in DB with time

node-cron runs every minute to check and send due messages

➤ Cancel Scheduled Message
Users can see a list of scheduled messages

Option to cancel (which deletes from DB)

📸 UI Features
✅ Connect your Slack Workspace

📋 List all channels (via API)

💬 Compose a message

🕒 Select scheduled time (via datetime input)

📅 View scheduled messages

❌ Cancel any future message

🌐 Deployment (Optional)
If you deploy:

Frontend: Vercel or Netlify

Backend: Render, Heroku, Railway

Update .env values with your deployed backend URL and Slack redirect URL

💡 Challenges & Learnings
🔄 Refresh Token Logic
Slack does not provide long-lived refresh tokens. Learned to:

Use oauth.v2.access to reauthenticate when tokens expire

Store token expiry time in DB

Auto-refresh just before expiry

⏰ Reliable Scheduling
Message scheduling with setTimeout isn't reliable for long durations.

Switched to node-cron polling every minute

Made sure to handle messages missed due to downtime

🔐 Secure Token Storage
Used DB with encryption (optional) or .env secret key

Scoped tokens to team/user

🔄 Channel Selection
Slack API returns only channels user has access to

Used conversations.list with Bearer token

✅ To-Do (For Improvement)
 Add login/session support per Slack workspace

 Use Redis or Bull for more robust job queuing

 Add email alerts/reminders


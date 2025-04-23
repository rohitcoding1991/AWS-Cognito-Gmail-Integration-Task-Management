# AWS Cognito, Gmail Integration, Task-Management

Project includes user authentication using AWS Cognito, basic CRUD operations with a PostgreSQL database through Prisma for tasks, and email retrieval via the Gmail API. A cron job is also implemented to manage daily tasks in the system.

## Features

- **User Authentication**: AWS Cognito integration for user registration and login.
- **Task Management**: Basic CRUD operations for task management using Prisma and PostgreSQL.
- **Cron Jobs**: Automated scheduled tasks to archive or clean up old tasks.
- **Gmail API Integration**: Retrieve emails from the user's Gmail account via OAuth 2.0.

## Getting Started

### Prerequisites

- Node.js v20+ and npm installed.
- PostgreSQL database set up and accessible.
- AWS account with Cognito configured.
- Google Cloud project with Gmail API enabled.

### Setup and Installation

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/rohitcoding1991/AWS-Cognito-Gmail-Integration-Task-Management.git
   cd AWS-Cognito-Gmail-Integration-Task-Management
   ```

2. **Install Dependencies:**

   ```bash
   npm install
   ```

3. **Configure Environment Variables:**

   - Rename `.env.example` to `.env`.
   - Fill in the required values for AWS Cognito, PostgreSQL, and Gmail API credentials.

   Example `.env` file:

   ```env
   COGNITO_CLIENT_ID=
   AWS_ACCESS_KEY_ID=
   AWS_SECRET_ACCESS_KEY=
   JWKS_URL=
   GOOGLE_CLIENT_ID=
   GOOGLE_CLIENT_SECRET=
   GOOGLE_REDRIECT_URI=
   DATABASE_URL=
   COGNITO_USER_POOL_ID=
   ```

4. **Run Database Migrations:**

When you do npm install, The Prisma bindings will be automatically injected in `node_modules`. `postinstall` command in the package.json is responsible for that. Set up the database schema using Prisma:

```bash
npx prisma migrate dev --name add_oauth_token_model
```

5. **Start the Server:**

   Launch the application:

   ```bash
   npm start
   ```

### Scheduled Cron Job

A daily cron job is set to run at midnight, which will archive completed tasks. You can adjust the cron job timing or behavior in the `cronJobs.js` file.

```javascript
cron.schedule("0 0 * * *", async () => {
  // Archive completed tasks
});
```

### Performance:

- Applied pagination in the gmail api to handle the large dataset without overloading the application and in the task crud apis.
- Applied cron job as an efficient solution for handling background tasks like archiving tasks or cleaning up old records.

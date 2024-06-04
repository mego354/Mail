# CS50’s Web Programming with Python and JavaScript - Project 3: Mail

## Project Overview

This project implements a single-page email client using JavaScript, HTML, and CSS. The client is designed to interact with a provided API to manage emails within a simulated inbox, sent mailbox, and archive.

## Features

### Send Mail
- Users can send an email using a form.
- The form data is sent via a POST request to `/emails`.
- After sending, the user is redirected to the "Sent" mailbox.

### Mailbox
- Users can view their Inbox, Sent mailbox, or Archive.
- Emails are fetched via GET requests to `/emails/<mailbox>`.
- Emails are displayed with the sender, subject, and timestamp.
- Unread emails are highlighted with a white background; read emails have a gray background.

### View Email
- Clicking an email opens a detailed view.
- Email details (sender, recipients, subject, timestamp, and body) are fetched via GET requests to `/emails/<email_id>`.
- The email is marked as read when viewed.
- The view includes buttons for archiving/unarchiving and replying to the email.

### Archive and Unarchive
- Users can archive/unarchive emails from the inbox.
- Archiving/unarchiving is managed via PUT requests to `/emails/<email_id>`.
- After updating, the user is redirected to the inbox.

### Reply
- Users can reply to an email using a "Reply" button.
- The reply form is pre-filled with the recipient, subject, and original email body.
- The subject is prefixed with "Re:" if not already present.

## Setup Instructions

1. **Run the Django Web Server**:
   ```bash
   python manage.py runserver
   ```
2. **Register and Login**:
   - Open the web server in your browser.
   - Register a new account using the "Register" link.
   - Login with the registered account.

3. **Navigate the Interface**:
   - Use the navigation buttons to view different mailboxes.
   - Use the "Compose" button to create and send new emails.

## API Endpoints

### GET /emails/<mailbox>
Fetch all emails in a specified mailbox (inbox, sent, or archive).

**Response Example**:
```json
[
    {
        "id": 100,
        "sender": "foo@example.com",
        "recipients": ["bar@example.com"],
        "subject": "Hello!",
        "body": "Hello, world!",
        "timestamp": "Jan 2 2020, 12:00 AM",
        "read": false,
        "archived": false
    },
    {
        "id": 95,
        "sender": "baz@example.com",
        "recipients": ["bar@example.com"],
        "subject": "Meeting Tomorrow",
        "body": "What time are we meeting?",
        "timestamp": "Jan 1 2020, 12:00 AM",
        "read": true,
        "archived": false
    }
]
```

### GET /emails/<int:email_id>
Fetch details of a specific email by its ID.

**Response Example**:
```json
{
    "id": 100,
    "sender": "foo@example.com",
    "recipients": ["bar@example.com"],
    "subject": "Hello!",
    "body": "Hello, world!",
    "timestamp": "Jan 2 2020, 12:00 AM",
    "read": false,
    "archived": false
}
```

### POST /emails
Send a new email. Requires `recipients`, `subject`, and `body`.

**Request Example**:
```json
{
    "recipients": "baz@example.com",
    "subject": "Meeting time",
    "body": "How about we meet tomorrow at 3pm?"
}
```

**Response Example**:
```json
{
    "message": "Email sent successfully."
}
```

### PUT /emails/<int:email_id>
Update an email's `read` or `archived` status.

**Request Example**:
```json
{
    "archived": true
}
```

## Implementation Details

### inbox.js
- **Event Listeners**: Added to buttons for navigating views and sending emails.
- **Functions**:
  - `compose_email()`: Shows the compose view and clears form fields.
  - `load_mailbox(mailbox)`: Fetches and displays emails for the selected mailbox.
  - `view_email(email_id)`: Fetches and displays a specific email's details.
  - `send_email()`: Sends an email and redirects to the Sent mailbox.
  - `archive_email(email_id, archive)`: Archives/unarchives an email and reloads the inbox.
  - `reply_email(email)`: Prepares the reply form with the original email's details.

### inbox.html
- **Structure**: Contains sections for viewing emails and composing new emails.
- **JavaScript Inclusion**: Includes `inbox.js` to handle all dynamic behaviors.

## Contributing

1. Fork the repository.
2. Create a new branch.
3. Make your changes.
4. Submit a pull request.

[Demo Video](https://youtu.be/sbO6f1nRymQ?si=rabUn1mMfboZnrAx)


For more details on the project specifications, visit the [CS50 Mail Project](https://cs50.harvard.edu/web/2020/projects/3/mail/).

# PythonEmailsSending
Sending Emails With Python

# SMTP Email Sender with Attachment

This Python script allows you to send emails with a CSV file attachment using the Simple Mail Transfer Protocol (SMTP). The script is designed to work with various email providers and can be configured with your SMTP server details.

## Prerequisites

- Python 3.x
- `smtplib` library (comes pre-installed with Python)
- `email` library (comes pre-installed with Python)

## Installation

No additional packages are required to be installed. Simply download or clone the repository to get started.

## Usage

1. **Clone the Repository:**
    ```bash
    git clone https://github.com/AdirMachineLearning/smtp-email-sender.git
    cd smtp-email-sender
    ```

2. **Configure SMTP Server Details:**

   Update the following variables in the script with your SMTP server details and credentials:

    ```python
    smtp_server = 'smtp.example.com'      # Your SMTP server address
    smtp_port = 25                        # SMTP port number (25 for unencrypted communication, 587 for TLS, 465 for SSL)
    smtp_user = 'your_email@example.com'  # Your email address
    smtp_password = 'your_password'       # Your email account password
    subject = 'Subject of the Email'      # Subject of the email
    body = 'This is the body of the email.'  # Body of the email
    sender_email = 'your_email@example.com'  # Sender's email address
    recipient_emails = ['recipient1@example.com', 'recipient2@example.com']  # Recipient email addresses
    attachment_path = 'path/to/your/csvfile.csv'                             # Path to the CSV file to be attached
    ```

3. **Run the Script:**

    ```bash
    python send_email.py
    ```

## Example Code

Here is the full code with comments explaining each line:

```python
import smtplib  # Import the smtplib module for sending emails using the Simple Mail Transfer Protocol (SMTP)
from email.mime.multipart import MIMEMultipart  # Import MIMEMultipart for creating a multipart email message
from email.mime.text import MIMEText  # Import MIMEText for adding text content to the email
from email.mime.base import MIMEBase  # Import MIMEBase for handling the email attachment
from email import encoders  # Import encoders for encoding the email attachment

def send_email_with_attachment(smtp_server, smtp_port, smtp_user, smtp_password, subject, body, sender_email, recipient_emails, attachment_path):
    # Define a function to send an email with a CSV file attachment

    msg = MIMEMultipart()  # Create a MIMEMultipart object to represent the email message
    msg['From'] = sender_email  # Set the sender's email address
    msg['To'] = ', '.join(recipient_emails)  # Set the recipient's email addresses, joined by commas
    msg['Subject'] = subject  # Set the subject of the email

    msg.attach(MIMEText(body, 'plain'))  # Attach the plain text body to the email

    with open(attachment_path, 'rb') as attachment:  # Open the CSV file in binary read mode
        part = MIMEBase('application', 'octet-stream')  # Create a MIMEBase object to represent the attachment
        part.set_payload(attachment.read())  # Read the content of the file and set it as the payload of the attachment
        encoders.encode_base64(part)  # Encode the attachment in base64 to ensure it can be safely sent via email
        part.add_header('Content-Disposition', f'attachment; filename={attachment_path}')  # Add a header to specify the attachment's filename
        msg.attach(part)  # Attach the file to the email message

    try:
        with smtplib.SMTP(smtp_server, smtp_port) as server:  # Connect to the SMTP server using the specified server and port
            if smtp_port == 587:  # Check if the port is 587, which is used for encrypted communication
                server.starttls()  # Start TLS encryption for a secure connection
            server.login(smtp_user, smtp_password)  # Log in to the SMTP server using the provided username and password
            server.sendmail(sender_email, recipient_emails, msg.as_string())  # Send the email with the attachment
            print("Email sent successfully")  # Print a success message if the email is sent
    except Exception as e:  # Catch any exceptions that occur during the process
        print(f"Failed to send email: {e}")  # Print an error message if the email fails to send

# Example usage
smtp_server = 'smtp.example.com'                 # Define the SMTP server address
smtp_port = 25                                   # Define the SMTP port number (25 for unencrypted communication)
smtp_user = 'your_email@example.com'             # Define the SMTP username (your email address)
smtp_password = 'your_password'                  # Define the SMTP password (your email account password)
subject = 'Subject of the Email'                 # Define the subject of the email
body = 'This is the body of the email.'          # Define the body of the email
sender_email = 'your_email@example.com'          # Define the sender's email address
recipient_emails = ['recipient1@example.com', 'recipient2@example.com']  # Define the recipient email addresses
attachment_path = 'path/to/your/csvfile.csv'     # Define the path to the CSV file to be attached

send_email_with_attachment(smtp_server, smtp_port, smtp_user, smtp_password, subject, body, sender_email, recipient_emails, attachment_path)  # Call the function to send the email with the attachment


## Common Email Providers

- **Gmail**:
  - SMTP server: `smtp.gmail.com`
  - Port: 587 (with TLS) or 465 (with SSL)
  - Requires SSL: Yes
  - Requires TLS: Yes (if available)
  - Requires Authentication: Yes
  - Username: Your Gmail address (e.g., `your_email@gmail.com`)
  - Password: Your Gmail password (or app-specific password if 2-step verification is enabled)

- **Outlook/Hotmail**:
  - SMTP server: `smtp-mail.outlook.com`
  - Port: 587 (with TLS)
  - Requires SSL: Yes
  - Requires TLS: Yes (if available)
  - Requires Authentication: Yes
  - Username: Your Outlook/Hotmail address (e.g., `your_email@hotmail.com`)
  - Password: Your Outlook/Hotmail password

- **Yahoo Mail**:
  - SMTP server: `smtp.mail.yahoo.com`
  - Port: 587 (with TLS) or 465 (with SSL)
  - Requires SSL: Yes
  - Requires TLS: Yes (if available)
  - Requires Authentication: Yes
  - Username: Your Yahoo Mail address (e.g., `your_email@yahoo.com`)
  - Password: Your Yahoo Mail password

- **Office 365**:
  - SMTP server: `smtp.office365.com`
  - Port: 587 (with TLS)
  - Requires SSL: Yes
  - Requires TLS: Yes (if available)
  - Requires Authentication: Yes
  - Username: Your Office 365 address (e.g., `your_email@yourdomain.com`)
  - Password: Your Office 365 password

- **iCloud**:
  - SMTP server: `smtp.mail.me.com`
  - Port: 587 (with TLS) or 465 (with SSL)
  - Requires SSL: Yes
  - Requires TLS: Yes (if available)
  - Requires Authentication: Yes
  - Username: Your iCloud email address (e.g., `your_email@me.com`)
  - Password: Your iCloud email password

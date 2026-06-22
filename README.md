# Email JSON

A lightweight, single-file JSON-based email storage and management system designed for simple email configuration, contact information storage, and email-based identification.

## Overview

Email JSON provides:
- Simple JSON-based email storage
- Contact information management
- Email-based identification system
- Lightweight configuration file
- Easy integration with applications
- Quick email lookups
- User identification

## Features

- **Minimal Design**: Simple, single-file structure
- **JSON Format**: Language-agnostic data format
- **Fast Access**: Quick email lookups
- **Easy Integration**: Simple to embed in any application
- **No Dependencies**: Pure JSON, no external libraries required
- **Version Control**: Track changes via Git
- **Flexible Structure**: Extensible for additional fields

## Tech Stack

- **Data Format**: JSON (JavaScript Object Notation)
- **Storage**: File-based
- **Compatibility**: Any programming language
- **Version Control**: Git

## Project Structure

```
email-json/
├── email.json            # Email storage file
├── README.md            # This file
└── .github/             # GitHub configuration
```

## Email JSON Schema

### Basic Structure

```json
{
  "email": "24f3004981@ds.study.iitm.ac.in"
}
```

### Extended Structure (Optional)

```json
{
  "email": "24f3004981@ds.study.iitm.ac.in",
  "name": "User Name",
  "verified": true,
  "primary": true,
  "created_at": "2026-01-30T10:00:00Z"
}
```

## Current Email

**Email**: `24f3004981@ds.study.iitm.ac.in`

This appears to be an IITM (Indian Institute of Technology Madras) student email address.

## Installation & Usage

### Direct Usage

1. Clone the repository:
```bash
git clone https://github.com/DS24F3004981/email-json.git
cd email-json
```

2. Access the email data:

**JavaScript/Node.js**:
```javascript
const emailData = require('./email.json');
console.log(emailData.email);
// Output: 24f3004981@ds.study.iitm.ac.in
```

**Python**:
```python
import json

with open('email.json', 'r') as f:
    email_data = json.load(f)
    print(email_data['email'])
    # Output: 24f3004981@ds.study.iitm.ac.in
```

**cURL**:
```bash
curl -s https://raw.githubusercontent.com/DS24F3004981/email-json/main/email.json | jq '.email'
```

**Bash**:
```bash
cat email.json | grep -o '"email":"[^"]*"' | cut -d'"' -f4
```

## Use Cases

### 1. User Identification

```javascript
const fs = require('fs');
const emailConfig = JSON.parse(fs.readFileSync('email.json'));

function identifyUser() {
  return emailConfig.email;
}

console.log(`User: ${identifyUser()}`);
```

### 2. Contact Information Storage

Store user contact details:

```json
{
  "email": "24f3004981@ds.study.iitm.ac.in",
  "name": "Student Name",
  "phone": "+91-XXXXXXXXXX",
  "institution": "IIT Madras",
  "department": "Data Science"
}
```

Access in application:

```python
import json

with open('email.json') as f:
    contact = json.load(f)

print(f"Name: {contact.get('name')}")
print(f"Email: {contact['email']}")
print(f"Institution: {contact.get('institution')}")
```

### 3. Configuration File

Use as application configuration:

```javascript
// config.js
const emailConfig = require('./email.json');

module.exports = {
  adminEmail: emailConfig.email,
  supportEmail: emailConfig.email,
  notificationEmail: emailConfig.email
};
```

### 4. Email Verification

```python
import json
import re

def load_email_config():
    with open('email.json') as f:
        return json.load(f)

def validate_email(email):
    pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
    return re.match(pattern, email) is not None

config = load_email_config()
if validate_email(config['email']):
    print(f"✓ Valid email: {config['email']}")
else:
    print("✗ Invalid email format")
```

### 5. Multi-User System

Extend for multiple email addresses:

```json
{
  "users": [
    {
      "id": 1,
      "email": "24f3004981@ds.study.iitm.ac.in",
      "role": "student"
    },
    {
      "id": 2,
      "email": "instructor@iitm.ac.in",
      "role": "instructor"
    }
  ]
}
```

Access users:

```python
import json

with open('email.json') as f:
    data = json.load(f)

for user in data['users']:
    print(f"{user['role']}: {user['email']}")
```

## API Integration

### Send Email via API

```python
import json
import smtplib

def get_recipient_email():
    with open('email.json') as f:
        return json.load(f)['email']

def send_email(subject, body):
    recipient = get_recipient_email()
    
    # Email sending logic
    print(f"Sending email to {recipient}")
```

### Notification System

```javascript
const emailConfig = require('./email.json');

class NotificationService {
  constructor() {
    this.recipientEmail = emailConfig.email;
  }
  
  async sendNotification(message) {
    console.log(`Sending to ${this.recipientEmail}: ${message}`);
    // Implementation
  }
}
```

## Email Domain Information

**Domain**: `ds.study.iitm.ac.in`

- **Institution**: IIT Madras (Indian Institute of Technology Madras)
- **Type**: Educational Institution
- **Email Format**: Student email with enrollment number
- **Format**: `{enrollment_number}@ds.study.iitm.ac.in`

### IITM Email Benefits

- Academic email address for institutional purposes
- Access to educational resources and platforms
- Professional communication channel
- Alumni network connectivity
- Research collaboration opportunities

## Working with Email Data

### Parse Email Components

```python
import json

def parse_email(email_string):
    """Parse email into local and domain parts"""
    local, domain = email_string.split('@')
    return {
        'local_part': local,
        'domain': domain,
        'institution': domain.split('.')[-2:][0] if '.' in domain else None
    }

with open('email.json') as f:
    email = json.load(f)['email']
    parts = parse_email(email)
    print(f"User ID: {parts['local_part']}")
    print(f"Domain: {parts['domain']}")
```

### Validate Email Format

```python
import json
import re

def is_valid_iitm_email(email):
    """Check if email is valid IITM student email"""
    pattern = r'^\d+@ds\.study\.iitm\.ac\.in$'
    return bool(re.match(pattern, email))

with open('email.json') as f:
    email = json.load(f)['email']
    
if is_valid_iitm_email(email):
    print("✓ Valid IITM student email")
else:
    print("✗ Invalid IITM student email")
```

### Extract User Identifier

```python
import json

def get_user_id():
    """Extract user ID from IITM email"""
    with open('email.json') as f:
        email = json.load(f)['email']
    return email.split('@')[0]

user_id = get_user_id()
print(f"User ID: {user_id}")  # Output: 24f3004981
```

## Integration Examples

### Express.js Application

```javascript
const express = require('express');
const emailConfig = require('./email.json');
const app = express();

app.get('/api/contact', (req, res) => {
  res.json(emailConfig);
});

app.get('/api/email', (req, res) => {
  res.json({ email: emailConfig.email });
});

app.listen(3000);
```

### Flask Application

```python
from flask import Flask, jsonify
import json

app = Flask(__name__)

with open('email.json') as f:
    email_config = json.load(f)

@app.route('/api/contact')
def get_contact():
    return jsonify(email_config)

@app.route('/api/email')
def get_email():
    return jsonify({'email': email_config['email']})

if __name__ == '__main__':
    app.run()
```

### HTML Form Population

```html
<form id="contactForm">
  <input type="email" id="emailField" name="email" />
</form>

<script>
  fetch('./email.json')
    .then(response => response.json())
    .then(data => {
      document.getElementById('emailField').value = data.email;
    });
</script>
```

### Mobile App Integration

```javascript
// React Native
import React, { useState, useEffect } from 'react';
import { Text, View } from 'react-native';

export default function App() {
  const [email, setEmail] = useState('');
  
  useEffect(() => {
    fetch('./email.json')
      .then(res => res.json())
      .then(data => setEmail(data.email));
  }, []);
  
  return (
    <View>
      <Text>Email: {email}</Text>
    </View>
  );
}
```

## Data Management

### Update Email Address

```python
import json

def update_email(new_email):
    """Update email in JSON file"""
    with open('email.json', 'r+') as f:
        data = json.load(f)
        data['email'] = new_email
        f.seek(0)
        json.dump(data, f, indent=2)
        f.truncate()

# Usage
update_email("new.email@ds.study.iitm.ac.in")
```

### Add Metadata

```python
import json
from datetime import datetime

def add_metadata():
    """Add timestamps and metadata to email"""
    with open('email.json', 'r+') as f:
        data = json.load(f)
        data['created_at'] = datetime.now().isoformat()
        data['updated_at'] = datetime.now().isoformat()
        data['verified'] = True
        f.seek(0)
        json.dump(data, f, indent=2)
        f.truncate()

add_metadata()
```

## Best Practices

1. **Keep it Simple**: Don't over-complicate the schema
2. **Validate Email**: Validate email format before storing
3. **Secure**: Don't commit sensitive email addresses
4. **Backup**: Maintain backups of email data
5. **Version Control**: Track changes via Git
6. **Documentation**: Document any custom fields
7. **Privacy**: Handle email data according to privacy laws

## Security Considerations

### Protect Email Privacy

```bash
# Add to .gitignore if containing sensitive data
echo "email.json" >> .gitignore
```

### Encrypt Sensitive Data

```python
from cryptography.fernet import Fernet
import json

def encrypt_email(email):
    """Encrypt email address"""
    key = Fernet.generate_key()
    cipher = Fernet(key)
    return cipher.encrypt(email.encode())

def decrypt_email(encrypted_email, key):
    """Decrypt email address"""
    cipher = Fernet(key)
    return cipher.decrypt(encrypted_email).decode()
```

## Validation & Testing

### Validate JSON Structure

```bash
# Using jq
jq empty email.json

# Using Python
python -m json.tool email.json > /dev/null
```

### Unit Tests

```python
import json
import unittest

class TestEmailJSON(unittest.TestCase):
    def setUp(self):
        with open('email.json') as f:
            self.email_data = json.load(f)
    
    def test_email_exists(self):
        self.assertIn('email', self.email_data)
    
    def test_email_format(self):
        email = self.email_data['email']
        self.assertIn('@', email)
        self.assertIn('.', email)
    
    def test_valid_iitm_email(self):
        email = self.email_data['email']
        self.assertTrue(email.endswith('ds.study.iitm.ac.in'))

if __name__ == '__main__':
    unittest.main()
```

## Troubleshooting

### JSON Parse Error

```
Error: Unexpected character in JSON
```

Validate JSON syntax:
```bash
python -m json.tool email.json
```

### File Not Found

```
Error: File not found: email.json
```

Ensure file exists in correct directory:
```bash
ls -la email.json
```

### Permission Denied

```bash
chmod 644 email.json
```

## Contributing

1. Fork the repository
2. Update email.json if needed
3. Validate JSON format
4. Commit with clear messages
5. Push and create a pull request

## License

This project is open source and available under the MIT License.

## Author

Created by DS24F3004981

## Resources

- [JSON Format](https://www.json.org/)
- [Email Format Standards](https://tools.ietf.org/html/rfc5321)
- [IIT Madras](https://www.iitm.ac.in/)

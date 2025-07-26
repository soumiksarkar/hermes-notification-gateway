# Hermes - A Decentralized Notification Gateway (MVP)

[![Go Version](https://img.shields.io/badge/Go-1.20+-blue.svg)](https://golang.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Status: MVP](https://img.shields.io/badge/Status-MVP-orange.svg)](https://github.com/soumiksarkar/hermes-notification-gateway)

## 🚀 Vision

Hermes aims to be a **self-hostable**, **open-source**, and **decentralized notification gateway**. Instead of relying on centralized third-party services, Hermes empowers users to unify and manage various notification providers (like email, SMS, push notifications, and potentially decentralized messaging protocols) through a single Go-based backend, offering greater control and privacy.

## 📋 Current Status: Minimal Viable Product (MVP)

This repository contains the very first, foundational version of Hermes. The primary goal of this MVP is to establish the basic architecture and demonstrate the core capability of sending notifications through a self-hosted gateway.

## ✨ Key Features (MVP)

- **📧 Email Notification via SMTP**: Send emails using your own SMTP server credentials
- **🌐 Simple REST API**: A basic HTTP endpoint for external applications to trigger email notifications
- **⚙️ Configuration via Environment Variables**: Easy setup using standard environment variables

## 🚀 Getting Started

### Prerequisites

- **Go**: Ensure you have Go installed (version 1.20 or newer is recommended)
- **SMTP Server Access**: You'll need credentials for an SMTP server (e.g., Gmail SMTP, your own mail server, etc.) to send emails

### 1. Clone the Repository

```bash
git clone https://github.com/soumiksarkar/hermes-notification-gateway.git
cd hermes-notification-gateway
```

### 2. Configuration

Hermes uses environment variables for configuration. Set the following variables based on your SMTP server details:

```bash
export SMTP_HOST="your.smtp.server.com"      # e.g., smtp.gmail.com
export SMTP_PORT="587"                       # e.g., 587 or 465 (for SSL/TLS)
export SMTP_USERNAME="your-email@example.com"
export SMTP_PASSWORD="your-email-password"   # Or an app-specific password if using Gmail
export SMTP_FROM_ADDRESS="your-email@example.com" # The 'From' address for sent emails
export API_PORT="8080"                       # Port for the Hermes API server
```

> **⚠️ Important Security Note**: Storing passwords directly in environment variables is okay for development, but for production environments, consider more secure options like Go's flag package with secure prompting, a dedicated secrets management solution, or a `.env` file that is not committed to version control.

### 3. Run the Application

```bash
go run main.go
```

You should see output indicating that the Hermes API server is starting:

```
Hermes API server starting on :8080...
```

## 🔌 API Endpoints (MVP)

The current MVP exposes a single API endpoint for sending emails.

### Send Email Notification

Sends an email through the configured SMTP server.

- **URL**: `/send-email`
- **Method**: `POST`
- **Content-Type**: `application/json`

#### Request Body Example

```json
{
  "to": "recipient@example.com",
  "subject": "Hello from Hermes MVP!",
  "body": "This is a test notification sent via the Hermes decentralized gateway.",
  "html": "<p>This is a <strong>HTML test</strong> notification sent via the Hermes decentralized gateway.</p>"
}
```

#### Parameters

- `to` (string, required): The recipient's email address
- `subject` (string, required): The subject line of the email
- `body` (string, optional): The plain text content of the email
- `html` (string, optional): The HTML content of the email. If both `body` and `html` are provided, `html` will take precedence for email clients that support HTML

#### Success Response

**Code**: `200 OK`

**Body**:
```json
{
  "message": "Email sent successfully!"
}
```

#### Error Responses

**Code**: `400 Bad Request`

**Body**: `{ "error": "Invalid request payload" }` (e.g., missing 'to' or 'subject')

**Code**: `500 Internal Server Error`

**Body**: `{ "error": "Failed to send email: [specific error message]" }` (e.g., SMTP connection issue, authentication failure)

## 🗺️ Roadmap & Future Plans

This is just the beginning! Future enhancements for Hermes include:

- **📱 Support for More Providers**: Integration with other notification channels (e.g., in-app notifications, specific decentralized messaging protocols like Matrix or XMPP)
- **🎯 Rule-Based Routing**: Allow users to define complex rules for how notifications are delivered based on content, priority, recipient, etc.
- **🖥️ Basic Management UI**: A simple web interface for configuring providers and routing rules
- **📊 Notification Logging & History**: Store and view past notifications
- **🔄 Advanced Error Handling & Retries**: Robust mechanisms for handling failed deliveries

## 👋 Contributing

We welcome contributions from the community! If you're interested in helping to build a truly decentralized notification gateway, please check out our (future) `CONTRIBUTING.md` for guidelines. For now, feel free to:

- Open issues
- Submit pull requests
- Discuss ideas

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Built with ❤️ for a more decentralized future**

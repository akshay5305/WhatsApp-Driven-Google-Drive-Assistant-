
# WhatsApp-Driven Google Drive Assistant (n8n Workflow)

> **📹 Demo Video:**
( )
> A complete exhibition screen recording demonstrating the workflow functionality will be placed here once the WhatsApp integration is complete.

## Overview

This project implements an intelligent Google Drive file management system using n8n automation workflows. The system automatically processes files uploaded to Google Drive by categorizing them using AI, organizing them into appropriate folders, renaming them with standardized conventions, and maintaining comprehensive audit logs.

## Current Implementation Status

### ✅ Completed Features

1. **Automated File Detection & Processing**
   - Google Drive trigger monitors root folder for new file uploads
   - Supports multiple file types: Google Docs, Sheets, Slides, and PDFs
   - Real-time file processing with configurable polling intervals

2. **AI-Powered File Classification**
   - OpenAI GPT-4.1-mini integration for intelligent content analysis
   - Automatic categorization into 8 predefined business categories:
     - 📊 Accounting (Financial statements, receipts, bookkeeping)
     - 👥 Recruitment (Resumes, job descriptions, interview notes)
     - 💰 Sales (Pipelines, contracts, revenue tracking)
     - 📈 Marketing (Campaigns, analytics, content calendars)
     - 🏢 Consulting (Client deliverables, project tracking)
     - 📋 Incorporation (Legal docs, filings, agreements)
     - 👤 Personal (Non-business files, personal notes)
     - 📂 Miscellaneous (Uncategorized content)

3. **Smart File Organization**
   - Automatic file conversion to PDF format for standardization
   - Content extraction and analysis (first 5000 characters)
   - Intelligent folder assignment based on content classification
   - Standardized file renaming: `[Description] – [MM/DD/YYYY]` format

4. **Comprehensive Audit Logging**
   - Google Sheets integration for tracking all file operations
   - Logs include: timestamp, file name, location, file type, approval status
   - Direct links to files and destination folders for easy access
   - File type detection and categorization

5. **Advanced File Processing**
   - Google Drive OAuth2 authentication
   - File download and content extraction capabilities
   - MIME-type aware processing for different document types
   - Error handling and data validation

### 🚧 In Progress

- **WhatsApp Integration**: Currently developing the WhatsApp listener component using Twilio Sandbox API for command-based file operations

### 📋 Planned WhatsApp Commands

Once the WhatsApp integration is complete, the following commands will be supported:

```
LIST /FolderName          - List files in specified folder
DELETE /Path/filename.pdf - Delete specific file (with confirmation)
MOVE /Source/file /Dest   - Move file between folders  
SUMMARY /FolderName       - AI-generated summary of folder contents
HELP                      - Display available commands
```

## Technical Architecture

### Workflow Components

1. **Google Drive Trigger** - Monitors root folder for new files
2. **File Type Filter** - Validates supported file formats
3. **Content Processor** - Downloads and extracts file content
4. **AI Classifier** - Categorizes content using OpenAI API
5. **File Organizer** - Moves files to appropriate folders
6. **Audit Logger** - Records all operations in Google Sheets

### Technology Stack

- **Automation Platform**: n8n (Node-based workflow automation)
- **Cloud Storage**: Google Drive API v3
- **AI Service**: OpenAI GPT-4.1-mini
- **Authentication**: OAuth2 for Google services
- **Logging**: Google Sheets API
- **File Processing**: Built-in n8n file handling nodes

## Setup Instructions

### Prerequisites

- n8n instance (Docker or cloud deployment)
- Google Cloud Project with Drive & Sheets API enabled
- OpenAI API account with GPT-4 access
- Twilio account for WhatsApp integration (upcoming)

### Environment Configuration

Create a `.env` file with the following variables:

```env
# Google OAuth2 Credentials
GOOGLE_CLIENT_ID=your_client_id
GOOGLE_CLIENT_SECRET=your_client_secret
GOOGLE_REFRESH_TOKEN=your_refresh_token

# OpenAI Configuration
OPENAI_API_KEY=your_openai_api_key

# Twilio WhatsApp (Coming Soon)
TWILIO_ACCOUNT_SID=your_account_sid
TWILIO_AUTH_TOKEN=your_auth_token
TWILIO_WHATSAPP_NUMBER=your_whatsapp_number

# Google Drive Folder IDs
ACCOUNTING_FOLDER_ID=1e9ety6wdCzwXhjbh2sAPIIhrxI3WNGT4
RECRUITMENT_FOLDER_ID=1okbwxsrJb2LVKD1dfG_FXxkLulMeLUFu
SALES_FOLDER_ID=1UKb5H8mcS8YTWQIwPmUV_GgQI7pPXGvW
MARKETING_FOLDER_ID=1bZQp61Zfm5NXAcsaTZgR4sTlKQLT1nPm
CONSULTING_FOLDER_ID=1wfuNlDtlUUxJIUbaXtZWJdnIRzdxBb8B
INCORPORATION_FOLDER_ID=1jatzsie7Y6wbpxDx0s1JM03R1p8mbPeU
PERSONAL_FOLDER_ID=11zYE5sKrcoJbuwcB2fYslK-DSlKMqEg1
MISCELLANEOUS_FOLDER_ID=18xg3NOiazeBssQPDokDz4DQl4hWl3iYg

# Audit Logging
AUDIT_SPREADSHEET_ID=1mCY_UFOQ_4sZ-t5ZCqXUwL1a-4B-AK8jiSnxcA5-EXE
```

### Installation Steps

1. **Clone Repository**
   ```bash
   git clone https://github.com/yourusername/whatsapp-drive-assistant
   cd whatsapp-drive-assistant
   ```

2. **Setup n8n with Docker**
   ```bash
   docker run -it --rm \
     --name n8n \
     -p 5678:5678 \
     -v ~/.n8n:/home/node/.n8n \
     n8nio/n8n
   ```

3. **Import Workflow**
   - Access n8n at `http://localhost:5678`
   - Go to Workflows → Import from File
   - Select `My workflow.json` from this repository

4. **Configure Credentials**
   - Google Drive OAuth2 API
   - OpenAI API
   - Google Sheets OAuth2 API

5. **Activate Workflow**
   - Enable the workflow in n8n interface
   - Test with sample file upload to Google Drive

## File Classification Logic

The AI classifier analyzes file content and applies these categorization rules:

- **Accounting**: Financial keywords, numbers, monetary values
- **Recruitment**: Resume indicators, job-related terms
- **Sales**: Pipeline terms, revenue data, client information
- **Marketing**: Campaign metrics, promotional content
- **Consulting**: Client references, project deliverables
- **Incorporation**: Legal terminology, corporate documents
- **Personal**: Non-business indicators, personal references
- **Miscellaneous**: Default fallback category

## Security Features

- OAuth2 authentication for all Google services
- Secure credential storage in n8n
- Audit trail for all file operations
- Confirmation required for destructive operations
- Scoped API access (read/write only to specified folders)

## Error Handling

- File type validation before processing
- API rate limit management
- Fallback categorization for unclear content
- Comprehensive logging of all operations and errors
- Graceful handling of API failures

## Contributing

This project is part of an internship application. Future enhancements may include:

- Natural language command processing
- Advanced file search capabilities
- Integration with additional cloud storage providers
- Mobile app interface
- Advanced AI summarization features

## Roadmap

- [x] Core file organization workflow
- [x] AI-powered classification
- [x] Audit logging system
- [ ] WhatsApp integration (In Progress)
- [ ] Command validation and security
- [ ] Natural language processing
- [ ] Advanced error recovery
- [ ] Performance optimization

## License

MIT License - See LICENSE file for details

---

**Current Workflow Name**: `My workflow` (File organization and AI classification system)

> **Note**: The WhatsApp listening component is currently under development and will be updated ASAP. The core file organization system is fully functional and ready for production use.

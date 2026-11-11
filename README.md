# Automated Invoice Processing with n8n | ConvergLeads

An automated invoice processing workflow built with n8n, designed to receive invoices, identify file formats, extract invoice information, validate data, request human approval, and simulate invoice submission to SAP.

## 🚀 Overview

Invoice processing is an essential but often repetitive business activity.

Employees frequently spend time receiving invoices, opening documents, extracting information, checking amounts, and entering data into business systems.

This project demonstrates how workflow automation can simplify and improve this process.

With **ConvergLeads**, we designed an n8n workflow that automates several stages of invoice processing while keeping human approval as an important control point before the SAP submission stage.

The solution supports multiple invoice file formats, including:

- PDF
- XLSX
- XLS
- CSV

## 🎥 Project Demonstration

Watch the complete workflow demonstration:

- 🇬🇧 [English Demo](demo/invoice-automation-demo-en.mp4)
- 🇩🇪 [German Demo](demo/invoice-automation-demo-de.mp4)

## 🏗️ Workflow Architecture



### Automation Flow

Receive Invoice File
↓
Identify File Type
↓
Route by File Type
↓
Extract PDF / XLSX / XLS / CSV
↓
Normalize Invoice Fields
↓
Validate Invoice
↓
Prepare Excel Row
↓
Create Excel Review
↓
Human Approval
↓
Approval Decision
↓
SAP Sandbox Simulation

## ⚙️ How the Workflow Works

### 1. Receive Invoice File

The process starts when an invoice file is received through an n8n Webhook.

During development and testing, PowerShell is used to send the invoice file to the local webhook endpoint.

The workflow receives the uploaded file and starts the automation process.

### 2. Identify File Type

The workflow automatically identifies the format of the incoming file.

It determines whether the document is a PDF, XLSX, XLS, or CSV file.

This step is important because different file formats require different extraction methods.

### 3. Route by File Type

After identifying the file format, the workflow routes the document to the corresponding processing branch.

Each supported file type follows its own extraction path.

This makes the workflow flexible and easier to extend.

### 4. Extract Invoice Data

The workflow uses dedicated extraction steps for the different file formats.

The objective is to retrieve the available invoice information from each document.

The extracted information can include:

- Supplier name
- Invoice number
- Invoice date
- Net amount
- VAT amount
- Gross amount

### 5. Normalize Invoice Fields

Invoices may contain different labels and data structures.

For example, one supplier may use "Invoice Number", while another uses "Rechnungsnummer".

The normalization step converts the extracted information into a consistent structure.

This allows the following workflow steps to process the invoice data in a standardized way.

### 6. Validate Invoice

Before continuing, the workflow checks the extracted invoice information.

The validation process checks whether important fields are available.

It also compares the financial amounts.

For example:

Net Amount + VAT Amount = Gross Amount

The workflow can identify missing information or differences between the invoice totals.

This helps detect potential errors before human approval.

### 7. Prepare Excel Row

The extracted and validated invoice information is organized into a structured data row.

This prepares the information for the next processing steps and makes it easier to review.

### 8. Create Excel Review

The workflow creates an Excel review file containing the invoice information.

This provides a structured overview of the extracted data and supports the human review process.

### 9. Human Approval – Wait

Human approval is an important part of the workflow.

After preparing the invoice information, the workflow waits for an employee to review the data.

The employee can inspect the invoice details and make a decision.

The workflow does not continue until the approval decision is submitted.

### 10. Approval Decision – IF

The IF node checks the employee's decision.

There are two possible outcomes:

**APPROVE**

If the invoice is approved, the workflow continues to the SAP submission step.

**REJECT**

If the invoice is rejected, it is not forwarded to the SAP submission step.

This ensures that the approval decision controls the next action.

### 11. SAP Sandbox Integration

After approval, the invoice information is sent to a separate SAP sandbox workflow through an HTTP request.

The sandbox receives the invoice information and simulates the acceptance and recording process.

**Important:** This demonstration currently uses a simulation environment. It does not perform a real posting in a company's production SAP system.

A production SAP integration would require authorized SAP access, suitable APIs, credentials, and company approval.

## 🛠️ Technologies Used

- **n8n:** Workflow automation and orchestration
- **PowerShell:** Sending test invoice files during development
- **Webhooks:** Receiving invoice files and communicating between workflows
- **JavaScript:** Data processing, normalization, and validation
- **PDF / Excel / CSV:** Supported invoice document formats
- **HTTP Request:** Communication with the SAP sandbox workflow
- **SAP Sandbox:** Simulated invoice submission and acceptance

## 🎯 Business Value

This project demonstrates how automation can support accounts payable and invoice processing activities.

Potential benefits include:

- Reduced manual data entry
- Faster invoice processing
- Consistent invoice data structures
- Early identification of missing or inconsistent information
- Human control before submission
- Improved process transparency
- A foundation for future SAP integration

## 💼 Use Cases

This workflow can be adapted for:

- Accounts payable departments
- Finance and accounting teams
- Small and medium-sized businesses
- Companies processing large numbers of invoices
- Administrative departments
- Automation and digital transformation projects

## 🔐 Security and Project Availability

This repository presents the project architecture and its main processing steps.

The complete production workflow JSON, API credentials, access tokens, passwords, and sensitive configuration details are not publicly distributed.

The demonstration uses fictitious invoice data.

## 📊 Project Status

- ✅ Invoice intake through n8n Webhook
- ✅ Automatic file type identification
- ✅ PDF extraction branch
- ✅ XLSX extraction branch
- ✅ XLS extraction branch
- ✅ CSV extraction branch
- ✅ Invoice field normalization
- ✅ Invoice data validation
- ✅ Excel review preparation
- ✅ Human approval process
- ✅ Approval and rejection routing
- ✅ HTTP communication with SAP sandbox
- ✅ SAP submission simulation tested

## 🚀 Future Improvements

Potential future development includes:

- Real SAP integration using authorized SAP APIs
- Advanced invoice extraction using OCR and AI
- Duplicate invoice detection
- Additional document format support
- Error handling and automated notifications
- Invoice archiving and audit logging
- Role-based approval processes

## 👩‍💻 Author

**Esther Madianga**

Freelance Automation Specialist | n8n & AI Automation

**ConvergLeads – AI Automation. One Platform. Endless Possibilities.**

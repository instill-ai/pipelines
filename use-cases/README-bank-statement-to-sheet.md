# Bank Statement to Google Sheets Pipeline

## Overview

The Bank Statement to Google Sheets pipeline is a sophisticated data extraction and automation tool that processes individual bank statements and automatically writes structured financial data to Google Sheets. This pipeline transforms raw bank statement documents into organized, analyzable data that can be used for financial tracking, reporting, and analysis.

### 📊 **Structured Data Extraction**

- **Transaction Details**: Complete lists of debit and credit transactions with dates and descriptions
- **Account Information**: Bank name, currency, and statement period details

### 🔢 **Automated Calculations**

- **Transaction Totals**: Automatic calculation of total debits and credits
- **Average Metrics**: Monthly averages for debits, credits, and bank balances
- **Transaction Counts**: Number of debit and credit transactions
- **Financial Summaries**: Comprehensive financial metrics for analysis

- **Direct Writing**: Automatically writes data to specified Google Sheets
- **Column Mapping**: Maps extracted data to specific sheet columns
- **Row Addition**: Adds new rows for each processed statement
- **Structured Format**: Maintains consistent data structure across entries

### 🛡️ **Data Quality & Security**

- **Format Compliance**: Ensures proper date formats and currency codes
- **Null Handling**: Gracefully handles missing information

## Input Variables

### `sheet-shared-link`

- **Type**: `string`
- **Description**: The shared link to the Google Sheets document where data will be written
- **Required**: Yes
- **Format**: Google Sheets sharing URL (e.g., https://docs.google.com/spreadsheets/d/...)

### `sheet-name`

- **Type**: `string`
- **Description**: The name of the specific sheet/tab in the Google Sheets document
- **Required**: Yes
- **Format**: Exact sheet name as it appears in the Google Sheets document

### `bank-statement`

- **Type**: `file`
- **Description**: Upload a single bank statement PDF to extract structured financial data
- **Required**: Yes
- **Format**: Supports document formats such as monthly bank statement PDF

## Processing Steps

### 1. **Document Conversion**

- **Task**: `TASK_CONVERT_TO_MARKDOWN`
- **Output**: Extracted text content from the bank statement document
- **Purpose**: Prepares the document for AI analysis and data extraction

### 2. **AI-Powered Data Extraction**

- **Model**: OpenAI GPT-4o
- **Task**: `TASK_TEXT_GENERATION`
- **Extraction Fields**:
  - **Month**: Statement period in mmm-yyyy format
  - **Month End Balance**: Closing balance for the statement period
  - **Bank**: Name of the financial institution
  - **Currency**: ISO 4217 currency code (USD, EUR, GBP, etc.)
  - **Debit Transactions**: Array of all withdrawal transactions
  - **Credit Transactions**: Array of all deposit transactions
- **Note**: Daily End Balances are calculated separately in step 4 for better accuracy

### 3. **JSON Processing & Validation**

- **Task**: `TASK_UNMARSHAL`
- **Purpose**: Converts AI response to structured JSON data
- **Validation**: Ensures data format compliance and completeness

### 4. **Daily Balance Calculation (Reasoning)**

- **Model**: OpenAI GPT-4o
- **Task**: `TASK_TEXT_GENERATION`
- **Purpose**: Calculates daily end balances using step-by-step reasoning
- **Algorithm**:
  - Works backward from known transaction balances
  - Handles sparse transactions and multiple transactions per day
  - Fills gaps between transaction dates
- **Output**: Natural language reasoning with calculated daily balances

### 5. **Daily Balance Formatting**

- **Model**: OpenAI GPT-4o
- **Task**: `TASK_TEXT_GENERATION`
- **Purpose**: Converts reasoning output to structured JSON format
- **Output**: Structured dailyEndBalances array

### 6. **Data Merging & Computed Fields Generation**

- **Task**: `TASK_JQ`
- **Purpose**: Merges daily balances with extracted data and calculates computed fields
- **Operations**:
  - Merges dailyEndBalances into the main data structure
  - Calculates number of debit and credit transactions
  - Calculates total debits and credits
  - Calculates average monthly debit and credit amounts
  - Calculates average bank balance for the period

### 7. **Column Mapping**

- **Task**: `TASK_RENAME_FIELDS`
- **Purpose**: Maps extracted data to Google Sheets column names
- **Mapping**:
  - `month` → `Month`
  - `totalDebits` → `Total Debits`
  - `totalCredits` → `Total Credits`
  - `monthEndBalance` → `Month end balance`
  - `avgMonthlyDebit` → `Avg. monthly debit`
  - `avgMonthlyCredit` → `Avg. monthly credit`
  - `avgBankBalance` → `Avg. bank balance`
  - `noOfDebitTransactions` → `No. of debit transactions`
  - `noOfCreditTransactions` → `No. of credit transactions`
  - `bank` → `Bank`
  - `fileName` → `File Name`
  - `currency` → `Currency`

### 8. **Google Sheets Integration**

- **Task**: `TASK_INSERT_ROW`
- **Connection**: Uses configured Google Sheets connection
- **Output**: Row information and write status

## Output Components

### 1. **Extracted Statement Text**

- **Title**: "Extracted Statement Text"
- **Content**: Raw text content extracted from the bank statement
- **Purpose**: Reference for verification and debugging
- **Format**: Markdown text

### 2. **Daily Balance Calculation Reasoning**

- **Title**: "Daily Balance Calculation Reasoning"
- **Content**: Step-by-step reasoning and calculations for daily balances
- **Purpose**: Debugging and verification of balance calculations
- **Format**: Natural language text with mathematical reasoning

### 3. **Merged Data JSON**

- **Title**: "Merged Data JSON"
- **Content**: Complete data with daily balances merged and computed fields added
- **Purpose**: Detailed view of all processed information
- **Format**: JSON object with all financial data and computed fields

### 4. **Sheet Data JSON**

- **Title**: "Sheet Data JSON"
- **Content**: Final data formatted for Google Sheets
- **Purpose**: Preview of data that will be written to sheets
- **Format**: JSON object with mapped column names

### 5. **Google Sheets Write Status**

- **Title**: "Google Sheets Write Row information"
- **Content**: Confirmation and details of the write operation
- **Purpose**: Verification that data was successfully written
- **Format**: Row information object

## Data Schema

### **Extracted Financial Data Structure**

```json
{
  "month": "Aug-2025",
  "monthEndBalance": 12500.5,
  "bank": "Bank of America",
  "currency": "USD",
  "listOfDebitTransactions": [
    {
      "date": "2025-08-15",
      "description": "Grocery Store Purchase",
      "amount": 85.75
    }
  ],
  "listOfCreditTransactions": [
    {
      "date": "2025-08-01",
      "description": "Salary Deposit",
      "amount": 3500.0
    }
  ],
  "dailyEndBalances": [
    {
      "date": "2025-08-01",
      "balance": 11500.0
    },
    {
      "date": "2025-08-02",
      "balance": 11500.0
    },
    ...
    {
      "date": "2025-08-31",
      "balance": 12500.5
    }
  ]
}
```

### **Computed Fields**

- **noOfDebitTransactions**: Count of debit transactions
- **noOfCreditTransactions**: Count of credit transactions
- **totalDebits**: Sum of all debit amounts
- **totalCredits**: Sum of all credit amounts
- **avgMonthlyDebit**: Average debit transaction amount
- **avgMonthlyCredit**: Average credit transaction amount
- **avgBankBalance**: Average daily balance for the period
- **fileName**: File identifier ("bs")

## Technical Requirements

### **AI Model Configuration**

- **Model**: OpenAI GPT-4o
- **Temperature**: 0.1 (ensures high deterministic output)
- **Top p**: 0.1 (ensures high deterministic output)
- **System Message**: Financial data extraction specialist role
- **Response Format**: Strict JSON schema validation for extraction, natural language for reasoning

### **Daily Balance Calculation Algorithm**

The pipeline uses a sophisticated backward calculation algorithm:

1. **Identify Known Balances**: Find all transaction dates with their resulting balances
2. **Sort Transactions**: Sort by date (earliest to latest)
3. **Work Backward**: For each transaction, calculate balance BEFORE the transaction:
   - DEBIT: Balance_before = Balance_after + Amount
   - CREDIT: Balance_before = Balance_after - Amount
4. **Fill Gaps**: Use the most recent calculated balance for days between transactions
5. **Handle Multiple Transactions**: Process all transactions on the same day chronologically

This approach ensures accurate daily balance calculations even with sparse transaction patterns.

### **Google Sheets Integration**

- **Authentication**: OAuth2 connection required
- **Column Mapping**: Automatic field-to-column mapping
- **Row Insertion**: Adds new rows without overwriting existing data

## Basic Usage

### **Step 1: Prepare Bank Statement**

- Ensure your bank statement is in a supported format (such as PDF)

### **Step 2: Prepare Google Sheets**

- Create or open a Google Sheets document
- Set up columns with the following names in order:
  - Month
  - Total Debits
  - Total Credits
  - Month end balance
  - Avg. monthly debit
  - Avg. monthly credit
  - Avg. bank balance
  - No. of debit transactions
  - No. of credit transactions
  - Bank
  - File Name
  - Currency
- Share the document and copy the sharing link
- Note the exact sheet name where data will be written

### **Step 3: Configure Pipeline**

1. Log in to the Instill AI Platform and click your profile in the bottom left to access the console

**Create a pipeline**

1. Navigate to "Pipelines" and click "+ Create Pipeline"
2. Give the pipeline a memorable name such as "bank-statement-to-sheet"
3. Copy the contents of `bank-statement-to-sheet.yaml` into the pipeline editor

**Set up Google Sheets integration**

4. Click your profile in the top right, then go to Settings > Integrations
5. Search for "Google Sheets" and click "Connect" to authorize access to your Google Sheets document
6. After successful connection, copy the connection ID (e.g., "google-sheets-...")
7. In your pipeline configuration, locate the Google Sheets connection line and replace the connection ID with the one you copied from the integrations page

### **Step 4: Run the Pipeline**

- Enter the Google Sheets sharing URL in the "Sheet Link" field
- Specify the exact sheet name (case-sensitive) in the "Sheet Name" field
- Upload your bank statement file
- Run the pipeline
- Review the pipeline outputs, especially the "Daily Balance Calculation Reasoning" for verification
- Check that the data was successfully written to Google Sheets

## Troubleshooting

Google Sheets Setup

- Create consistent column headers
- Use the exact column names expected by the pipeline

---

**Note**: This pipeline is designed for data extraction and automation only. It does not provide financial advice, investment recommendations, or tax guidance. The accuracy of extracted data depends on the quality and format of the input bank statements.

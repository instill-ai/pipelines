# Bank Account Aggregator Pipeline

## Overview

The Bank Account Aggregator is a streamlined pipeline that processes multiple bank statements and provides simple aggregated numbers and account details. This pipeline focuses on data consolidation and presentation without complex financial analysis, making it perfect for quick account overviews and financial snapshots.

## Key Features

### 🔢 **Simple Aggregation**

- **Total Balances**: Sum of all closing balances across accounts
- **Transaction Totals**: Combined deposits, withdrawals, and net changes
- **Account Summary**: Number of banks, account types, and total accounts
- **Balance Distribution**: Breakdown by account type and institution

### 📋 **Account Details Listing**

- **Clean Table Format**: Professional account summary table
- **Security Focused**: Account numbers masked (last 4 digits only)
- **Organized Data**: Sorted by bank name and account type
- **Complete Information**: All essential account details

### 🛡️ **Security & Privacy**

- **Account Masking**: Automatic masking of sensitive account numbers
- **Essential Data Only**: Extracts only necessary information
- **Professional Standards**: Maintains confidentiality and security

## Input Variables

### `bank_statements`

- **Type**: `array:file`
- **Description**: Upload multiple bank statements from different financial institutions (PDF, DOCX, etc.)
- **Required**: Yes
- **Format**: Supports document formats including PDF, DOCX, and other text-based documents

## Processing Steps

### 1. **Individual Statement Processing**

- **Document Conversion**: Converts each statement to markdown text
- **Data Extraction**: Extracts key account information using AI
- **Information Captured**:
  - Bank/Institution name
  - Account holder name
  - Account number (masked)
  - Account type (checking, savings, credit)
  - Statement period (start/end dates)
  - Balance information (opening, closing, available)
  - Transaction summary (deposits, withdrawals, net change)

### 2. **Aggregated Numbers Calculation**

- **Total Balances**: Sums all closing balances by account type
- **Transaction Totals**: Combines deposits and withdrawals across accounts
- **Account Summary**: Counts banks, account types, and total accounts
- **Balance Distribution**: Analyzes liquid assets and credit balances

### 3. **Account Summary Table Generation**

- **Table Creation**: Generates clean, organized table format
- **Data Organization**: Sorts by bank name, then account type
- **Professional Formatting**: Includes headers, totals, and proper alignment
- **Security Compliance**: Ensures account numbers are properly masked

## Output Components

### 1. **Aggregated Numbers Summary**

- **Title**: "Aggregated Numbers Summary"
- **Content**: Key financial totals and summaries
- **Format**: Clear, organized text with bold numbers
- **Includes**:
  - Total net worth and balance breakdowns
  - Transaction totals (deposits, withdrawals, net change)
  - Account distribution and diversification
  - Balance analysis by institution

### 2. **Account Details Summary**

- **Title**: "Account Details Summary"
- **Content**: Professional table of all accounts
- **Format**: Clean table with 6 columns
- **Columns**:
  - Bank Name
  - Account Type
  - Account Number (masked)
  - Account Holder
  - Period
  - End Balance

### 3. **Individual Account Details**

- **Title**: "Individual Account Details"
- **Content**: Detailed information for each account
- **Format**: Structured text for each account
- **Includes**: Complete extracted information for reference

## Technical Requirements

### **AI Model**

- **Model**: OpenAI GPT-4o
- **Task**: Text generation for data extraction and analysis
- **Temperature**: 0.1-0.2 (low for accuracy)
- **Top-p**: 0.9 (balanced creativity and consistency)

### **Document Processing**

- **Task**: `TASK_CONVERT_TO_MARKDOWN`
- **Support**: Document formats (PDF, DOCX, and other text-based documents)
- **Processing**: OCR and text extraction capabilities

### **Data Security**

- **Account Masking**: Automatic masking of account numbers
- **Data Handling**: Secure processing of financial information
- **Output Format**: Text-based outputs (no structured data storage)

## Use Cases

### **Perfect For:**

- **Quick Account Overview**: Get a snapshot of all accounts
- **Financial Consolidation**: Combine information from multiple banks
- **Account Portfolio Review**: See all accounts in one place
- **Monthly Financial Snapshots**: Track account positions over time
- **Basic Financial Reporting**: Simple aggregation for reports

### **Not Suitable For:**

- **Complex Financial Analysis**: No detailed financial health assessment
- **Risk Assessment**: No risk scoring or analysis
- **Investment Planning**: No investment recommendations
- **Budget Analysis**: No detailed spending categorization

## Basic Usage

### **Step 1: Prepare Bank Statements**

- Gather bank statements from all financial institutions
- Ensure statements are in supported formats (PDF, DOCX, etc.)
- Verify statements contain the required period information

### **Step 2: Upload Statements**

- Upload multiple bank statements to the pipeline
- The pipeline will process each statement individually
- All statements will be analyzed and aggregated

### **Step 3: Review Outputs**

- **Aggregated Numbers**: Check total balances and transaction summaries
- **Account Table**: Review the clean account summary table
- **Individual Details**: Reference detailed information for each account

## Example Output

### **Aggregated Numbers Summary**

```
# AGGREGATED NUMBERS SUMMARY

## Total Balances
- **Total Net Worth:** $45,250.00
- **Checking Accounts:** $12,500.00
- **Savings Accounts:** $28,750.00
- **Credit Accounts:** $4,000.00 (available credit)

## Transaction Totals (This Period)
- **Total Deposits:** $8,500.00
- **Total Withdrawals:** $6,200.00
- **Net Change:** +$2,300.00

## Account Summary
- **Number of Banks:** 3 institutions
- **Total Accounts:** 5 accounts
- **Account Types:** 2 checking, 2 savings, 1 credit
```

### **Account Details Summary Table**

```
| Bank Name        | Account Type | Account # | Account Holder | Period           | End Balance |
|------------------|--------------|-----------|----------------|------------------|-------------|
| Bank of America  | Checking     | ****1234  | John Smith     | Jan 1-31, 2024  | $5,500.00   |
| Chase Bank       | Savings      | ****3456  | John Smith     | Jan 1-31, 2024  | $11,500.00  |
| Wells Fargo      | Credit       | ****7890  | John Smith     | Jan 1-31, 2024  | $4,000.00   |
|------------------|--------------|-----------|----------------|------------------|-------------|
| **TOTAL**        |              |           |                |                  | **$21,000.00** |
```

## Best Practices

### **Data Preparation**

- Use recent bank statements for accurate information
- Ensure all statements cover the same time period
- Verify account information is clearly visible in statements

### **Security Considerations**

- Account numbers are automatically masked in outputs
- No sensitive data is stored or retained
- Use secure channels for uploading financial documents

### **Output Usage**

- Review aggregated numbers for quick financial overview
- Use account table for portfolio management
- Reference individual details for specific account information

## Limitations

### **Current Limitations**

- **No Historical Analysis**: Focuses on current statement period only
- **No Trend Analysis**: No comparison with previous periods
- **No Financial Advice**: Provides data only, no recommendations
- **No Budget Integration**: No spending categorization or budget analysis

### **Technical Limitations**

- **Document Quality**: Requires clear, readable bank statements
- **Format Support**: Limited to document formats (PDF, DOCX, etc.)
- **Processing Time**: Depends on number and size of statements

## Support

For questions or issues with the Bank Account Aggregator pipeline:

- Review the technical requirements and limitations
- Ensure bank statements are in supported document formats
- Verify all required information is present in statements
- Check that account information is clearly visible

---

**Note**: This pipeline is designed for data aggregation and presentation only. It does not provide financial advice, risk assessment, or investment recommendations. Always consult with qualified financial professionals for financial planning and investment decisions.

# AI Consultant Profile Generation Pipeline

## Description

The AI Consultant Profile Generation Pipeline automatically creates comprehensive professional profiles for consultants by analyzing multiple data sources including LinkedIn profiles, uploaded documents, and web research. It evaluates consultants against specific skill requirements and generates structured, human-readable reports with insights on background, expertise, achievements, and communication style.

## Features

- **Multi-Source Analysis**: Integrates information from LinkedIn profiles, uploaded documents, and web research
- **Intelligent Document Processing**: Automatically converts and analyzes various document formats (PDFs, presentations, case studies, proposals)
- **Web Research Integration**: Uses Perplexity AI to gather additional publicly available information about consultants
- **Structured Output**: Generates professional, human-readable reports with consistent formatting
- **Skills Evaluation**: Evaluates consultants against specific skill requirements
- **Comprehensive Assessment**: Provides insights on background, expertise, achievements, and communication style
- **Video Reference**: Includes video URLs in reports for additional context (content not analyzed)

## Input Variables

| Variable               | Type       | Description                                                                        |
| ---------------------- | ---------- | ---------------------------------------------------------------------------------- |
| `consultant_name`      | string     | Name of the consultant to analyze                                                  |
| `linkedin_url`         | string     | LinkedIn profile URL of the consultant                                             |
| `video_url`            | string     | URL to consultant's video content (included in report for reference, not analyzed) |
| `skills_list`          | string     | List of skills to evaluate the consultant on                                       |
| `domain`               | string     | Professional domain/industry of the consultant                                     |
| `consultant_documents` | array:file | Upload multiple documents (PDFs, presentations, case studies, proposals, etc.)     |

## Pipeline Components

### 1. Document Processing (`process_documents`)

- **Type**: Iterator
- **Function**: Processes all uploaded consultant documents
- **Action**: Converts documents to markdown format for analysis
- **Output**: Extracted text content from all documents

### 2. Consultant Research (`get_consultant_info`)

- **Type**: Perplexity AI
- **Function**: Gathers comprehensive information about the consultant
- **Action**: Researches LinkedIn profile and public information
- **Model**: Sonar Pro
- **Output**: Detailed research findings about the consultant

### 3. Report Generation (`generate_final_report`)

- **Type**: OpenAI GPT-4
- **Function**: Creates the final comprehensive consultant profile
- **Action**: Integrates all information sources into a structured report
- **Output**: Professional consultant evaluation report

## Output

### 1. Final Consultant Evaluation Report

- **Type**: Text
- **Content**: Comprehensive, human-readable consultant profile
- **Structure**:
  - Executive overview
  - Professional background
  - Industry expertise & specializations
  - Key achievements & project highlights
  - Skills & competencies
  - Communication & presentation style
  - Additional resources
  - Summary

### 2. Document Texts

- **Type**: Text
- **Content**: Raw extracted text from uploaded documents
- **Use**: Reference for document analysis results

### 3. Consultant Research Information

- **Type**: Text
- **Content**: Detailed research findings from web sources
- **Use**: Reference for research data

### 4. Consultant Research Sources

- **Type**: Array
- **Content**: Source URLs and metadata from research
- **Use**: Verification and additional context

## Use Cases

### HR and Recruitment

- Evaluate consultant candidates for project assignments
- Assess skills and experience against job requirements
- Create standardized consultant profiles for internal databases

### Consulting Firms

- Generate client-ready consultant profiles
- Evaluate internal consultant capabilities
- Create marketing materials for consultant services

### Project Management

- Assess consultant fit for specific projects
- Evaluate consultant expertise in relevant domains
- Create comprehensive consultant briefings

### Business Development

- Generate consultant profiles for proposals
- Assess consultant capabilities for client presentations
- Create consultant portfolios for business development

## Technical Requirements

### Components Required

- **OpenAI**: For report generation using GPT-4
- **Perplexity**: For web research and information gathering

Read more about how to [set up components](https://docs.instill-ai.com/docs/set-up-component).

## Example Usage

```yaml
# Example input configuration
consultant_name: "Dr. Sarah Johnson"
linkedin_url: "https://www.linkedin.com/in/sarah-johnson-consultant"
video_url: "https://example.com/sarah-presentation"
skills_list: "Strategic Planning, Change Management, Digital Transformation, Stakeholder Management, Data Analysis"
domain: "Technology Consulting"
consultant_documents: [file1.pdf, file2.pptx, file3.docx]
```

## Output Example

The pipeline generates a structured report like:

# Dr. Sarah Johnson

Dr. Sarah Johnson is a seasoned technology consultant with 15+ years of experience in digital transformation and strategic planning. She specializes in helping Fortune 500 companies navigate complex technological changes while maintaining operational excellence.

## Professional Background

[Comprehensive career overview with progression and achievements]

## Industry Expertise & Specializations

[Domain knowledge and areas of specialization]

## Key Achievements & Project Highlights

[Notable accomplishments and successful projects]

## Skills & Competencies

[Comprehensive skills assessment with evidence]

## Communication & Presentation Style

[Insights about communication effectiveness]

## Additional Resources

- **Video Content:** https://example.com/sarah-presentation
- **LinkedIn Profile:** https://www.linkedin.com/in/sarah-johnson-consultant

## Summary

[Overall assessment and professional standing]

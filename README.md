# Instill Pipelines Collection

A curated collection of production-ready AI pipeline recipes for [Instill Core CE](https://github.com/instill-ai/instill-core). Jump-start your AI applications with ready-to-use workflows for document processing, RAG systems, web automation, and business process automation.

## Prerequisites

- **Instill Core CE** - Follow the [official installation guide](https://github.com/instill-ai/instill-core)
- **OpenAI API Key** - For out-of-box RAG service
- **Integrations** - Configure external service components as needed

## Quick Start

1. **Launch Instill Core CE** - Follow the [official installation guide](https://github.com/instill-ai/instill-core)
2. **Clone this repository** - `git clone https://github.com/instill-ai/pipelines.git`
3. **Choose a pipeline recipe** from the categories below
4. **Create a pipeline** in the console and add the YAML recipe to the pipeline editor
5. **Run and customize** the pipeline in the console for your use case

## Pipeline Categories

### 🤖 **RAG (Retrieval-Augmented Generation)**

Advanced question-answering systems with document retrieval and AI generation.

- **`simple-rag-openai.yaml`** - Basic RAG with OpenAI GPT-4
- **`simple-rag-anthropic.yaml`** - RAG powered by Anthropic Claude
- **`simple-rag-mistral.yaml`** - Cost-effective RAG with Mistral AI
- **`rag-cohere-reranker.yaml`** - Enhanced retrieval with Cohere reranking
- **`rag-assistant-openai.yaml`** - Conversational RAG with memory
- **`simple-corrective-rag.yaml`** - Self-correcting RAG with validation
- **`auto-evaluative-rag.yaml`** - Self-evaluating RAG with quality assessment
- **`rag-report-generator.yaml`** - Automated report generation from documents

### 📄 **File Parsing & Processing**

Transform documents into AI-ready structured content.

- **`simple-doc-to-markdown.yaml`** - Convert documents to clean Markdown
- **`fast-doc-to-text.yaml`** - Quick text extraction from documents
- **`parse-and-chunk.yaml`** - Intelligent parsing with semantic chunking
- **`hybrid-multimodal-parser.yaml`** - Process text, images, and mixed content
- **`audio-to-markdown.yaml`** - Transcribe audio to structured Markdown
- **`video-to-markdown.yaml`** - Extract video content as Markdown

### 🌐 **Web Automation & Scraping**

Automated web data extraction and processing.

- **`crawl-and-scrape.yaml`** - Basic web crawling with content extraction
- **`structured-web-insights.yaml`** - Extract structured data from websites
- **`web-to-catalog.yaml`** - Ingest web content into knowledge catalogs

### 📊 **File Comparison**

Intelligent document analysis and comparison.

- **`semantic-diff.yaml`** - Semantic document comparison with difference detection

### 🏢 **Business Applications**

Ready-to-use enterprise automation workflows.

- **`automated-email-response.yaml`** - AI-powered email response generation
- **`contract-redflags-slack.yaml`** - Contract analysis with Slack notifications
- **`slack-notification-example.yaml`** - Basic Slack integration template

## Configuration

Each pipeline recipe includes customizable variables, such as:

- **Model Selection** - Choose AI models (OpenAI, Anthropic, Mistral)
- **Generation Parameters** - Adjust temperature, top-p, and other settings
- **External Integrations** - Configure email, database, and API connections
- **Output Formats** - Customize response structures

## Contributing

We welcome contributions! To add your pipeline recipe:

1. Fork the repository
2. Create a new YAML file in the appropriate category directory
3. Follow existing naming conventions and structure
4. Add clear variable descriptions and usage examples
5. Include a README for your pipeline explaining its purpose, inputs, outputs, and usage examples
6. Submit a pull request with a detailed description

## Resources

- [Instill Core CE GitHub](https://github.com/instill-ai/instill-core)
- [Instill Core Documentation](https://docs.instill-ai.com)

## Support

- **Issues** - Report bugs via [GitHub Issues](https://github.com/instill-ai/instill-core/issues)
- **Discussions** - Join [Discord community](https://discord.gg/sevxWsqpGh) for help

## License

See [LICENSE](./LICENSE) for details.

---

**Built with ❤️ by the [Instill AI](https://www.instill-ai.com) team**

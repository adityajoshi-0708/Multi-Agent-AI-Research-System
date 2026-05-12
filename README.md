# Multi-Agent Research System

## Overview

A sophisticated research automation system leveraging multiple AI agents to conduct comprehensive research, synthesize information, and generate structured reports. The system orchestrates specialized agents to search, scrape, write, and critically evaluate research findings.

## Architecture

The system comprises four coordinated agents operating within a pipeline framework:

1. **Search Agent** - Queries the web for recent, reliable information on specified topics using Tavily Search API
2. **Reader Agent** - Scrapes and extracts clean content from URLs identified by the search agent
3. **Writer Agent** - Synthesizes gathered information into well-structured research reports
4. **Critic Agent** - Evaluates reports and provides constructive feedback and scoring

## System Requirements

- Python 3.8 or higher
- Mistral AI API key
- Tavily Search API key

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd Multi-agent-research-system
```

2. Create and activate virtual environment:
```bash
python -m venv .venv
.venv\Scripts\Activate.ps1  # Windows
source .venv/bin/activate   # macOS/Linux
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Configure environment variables in `.env`:
```
MISTRAL_API_KEY=your_mistral_api_key
TAVILY_API_KEY=your_tavily_api_key
```

## Usage

### Command Line Interface

Run the research pipeline from terminal:
```bash
python pipeline.py
```

When prompted, enter your research topic. The system will execute the complete research workflow and display results at each stage.

### Example
```bash
Enter a research topic: Quantum Computing Applications in Healthcare
```

### Streamlit Web Interface

Launch the interactive web application:
```bash
streamlit run app.py
```

Access the interface at `http://localhost:8501`

## Project Structure

```
.
├── agents.py          # Agent definitions and LLM configuration
├── pipeline.py        # Research workflow orchestration
├── tools.py           # Search and scraping utilities
├── app.py             # Streamlit web interface
├── requirements.txt   # Python dependencies
├── .env               # API credentials
└── README.md          # Project documentation
```

## Output

The pipeline generates:

- **Search Results** - Top relevant sources with titles, URLs, and snippets
- **Scraped Content** - Full text extraction from primary sources
- **Research Report** - Structured document including:
  - Introduction
  - Key Findings (minimum 3 points)
  - Conclusion
  - Source References
- **Critical Evaluation** - Performance score and improvement suggestions

## Configuration

### Model Selection

Modify the model in `agents.py`:
```python
llm = ChatMistralAI(
    model="mistral-large-latest",  # or mistral-small for cost optimization
    temperature=0,
    max_retries=3
)
```

### Rate Limiting

The system includes built-in delays between requests:
- 3-second intervals between agent calls
- Automatic retry with exponential backoff
- Configurable sleep duration in `pipeline.py`

## Dependencies

Core Components:
- **LangChain** - Agent and chain orchestration
- **Mistral AI** - Large language model backend
- **Tavily** - Web search API
- **BeautifulSoup4** - HTML parsing and content extraction
- **Streamlit** - Web interface framework

See `requirements.txt` for complete dependency list.

## Error Handling

### Rate Limit Errors (HTTP 429)

If rate limits are exceeded:
1. Increase sleep duration between requests in `pipeline.py`
2. Upgrade Mistral API tier for higher limits
3. Switch to a lower-cost model like `mistral-small`

### Connection Errors

Ensure API credentials are correctly set in `.env` file and have active network connectivity.

## Performance Notes

- Average execution time: 2-4 minutes per topic
- Network requests are the primary bottleneck
- Increasing delays improves reliability but increases total execution time

## API Credentials

- **Mistral AI**: Obtain from https://console.mistral.ai/
- **Tavily Search**: Obtain from https://tavily.com/

## Limitations

- Subject to API rate limits of respective services
- Content quality depends on available sources for the research topic
- Web scraping may fail on JavaScript-heavy or restricted websites

## Contributing

Contributions are welcome. Please ensure code follows the existing style conventions and test thoroughly before submission.

## License

Specify your project license here.

## Support

For issues or questions, please refer to the official documentation or contact the development team.

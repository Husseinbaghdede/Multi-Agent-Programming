# Developer Tools Research Agent

A sophisticated AI-powered research agent that automatically discovers, analyzes, and compares developer tools and technologies. Built with LangGraph workflows and powered by advanced web scraping capabilities.

## 🚀 Overview

This intelligent agent streamlines the developer tool evaluation process by:
- **Automated Discovery**: Extracts relevant tools from industry articles and comparisons
- **Deep Analysis**: Scrapes official websites to gather comprehensive tool information
- **Smart Recommendations**: Provides actionable insights based on pricing, features, and technical capabilities

## ✨ Key Features

### 🔍 Intelligent Tool Discovery
- Searches for relevant articles and comparison guides
- Extracts actual product names from content using LLM-powered analysis
- Fallback mechanisms ensure comprehensive coverage

### 📊 Comprehensive Analysis
- **Pricing Models**: Identifies Free, Freemium, Paid, or Enterprise tiers
- **Technical Stack**: Extracts supported languages, frameworks, and technologies
- **API Availability**: Detects REST APIs, GraphQL endpoints, and SDK support
- **Integration Ecosystem**: Maps compatibility with popular development tools
- **Open Source Status**: Determines licensing and source availability

### 🎯 Developer-Focused Insights
- Language-specific support analysis
- Development workflow integration capabilities
- API and programmatic access evaluation
- Cost-benefit recommendations

## 🏗️ Architecture

Built on a modular, extensible architecture:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Tool Extract  │───▶│    Research     │───▶│    Analysis     │
│                 │    │                 │    │                 │
│ • Article Search│    │ • Official Sites│    │ • LLM Analysis  │
│ • LLM Filtering │    │ • Web Scraping  │    │ • Structured    │
│ • Tool Names    │    │ • Data Collection│    │   Output       │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### Core Components

- **LangGraph Workflow**: State-managed research pipeline
- **Firecrawl Integration**: Advanced web scraping with markdown output
- **OpenAI GPT-4**: Structured analysis and recommendations
- **Pydantic Models**: Type-safe data validation and serialization

## 🛠️ Technology Stack

- **Python 3.8+**
- **LangGraph**: Workflow orchestration
- **LangChain**: LLM integration and structured output
- **Firecrawl**: Web scraping and content extraction
- **Pydantic**: Data validation and serialization
- **OpenAI API**: Natural language processing

## ⚡ Quick Start

### Prerequisites
```bash
# Required API keys
FIRECRAWL_API_KEY=your_firecrawl_key
OPENAI_API_KEY=your_openai_key
```

### Installation
```bash
# Clone repository
git clone <repository-url>
cd developer-tools-research-agent

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Add your API keys to .env file
```

### Usage
```bash
# Interactive mode
python main.py

# Example queries:
# "best database for Python web apps"
# "open source authentication solutions"
# "serverless deployment platforms"
```

## 📝 Example Output

```
🔍 Developer Tools Query: best database for Python web apps

📊 Results for: best database for Python web apps
============================================================

1. 🏢 Supabase
   🌐 Website: https://supabase.com
   💰 Pricing: Freemium
   📖 Open Source: True
   🛠️  Tech Stack: PostgreSQL, JavaScript, TypeScript, Python, Dart
   💻 Language Support: Python, JavaScript, TypeScript, Dart, Swift
   🔌 API: ✅ Available
   🔗 Integrations: GitHub, Vercel, Netlify, Next.js
   📝 Description: Open-source Firebase alternative with real-time database

2. 🏢 PlanetScale
   🌐 Website: https://planetscale.com
   💰 Pricing: Freemium
   📖 Open Source: False
   🛠️  Tech Stack: MySQL, Vitess, Kubernetes
   💻 Language Support: Python, Node.js, Go, PHP, Ruby
   🔌 API: ✅ Available
   🔗 Integrations: Prisma, Django, Rails, Laravel

Developer Recommendations:
----------------------------------------
For Python web apps, Supabase offers the best balance of features and cost-effectiveness with its generous free tier and built-in authentication. PlanetScale excels for high-scale applications requiring MySQL compatibility. Consider Supabase for rapid prototyping and PlanetScale for production applications with complex scaling needs.
```

## 🔧 Configuration

### Environment Variables
```env
# Required
FIRECRAWL_API_KEY=fc-your-api-key
OPENAI_API_KEY=sk-your-openai-key

# Optional
SEARCH_RESULTS_LIMIT=5
ANALYSIS_TEMPERATURE=0.1
```

### Customization Options

**Search Parameters**:
- Modify `num_results` in `FirecrawlService.search_companies()`
- Adjust content length limits in workflow steps

**Analysis Prompts**:
- Customize prompts in `src/prompts.py`
- Add domain-specific analysis criteria
- Modify structured output schemas

**Output Format**:
- Extend `CompanyInfo` model for additional fields
- Customize recommendation templates
- Add export capabilities (JSON, CSV, etc.)

## 🧪 Advanced Usage

### Programmatic API
```python
from src.workflow import Workflow

# Initialize workflow
workflow = Workflow()

# Run analysis
result = workflow.run("best CI/CD tools for microservices")

# Access structured data
for company in result.companies:
    print(f"{company.name}: {company.pricing_model}")
    
# Get recommendations
print(result.analysis)
```

### Custom Analysis Pipeline
```python
from src.models import ResearchState
from src.workflow import Workflow

# Create custom state
state = ResearchState(
    query="GraphQL backends for mobile apps",
    extracted_tools=["Hasura", "Apollo", "PostGraphile"]
)

# Run specific steps
workflow = Workflow()
result = workflow._research_step(state)
```

## 🧩 Extension Points

### Adding New Data Sources
```python
class CustomScraper:
    def search_companies(self, query: str):
        # Implement custom search logic
        pass
    
    def scrape_company_pages(self, url: str):
        # Implement custom scraping logic
        pass
```

### Custom Analysis Models
```python
class EnterpriseAnalysis(BaseModel):
    compliance_certifications: List[str]
    enterprise_features: List[str]
    support_tiers: List[str]
    # Add enterprise-specific fields
```

## 🔒 Security & Privacy

- **API Key Management**: Environment-based configuration
- **Rate Limiting**: Built-in request throttling
- **Data Privacy**: No persistent storage of scraped content
- **Error Handling**: Graceful degradation on API failures

## 🚦 Limitations

- **Rate Limits**: Constrained by Firecrawl and OpenAI API limits
- **Content Accuracy**: Dependent on website content quality
- **Language Support**: Currently optimized for English content
- **Real-time Data**: Information reflects website content at scraping time

## 📊 Performance

- **Average Query Time**: 30-45 seconds
- **Concurrent Requests**: Limited by API rate limits
- **Memory Usage**: ~100MB typical, ~500MB peak
- **Cache Strategy**: No caching (fresh data each query)

## 🤝 Contributing

### Development Setup
```bash
# Development dependencies
pip install -r requirements-dev.txt

# Run tests
pytest tests/

# Code formatting
black src/ main.py
flake8 src/ main.py
```

### Contribution Guidelines
- Follow PEP 8 style guidelines
- Add type hints for all functions
- Include docstrings for public APIs
- Write unit tests for new features
- Update documentation for API changes

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Issues**: GitHub Issues for bug reports and feature requests
- **Documentation**: Wiki for detailed guides and examples
- **Community**: Discussions for questions and sharing

## 🗺️ Roadmap

- **v2.0**: Multi-language content support
- **v2.1**: Persistent caching and data storage
- **v2.2**: Advanced filtering and comparison metrics
- **v2.3**: Integration with package managers (npm, PyPI, etc.)
- **v3.0**: Real-time monitoring and trend analysis

---

*Built with ❤️ for the developer community*

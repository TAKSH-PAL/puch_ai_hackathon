# MCP Starter - Delhi Metro Tools

![Python](https://img.shields.io/badge/python-3.11+-blue.svg)
![MCP](https://img.shields.io/badge/MCP-Model%20Context%20Protocol-green.svg)
![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)

A powerful MCP (Model Context Protocol) server that provides comprehensive Delhi Metro routing, scraping, and shareable PDF route cards. Originally designed for the Puch AI hackathon, this project serves as a starter template for building MCP servers with web scraping and document generation capabilities.

## 🚀 Features

### Metro Tools
- **`metro_route_scrape`** — Scrape route information including fare, duration, stations, and transfers from delhimetrorail.info
- **`fare_optimizer`** — Calculate total costs for adults/children with scraped fare data
- **`station_accessibility`** — Check accessibility features (lifts, escalators, ramps, parking) and gate information
- **`shareable_route_card`** — Generate professional one-page PDF route cards saved to disk
- **`validate`** — Required Puch validation tool for hackathon compliance

### Technical Stack
- **FastMCP** framework for rapid MCP server development
- **httpx** for async HTTP requests and web scraping
- **BeautifulSoup4** for HTML parsing
- **ReportLab** for PDF generation
- **Poetry** for dependency management
- **Pydantic** for data validation

## 📋 Prerequisites

- Python 3.11 or higher
- Poetry (recommended) or pip for dependency management
- Valid authentication token (for secured endpoints)

## 🛠️ Installation

### Using Poetry (Recommended)

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd mcp-starter
   ```

2. **Install dependencies**
   ```bash
   poetry install
   ```

3. **Activate the virtual environment**
   ```bash
   poetry shell
   ```

### Using pip

1. **Clone and setup virtual environment**
   ```bash
   git clone <repository-url>
   cd mcp-starter
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

## ⚙️ Configuration

1. **Create environment file**
   ```bash
   cp .env.example .env
   ```

2. **Configure your environment variables**
   ```
   AUTH_TOKEN="your-auth-token"
   MY_NUMBER="91your-number"
   ```

## 🚂 Usage

### Running the Server

Start the MCP server:

```bash
python main.py
```

### Available Tools

#### 1. Metro Route Scraping

```python
# Example of using the metro_route_scrape tool
result = await mcp.call("metro_route_scrape", {
    "from_station": "Mohan Nagar",
    "to_station": "Kashmere Gate"
})
```

#### 2. Fare Optimization

```python
# Example of using the fare_optimizer tool
result = await mcp.call("fare_optimizer", {
    "adults": 2,
    "children": 1,
    "fare": 50.0  # Optional, will use scraped fare if available
})
```

#### 3. Station Accessibility Information

```python
# Example of using the station_accessibility tool
result = await mcp.call("station_accessibility", {
    "station": "Kashmere Gate"
})
```

#### 4. Generate Shareable Route Card

```python
# Example of using the shareable_route_card tool
result = await mcp.call("shareable_route_card", {
    "from_station": "Mohan Nagar",
    "to_station": "Kashmere Gate",
    "include_accessibility": True,  # Optional
    "output_path": "route_card.pdf"  # Optional
})
```

## 📊 Response Format

All tools return structured data in a consistent format:

```json
{
  "status": "success",
  "data": { ... },  // Tool-specific response data
  "metadata": {
    "source": "delhimetrorail.info",
    "timestamp": "2023-08-12T09:45:30Z"
  }
}
```

## 🔒 Security Considerations

- Authentication tokens are required for certain endpoints
- All API keys and credentials should be stored in the `.env` file (never commit this to version control)
- Rate limiting is implemented to prevent excessive scraping

## 🔄 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

## 📝 Notes

> This project is designed for hackathon/demo purposes. Web scraping depends on the target website's HTML structure and may break if the site changes its layout or design.

## 🙏 Acknowledgements

- Delhi Metro Rail Corporation for providing public transit information
- Puch AI for organizing the hackathon that inspired this project
- All contributors who have helped improve this tool

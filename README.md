# Agentic Research Agent

An AI agent built for the **Anakin Forge Hackathon** that takes a topic, searches the web, reads the top results, and generates a clean, LLM-powered summary — all automatically, without a human reading each page manually.

## How It Works

```
Topic → Web Search → Scrape Top Pages → Combine Text → LLM Summary → Saved as .md
```

1. **Search** — Uses the `ddgs` (DuckDuckGo Search) library to find the top results for a given topic.
2. **Read** — Scrapes each result page using `requests` + `BeautifulSoup`, extracting the readable paragraph text.
3. **Reason** — Combines all the scraped text and sends it to an LLM (via the Groq API) with a summarization prompt.
4. **Output** — Saves the final summary as a clean `.md` file.

## Tech Stack

- **Python**
- **Groq API** (LLM — `openai/gpt-oss-20b`)
- **ddgs** — free web search
- **requests + BeautifulSoup** — web scraping
- **python-dotenv** — secure API key handling

## Setup & Usage

1. Clone this repo and install dependencies:
   ```
   pip install groq python-dotenv ddgs requests beautifulsoup4
   ```
2. Create a `.env` file in the project root with your own Groq API key:
   ```
   GROQ_API_KEY=your_key_here
   ```
3. Open `agentic-ai.ipynb` in Jupyter Notebook and run the cells.
4. Call the agent with any topic:
   ```python
   run_agent("latest smartphone trends 2026")
   ```
5. The summary will be saved as a `.md` file in the project folder.

## Example

Input topic: `"latest smartphone trends 2026"`
Output: A concise, point-wise summary of current smartphone trends, generated from live web content — saved to a markdown file.

## Notes

- The agent trims combined scraped text to stay within the Groq free-tier token limit.
- Includes error handling so a single failed page doesn't crash the whole pipeline.

## Future Plans

Planning to extend this into a standalone summarizer web app — accepting direct URLs (including video links) and offering a simple HTML/CSS/JS frontend.

---
Built by Vaishnavi Tripathi for the Anakin Forge Hackathon.

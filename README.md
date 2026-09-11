# Agentic Research & Comparison Agent

An AI agent built for the **Anakin Forge Hackathon** that goes beyond a chatbot — it browses live web content, reasons through multi-step research, and produces a decision-oriented output: either a topic summary or a head-to-head comparison with a clear recommendation.

## Features

1. **Research Agent** — takes a topic, searches the web, reads the top results, and generates a clean summary with sources.
2. **Comparison Agent** — takes two options (e.g. two products), independently researches both, and produces pros/cons for each plus a final recommendation on which is better and why. This is the multi-step reasoning piece: the agent doesn't just report facts, it weighs them and decides.

## How It Works

```
Topic(s) -> Web Search -> Scrape Top Pages -> Combine Text -> LLM Reasoning -> Summary / Recommendation -> Saved as .md (with sources)
```

1. **Search** — Uses the `ddgs` (DuckDuckGo Search) library to find top results for a topic.
2. **Read** — Scrapes each result page using `requests` + `BeautifulSoup`, extracting readable paragraph text.
3. **Reason** — Sends the combined content to an LLM (via the Groq API) with either a summarization prompt or a comparison-and-recommendation prompt.
4. **Output** — Saves the result as a `.md` file, including a list of the sources used.

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
3. Open `agentic-ai.ipynb` in Jupyter Notebook and run all cells.
4. **For a single-topic summary:**
   ```python
   run_agent("latest smartphone trends 2026")
   ```
5. **For a comparison with recommendation:**
   ```python
   compare_agent("iPhone 16", "Samsung Galaxy S25")
   ```
6. Output is saved as a `.md` file in the project folder (filename varies by mode/topic), including source links.

## Example

Input: `compare_agent("iPhone 16", "Samsung Galaxy S25")`
Output: A structured comparison — pros/cons for each phone, pulled from live web content, ending in a clear recommendation on which to choose and why. Sources are listed for both options.

## Notes

- Combined scraped text is trimmed to stay within the Groq free-tier token limit.
- Includes error handling so a failed page or empty search doesn't crash the pipeline.

## Future Plans

Planning to extend this into a standalone summarizer/comparison web app — accepting direct URLs (including video links) and offering a simple HTML/CSS/JS frontend.

---
Built by Vaishnavi Tripathi for the Anakin Forge Hackathon.

# AI-Powered Website Summarizer

This project is part of my learning while following [Edward Donner's LLM Engineering course and resources](https://edwarddonner.com/2024/11/13/llm-engineering-resources/). I come from a software development background and am exploring how to build applications powered by Large Language Models (LLMs).

## What does it do?

The project takes a website URL, extracts the website's text, and asks Google's Gemini model to produce a short summary.

The summary's style is controlled through a prompt. In the current notebook, the assistant is instructed to be **snarky, humorous, and concise etc**. You can change the instructions to experiment with other tones, such as:

- Professional and formal
- Simple and beginner-friendly
- Humorous or sarcastic
- Technical and detailed, etc

### How it works

1. You provide a website URL.
2. The scraper retrieves the website's text content.
3. A system instruction and user prompt tell Gemini what to do with that content.
4. Gemini generates a summary.
5. The notebook displays the result as Markdown.


> This is an LLM-powered application that uses an existing Gemini model through an API. It does not train or build a frontier model from scratch.

## Tech stack

- **Python** — application logic
- **Google Gemini API** — generates the summaries
- **Google Gen AI Python SDK (`google-genai`)** — connects Python to Gemini
- **Add python-dotenv** —  add it in your local dir and load the API key from a local `.env` file
- **Jupyter Notebook** — interactive development and experimentation
- **Website scraper (`scraper.py`)** — extracts website content
- **IPython Markdown display** — formats the generated summary in the notebook

## Project structure

The notebook imports a local module named `scraper`, so make sure `scraper.py` is present in the project directory (or in a directory on Python's import path).

If your notebook has a different filename, open that notebook instead. The `scraper.py` file must provide the `fetch_website_contents(url)` function used by the notebook.

## Setup and installation

### 1. Clone the repository

Replace the placeholder with your GitHub repository URL:

```bash
git clone https://github.com/cytormod/AI_Engineering_Projects.git
cd AI_Engineering_Projects
```

If you have already downloaded or cloned the project, open a terminal in the project directory.

### 2. Create and activate a virtual environment

**Linux / macOS:**

```bash
python3 -m venv .venv
source .venv/bin/activate
```

**Windows PowerShell:**

```powershell
py -m venv .venv
.venv\Scripts\Activate.ps1
```

### 3. Install the Python packages

With the virtual environment activated:

```bash
python -m pip install --upgrade pip
python -m pip install google-genai python-dotenv ipython jupyter
```

The notebook also imports `scraper.py`. Install any additional packages required by that file. For example, if it uses `requests` and `beautifulsoup4`, install them with:

```bash
python -m pip install requests beautifulsoup4
```

If the repository includes a `requirements.txt` or `pyproject.toml`, prefer installing the project's declared dependencies instead.

## Configure your Gemini API key

The project uses a Gemini API key to authenticate requests to Google's Gemini API.

### 1. Generate an API key

1. Open [Google AI Studio – API keys](https://aistudio.google.com/app/apikey).
2. Sign in with your Google account.
3. Create an API key (or select an existing key).
4. Copy the key and keep it private.

Official guide: [Get started with the Gemini API](https://ai.google.dev/gemini-api/docs/quickstart).

### 2. Create a `.env` file

In the **project's root directory** — the same directory from which you run the notebook — create a file named exactly:

```text
.env
```

Add your key in this format:

```dotenv
GEMINI_API_KEY=PASTE_YOUR_API_KEY_HERE
```

Replace the placeholder with your actual key. Do not add quotes unless your environment requires them, and do not add spaces around the `=` sign.

### 3. Keep the key out of GitHub

Add the following entries to your `.gitignore` file:

```gitignore
.env
.venv/
__pycache__/
.ipynb_checkpoints/
```

**Never commit, publish, or share your real API key.** If a key is accidentally exposed, revoke it in Google AI Studio and create a new one. Do not put the key directly in a notebook, Python source file, screenshot, or README.

## Run the notebook

1. Open the project folder in VS Code.
2. Open `day1.ipynb` (or the notebook's actual filename).
3. Select the Python interpreter from the `.venv` virtual environment as the notebook kernel.
4. Run the cells from top to bottom.
5. Try changing the URL and the system prompt to experiment with different summaries.

The notebook loads the key using `python-dotenv` and reads `GEMINI_API_KEY` from the environment. The `.env` file needs to be in the working directory where `load_dotenv()` can find it.

## Customizing the summary

The assistant's personality and output format are defined by the `system_prompt` in the notebook. For example:

```python
system_prompt = """
You are a professional assistant.
Analyze the website content and provide a clear, concise summary.
Respond in Markdown.
"""
```

You can also change the user prompt to request a different length, audience, or focus.

## Troubleshooting

| Problem | What to check |
|---|---|
| `No API key was found` | Confirm the file is named `.env`, is in the notebook's working directory, and contains `GEMINI_API_KEY=...`. |
| API authentication error | Check that the key is valid, has not been revoked, and is configured for the Gemini API. |
| `ModuleNotFoundError: No module named 'google'` | Activate `.venv` and install `google-genai` using the same Python interpreter as the notebook kernel. |
| `No module named 'dotenv'` | Install `python-dotenv` in the active environment. |
| `No module named 'scraper'` | Make sure `scraper.py` is present and that the notebook is running with the project directory on its import path. |
| Model not found / unavailable | Check the model IDs currently available to your API key in Google AI Studio or the Gemini API documentation, then update the model name used in the notebook. |
| Website cannot be scraped | The site may block automated requests, require JavaScript, or restrict access. Try another publicly accessible URL. |

**Model note:** The notebook currently contains more than one model ID. Model availability can change, so check the models available to your Gemini API key and use a supported model ID consistently in the API calls.

## Current scope and limitations

- The project summarizes the text that the scraper can successfully retrieve; it does not necessarily understand every image, video, interactive element, or dynamically loaded section on a webpage.
- Some websites block scraping or require JavaScript to render their content.
- The quality of the summary depends on the extracted content, prompt, and selected Gemini model.
- API usage is subject to Google's current quotas, rate limits, and pricing. Check [Gemini API pricing](https://ai.google.dev/gemini-api/docs/pricing) and your usage in [Google AI Studio](https://aistudio.google.com/).

## Learning goals

Through this first project, I am getting hands-on experience with:

- Calling an LLM through an API
- Managing API keys with environment variables
- Extracting text from websites
- Writing system instructions and user prompts
- Controlling an LLM's tone and response format
- Building a small Python application around an LLM

## Acknowledgements

- [Edward Donner – LLM Engineering Resources](https://edwarddonner.com/2024/11/13/llm-engineering-resources/)
- [Google AI Studio](https://aistudio.google.com/)
- [Gemini API documentation](https://ai.google.dev/gemini-api/docs)
- [Google Gen AI Python SDK](https://googleapis.github.io/python-genai/)

---

**Learning in public, building one project at a time.**

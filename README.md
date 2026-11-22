# novel-translator-fr

Scrapes a web novel chapter and its metadata from novelbin, then translates the chapter into French with Google Gemini.

## Features

- Fetches chapter text from `#chr-content` paragraphs.
- Fetches novel title, genres and description.
- Translates text to French with `gemini-1.5-flash` and a JSON response schema.
- Saves the title, chapter title and translated text to `translated_chapter.csv`.

## Tech stack

Python 3, requests, BeautifulSoup4, google-generativeai, python-dotenv.

## Project structure

```
main.py          entry point and CSV output
scraper.py       NovelScraper (chapter text, novel info)
translator.py    Translator (Gemini call)
requirements.txt
```

## Setup and run

1. `pip install -r requirements.txt`
2. Create a `.env` file with:
   - `GEMINI_API_KEY`: your Google Gemini API key.
3. `python main.py`

## Usage

The chapter and novel URLs are hardcoded in `main()` in `main.py`. Edit `chapter_url` and `novel_url`, then run. The output is `translated_chapter.csv`. The chapter title is written as the fixed text "Chapter 2".

## Status and limitations

- The code is a working sketch, not a polished tool. One chapter per run, no batching or retries.
- The scraper selectors fit novelbin pages only and may break if the site changes.
- The Gemini model name is old and may be retired; change it in `translator.py`.
- On invalid JSON the translator falls back to `eval` on the model output. Treat that as unsafe.
- Safety filters are set to `BLOCK_NONE`.
- Respect the source site's terms and copyright.

## License

MIT

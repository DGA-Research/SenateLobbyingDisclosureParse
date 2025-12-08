# Lobbying Disclosure Explorer

Streamlit interface plus reusable API client for exploring U.S. Senate Lobbying Disclosure (LDA) filings. Analysts can search by client or lobbyist, fetch the full paginated JSON payload, preview the most recent filings, and download flattened CSV exports without writing scripts.

## Features

- Authenticated requests against `https://lda.senate.gov/api/v1` via a lightweight `LDAClient` wrapper in `lda_api.py`.
- Client and lobbyist search modes with optional numeric IDs to bypass fuzzy lookups.
- Adjustable pause between paginated API calls to respect rate limits.
- Preview of the first 20 filings showing filing UUID, period, registrant, client, income, and expenses.
- Download buttons for the raw JSON payload, a fully flattened CSV, and a simplified CSV with core registrant/client fields.

## Requirements

- Python 3.9+
- `pip install streamlit requests`
- LDA API token added to `.streamlit/secrets.toml`:
  ```toml
  api_token = "your senate api token"
  ```

## Running the App

```bash
streamlit run streamlit_app.py
```

## Usage

1. Launch the Streamlit app and ensure it detects the `api_token` secret.
2. Choose **Client** or **Lobbyist** mode in the sidebar and provide a name and/or numeric ID.
3. Optionally tweak the pause slider if you are fetching large result sets.
4. Click **Fetch Filings** to call the API. The app reports the count and shows a preview table.
5. Use the download buttons to grab JSON or CSV exports for downstream analysis.

The underlying `lda_api.py` module can also be used programmatically for scripted ingestion or bulk exports.

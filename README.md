# Resume ATS Analyzer

A beginner-friendly Streamlit app that accepts PDF, DOCX, and TXT resumes, extracts text, and uses Google's Gemini Flash model to provide an estimated ATS-readiness score and actionable resume improvements. An additional transparent checklist score is calculated locally.

> **Important:** No third-party app can know the exact score a particular employer's ATS will assign. The scores here are estimates, not hiring guarantees.

## Features

- Upload PDF, DOCX, or TXT (maximum 5 MB)
- Optional job description matching
- Gemini feedback: strengths, prioritized improvements, keyword suggestions, formatting tips, and example bullet rewrites
- Simple local checklist score for a second perspective
- Download results as JSON
- No database or permanent resume storage in this starter app

## 1. Requirements

- Python 3.10 or newer (Python 3.11 or 3.12 recommended)
- A Google Gemini API key from [Google AI Studio](https://aistudio.google.com/apikey)
- Internet connection for Gemini requests

## 2. Run locally

Open a terminal in this folder and create a virtual environment:

**Windows PowerShell**

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
$env:GEMINI_API_KEY="PASTE_YOUR_API_KEY_HERE"
streamlit run app.py
```

If `py` is not recognized, try `python -m venv .venv` instead. If PowerShell blocks activation, you can skip activation and install/run with `.venv\Scripts\python.exe -m pip install -r requirements.txt` and `.venv\Scripts\python.exe -m streamlit run app.py`.

The app should open at `http://localhost:8501`.

### Alternative: use Streamlit Secrets locally

Create `.streamlit/secrets.toml` and add:

```toml
GEMINI_API_KEY = "PASTE_YOUR_API_KEY_HERE"
```

Do not upload this file or commit your API key to GitHub. The app also reads `GEMINI_API_KEY` from the environment.

## 3. Push to GitHub using the website UI (no Git commands)

1. Sign in at [GitHub](https://github.com/) and click **+** → **New repository**.
2. Give it a name such as `resume-ats-analyzer`. Choose **Public** or **Private**, then click **Create repository**.
3. On the repository page, choose **Add file** → **Upload files**.
4. Upload `app.py`, `README.md`, and `requirements.txt` from this project folder.
5. If you created `.streamlit/secrets.toml` locally, **do not upload it**. Do not put your API key in any source file.
6. Add a commit message such as `Add Resume ATS Analyzer app`, then click **Commit changes**.

The README and requirements filenames must be exactly `README.md` and `requirements.txt` for the steps below.

## 4. Deploy on Streamlit Community Cloud

1. Visit [Streamlit Community Cloud](https://share.streamlit.io/) and sign in with GitHub.
2. Click **Create app** and select **Yup, I have an app** (wording may vary).
3. Select your GitHub repository, branch (usually `main`), and main file path `app.py`.
4. Open **Advanced settings** before deploying. In the **Secrets** field, add this TOML line:

   ```toml
   GEMINI_API_KEY = "PASTE_YOUR_API_KEY_HERE"
   ```

5. Choose Python 3.11 or 3.12 if prompted, then click **Save** / **Deploy**.
6. Wait for the build to finish. Streamlit will provide a public app URL if your app's sharing settings allow public access.
7. If deployment fails, open the app's logs and check that the three files are in the repository root and `requirements.txt` contains the dependencies.

Official guide: [Deploy an app](https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app). Secrets guide: [Streamlit secrets management](https://docs.streamlit.io/deploy/streamlit-community-cloud/deploy-your-app/secrets-management).

## 5. Test checklist

- Start the app and confirm the page loads.
- Upload a text-based PDF, DOCX, and TXT file in separate runs.
- Try a scanned PDF: the app should explain that OCR may be required if no text can be extracted.
- Paste a job description and verify the report mentions job-relevant keywords.
- Try without a key: the app should display a clear setup message.
- Never use a real API key in a public screenshot, commit, or source file.

## Limitations and privacy

- Scanned/image-only PDFs need OCR before upload.
- Resume text is sent to Google Gemini when analysis is requested. Review Google's current API terms and privacy documentation before using real personal data.
- This demo does not persist resume files, but that does not mean the content is never processed or retained by the AI provider.
- The checklist is deliberately simple and cannot replicate proprietary ATS ranking logic.
- For production use, add rate limiting, stronger file validation, privacy disclosures, logging controls, and tests with representative resumes.

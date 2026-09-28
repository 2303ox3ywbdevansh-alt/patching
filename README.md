# VulnDetect

A Flask application for heuristic static analysis of source files and ZIP project archives.

## Run locally

```powershell
python -m pip install -r requirements.txt
python app.py
```

Open http://127.0.0.1:5000. Upload one supported source/configuration file or a project ZIP (up to 50 MB). ZIP contents are extracted with path checks and file-count, per-file, and expanded-size limits.

## Deploy to Railway

Deploy the contents of this folder from the repository root. The included `Procfile` starts Gunicorn on `0.0.0.0:$PORT`; `requirements.txt` installs Gunicorn. If Railway does not detect the Procfile, set the service Start Command to:

```sh
gunicorn --bind 0.0.0.0:$PORT app:app
```

After changing the code or start command, trigger a new deployment and check the deployment logs if it still fails.

## Detection coverage

Checks common risky code patterns across Python, JavaScript/TypeScript, PHP, Java, Ruby, Go, C#, C/C++, and configuration files. Findings include severity, file, line, matched code, and suggested remediation. Findings can be filtered/searched and exported as JSON.

This is a pattern-based SAST helper. It does not resolve data flow, understand all language syntax, audit dependency versions, or prove exploitability. Review findings in context; a clean scan does not guarantee that software is secure.

## Patch generation

Each report finding has a download action. For a small set of narrowly understood issues (debug mode, unsafe yaml.load, direct innerHTML, and disabled Python TLS verification), it creates a one-line unified diff. Other findings download a remediation guide explaining why the app did not guess a code edit. Patches are suggestions and are never applied automatically; review and test them before use.

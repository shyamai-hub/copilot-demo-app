# copilot-demo-app

📦 **Multi-service demo app** — This repository contains multiple example services showcasing different technology stacks and a simple React frontend:

- **backend-dotnet** — C# Web API (.NET 8)
- **backend-java** — Spring Boot (Java, Maven)
- **backend-python** — FastAPI (Python)
- **frontend** — React + Vite (JavaScript)
- **prompts** — notes and scripts for the demo

---

## Prerequisites ✅

Make sure you have these installed locally:

- .NET SDK 8.x (dotnet)
- Java JDK 11+ and Maven
- Python 3.10+ and pip (or a virtual environment)
- Node.js 18+ and npm or Yarn
- Optional: Docker & docker-compose

---

## Per-service quick start 🔧

All commands assume you run them from the workspace root (project root). Use separate terminals for each service.

### .NET (backend-dotnet)

Folder: `backend-dotnet`

Run:

```bash
cd backend-dotnet
# restore (optional)
dotnet restore
# run the API
dotnet run
```

Default dev URL: http://localhost:5000/ (see `Program.cs` for current binding)

Quick check:

```bash
curl http://localhost:5000/
```

Build & publish:

```bash
cd backend-dotnet
dotnet build -c Release
dotnet publish -c Release -o out
# run the published app
dotnet out/backend-dotnet.dll
```

---

### Java Spring Boot (backend-java)

Folder: `backend-java`

Run:

```bash
cd backend-java
# run via Maven
mvn spring-boot:run
```

Or build a JAR and run:

```bash
cd backend-java
mvn package
java -jar target/*.jar
```

Default dev URL: http://localhost:8080/

Quick check:

```bash
curl http://localhost:8080/
```

---

### Python FastAPI (backend-python)

Folder: `backend-python`

Recommended: create and activate a virtual environment, then install the project (using the `pyproject.toml`) so dependencies are installed automatically.

````bash
```bash
cd backend-python
# create a virtual environment with uv
uv venv
source .venv/bin/activate    # macOS / Linux
# install dependencies using uv
uv sync

# run with uvicorn (recommended):
uv run uvicorn main:app --reload --host 0.0.0.0 --port 8000
# or run directly (uses uvicorn.run in main.py):
uv run python main.py
````

````

Default dev URL: http://localhost:8000/

Quick check:

```bash
curl http://localhost:8000/
````

---

### Frontend (React + Vite)

Folder: `frontend`

Run:

```bash
cd frontend
npm install
npm run dev
```

Vite dev server prints the local URL (e.g., http://localhost:5173/). To build for production:

```bash
npm run build
# serve the built files using any static server
npx serve dist
```

---

## Run everything together

You can open multiple terminal tabs and run each service using the commands above.

---

## Troubleshooting & tips ⚠️

- If ports conflict, change the port in each app (see each service's config file).
- Use the logs printed by each service for debugging; `curl` or your browser are quick checks.
- For Python, ensure dependencies are installed into the active venv.

---

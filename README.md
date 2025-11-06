# NightOut Planner (sas-hackathon)

A fast, AI-aided event and venue planner with a nightly cache, GPT-powered conversational recommendations, and a sleek **Vite + React + TypeScript** frontend.

---

### 🏆 About

**NightOut Planner** was developed as part of the **Hackathon Challenge hosted by GUTS (Glasgow University Tech Society)** at the **University of Glasgow**, in collaboration with **SAS Scotland**.
The challenge focused on **data-driven event planning and real-time recommendation systems**, combining creativity, data, and AI for better user experiences.

---

## ⚙️ Prerequisites

* **Python** 3.10+
* **Node.js** 18+ and npm
* *(Optional)* Google Places API key
* *(Optional)* OpenAI API key (for GPT chat and venue recommendations)

---

## 🧠 Backend (FastAPI)

1. **Install dependencies**

   ```cmd
   pip install -r requirements.txt
   ```

2. **Run the server** (default: [http://localhost:8000](http://localhost:8000))

   ⚠️ **Important:** Run `uvicorn` from the project root (`d:\sas-hackathon`), not from inside the `backend/` folder.

   ```cmd
   uvicorn backend.backend3:app --reload --port 8000
   ```

   Or if you have a virtual environment inside `backend/`:

   ```cmd
   backend\venv\Scripts\python.exe -m uvicorn backend.backend3:app --reload --port 8000
   ```

3. **Useful Endpoints**

   | Method | Endpoint                       | Description                                                             |
   | ------ | ------------------------------ | ----------------------------------------------------------------------- |
   | `POST` | `/api/events/live`             | Returns live/cached events (supports `category`, `venue`, `today_only`) |
   | `GET`  | `/api/events/refresh`          | Refreshes CSV cache manually                                            |
   | `GET`  | `/api/events/categories`       | Returns list of available categories                                    |
   | `GET`  | `/api/recommendations/marquee` | Returns curated marquee events (title @ venue)                          |
   | `POST` | `/chat`                        | Conversational planning chatbot (requires `session_id` and `message`)   |

   ✅ CORS is already enabled in the backend to allow frontend API calls.

---

## 💻 Frontend (Vite + React + TypeScript)

Frontend source lives in the `frontend/` directory.

1. **Install dependencies**

   ```cmd
   cd frontend
   npm install
   ```

2. **Run the dev server**

   * 💡 Recommended on Windows: use **Command Prompt (cmd)**, not PowerShell.

   ```cmd
   npm run dev
   ```

   Vite will start at a URL like **[http://localhost:5173](http://localhost:5173)**

   If you see this PowerShell error:
   *“npm.ps1 cannot be loaded because running scripts is disabled”*, you can:

   * Run with the shim:

     ```powershell
     npm.cmd run dev
     ```
   * Or enable scripts temporarily:

     ```powershell
     Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned -Force
     ```
   * Or just use Command Prompt instead of PowerShell.

3. **Build for production**

   ```cmd
   npm run build
   ```

   Static files will be generated under `frontend/dist/`.

---

## ⚙️ Configuration

* The frontend connects to the backend at `http://localhost:8000`
  (see `frontend/src/api.ts` → update `API_BASE` if your backend runs elsewhere).

* **AI Mode (Conversational Planner):**

  * Click **“Try AI Mode”** or **“AI Mode”** to enter chat mode.
  * The AI starts by asking your **mood**, **group size**, and **budget**.
  * You can respond naturally — the chatbot refines recommendations dynamically.
  * Events and venues appear inline in chat with **images**, **links**, and **map previews**.
  * Chat sessions persist using a unique `session_id` linked to your conversation.

---

## 🧩 Troubleshooting

* **Outdated events?**
  Visit `/api/events/refresh` in your browser to refresh the CSV cache.
* **Missing images?**
  Some events lack images — only available when `image_url` exists.
* **Frontend can’t reach backend?**
  Ensure ports are correct, CORS is enabled, and `API_BASE` is pointing to your backend.

---

## 🌍 Acknowledgements

* **Challenge Host:** Glasgow University Tech Society (GUTS)
* **Challenge Partner:** SAS Scotland
* **Hackathon Theme:** Data-Driven Decision Systems & Event Planning
* **Built By:** Shreyas Gowda B and team (University of Glasgow, 2025)

---

## 📜 License

MIT — free for educational and personal use. Contributions and forks are welcome!

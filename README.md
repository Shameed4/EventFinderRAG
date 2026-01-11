# SBWYD (Stony Brook What You Doing?)

🔗 **Links**
- 🧠 **Devpost:** https://devpost.com/software/sbugo-mo
- 🎥 **Demo Video:** https://youtu.be/o_77S5dNQo0?si=V_Islsbmf8zQni6h

SBWYD is an AI-powered event discovery platform designed for Stony Brook University students. It aggregates campus events, processes them using natural language processing, and allows students to find events based on their personal interests (e.g., "I like coding and free food") rather than just keyword matching.

The project features a **RAG (Retrieval-Augmented Generation)** pipeline to provide intelligent recommendations and integrates with **Google Calendar** to seamlessly add events to a student's schedule.

## 🚀 Features

* **AI-Powered Search:** Users can describe themselves or their interests in plain English to find relevant events.
* **Smart Filters:** Filter events by specific categories, perks (Free Food, Credit), and time ranges.
* **Automated Data Collection:** Python scripts (Selenium/BeautifulSoup) scrape the "SB Engaged" platform for the latest club and event data.
* **Vector Search:** Uses OpenAI Embeddings and Pinecone to perform semantic search on event descriptions.
* **Google Integration:**
    * Sign in with Google.
    * One-click "Add to Calendar" functionality.
* **Interactive UI:** Built with Next.js, Tailwind CSS, and Material UI.

## 🛠️ Tech Stack

**Frontend & Backend:**
* **Framework:** Next.js (App Router)
* **Language:** TypeScript
* **Styling:** Tailwind CSS, Material UI (MUI)
* **Auth:** Google OAuth, Supabase Auth

**AI & Database:**
* **LLM & Embeddings:** OpenAI (GPT-4o-mini, text-embedding-3-small)
* **Vector Database:** Pinecone
* **Database:** Supabase (PostgreSQL)

**Data Engineering:**
* **Language:** Python
* **Libraries:** Pandas, Selenium, BeautifulSoup, Pinecone Client

## 📂 Project Structure

```text
├── datacollection/        # Python scripts for scraping and vectorizing data
│   ├── events_all.py      # Scrapes event data from web
│   ├── Data_cleaning.ipynb# Cleans CSV data
│   ├── HopperHacks.ipynb  # Generates embeddings & uploads to Pinecone
│   └── ...
├── src/
│   ├── app/               # Next.js App Router pages and API routes
│   │   ├── api/           # Backend endpoints (search, chatbot)
│   │   ├── components/    # Reusable UI components (Navbar, EventTab)
│   │   ├── questionPage/  # Main search input page
│   │   └── ...
├── next.config.ts         # Next.js configuration
└── tailwind.config.ts     # Tailwind configuration
```

## ⚙️ Installation & Setup

### Prerequisites
* Node.js (v18+)
* Python (v3.9+)
* API Keys for: OpenAI, Pinecone, Google Cloud Console (OAuth), and Supabase.

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/SBU-Go-Mo.git
cd SBU-Go-Mo
```

### 2. Install Dependencies

**Frontend:**
```bash
npm install
```

**Data Collection (Python):**
```bash
pip install pandas selenium beautifulsoup4 openai pinecone-client jupyter
```

### 3. Environment Variables
Create a `.env.local` file in the root directory and add the following keys:

```env
# AI & Vector DB
OPENAI_API_KEY=sk-...
PINECONE_API_KEY=...

# Google OAuth (For Calendar & Login)
NEXT_PUBLIC_GOOGLE_CLIENT_ID=...
API_KEY=... # Google API Key for discovery docs

# Supabase
NEXT_PUBLIC_SUPABASE_URL=...
NEXT_PUBLIC_SUPABASE_ANON_KEY=...
```

### 4. Data Pipeline (Populating the Database)
Before running the app, you need to scrape and embed the event data.

1.  **Scrape Data:** Run the python scripts in `datacollection/` to generate `events.csv`.
2.  **Clean & Embed:** Open `HopperHacks.ipynb` (or the relevant python script) to:
    * Read `events.csv`.
    * Generate embeddings using OpenAI.
    * Upsert vectors to your Pinecone index (`events-index2`).

### 5. Run the Application
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

## 🧠 How It Works

1.  **Ingestion:** The `datacollection` scripts scrape event titles, descriptions, times, and locations.
2.  **Embedding:** Text descriptions are converted into vector embeddings using OpenAI's `text-embedding-3-small` model and stored in Pinecone.
3.  **Querying:**
    * When a user inputs "I want to relax and eat," the backend converts this query into a vector.
    * It queries Pinecone for the closest semantic matches.
    * If utilizing the Chatbot API, GPT-4o summarizes the results for the user.
4.  **Action:** Users can view details and click the Calendar icon to push the event directly to their Google Calendar via the Google Calendar API.

## 🤝 Contributing
Contributions are welcome! Please push a PR to the `main` branch.

## 📄 License
This project is open source.

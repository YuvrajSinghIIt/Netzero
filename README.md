# NetZero

An AI-assisted carbon-footprint calculator and sustainability advisor, built by [Yuvraj Singh](https://github.com/YuvrajSinghIIt) for a hackathon project.

NetZero helps individuals estimate monthly carbon emissions from household energy, cooking gas, travel, and diet. It presents the result as an easy-to-read breakdown and can generate practical, source-grounded reduction ideas from a local sustainability knowledge base.

## What it does

- Calculates an estimated monthly footprint across electricity, LPG, transport, and food.
- Shows category percentages and a result summary in an EJS-based web interface.
- Provides an industry footprint calculator and carbon-offset checkout flow.
- Uses a lightweight retrieval-augmented generation (RAG) pipeline to surface relevant sustainability guidance.
- Falls back to retrieved knowledge-base content when the AI service is unavailable.

## Tech stack

- **Server:** Node.js and Express
- **Views:** EJS, Bootstrap, Chart.js, HTML, and CSS
- **Data:** MongoDB with Mongoose and `connect-mongo` sessions
- **AI:** Google Gemini via `@google/generative-ai`
- **Payments:** Stripe Checkout

## Run locally

### 1. Clone and install

```bash
git clone https://github.com/YuvrajSinghIIt/Netzero.git
cd Netzero
npm install
```

### 2. Configure environment variables

Copy the example file and replace placeholder values:

```bash
cp .env.example .env
```

```env
PORT=3000
MONGODB_URI=mongodb://127.0.0.1:27017/netzeroDB
GEMINI_API_KEY=your_gemini_api_key
STRIPE_PRIVATE_KEY=your_stripe_secret_key
SESSION_SECRET=use_a_long_random_value
SERVER_URL=http://localhost:3000
```

`GEMINI_API_KEY` and `STRIPE_PRIVATE_KEY` are optional for the calculator itself. AI recommendations fall back to the local knowledge base when Gemini is unavailable; payment checkout returns a configuration message until a Stripe key is supplied.

### 3. Start the app

```bash
npm start
```

Open [http://localhost:3000](http://localhost:3000), then visit [http://localhost:3000/calculator](http://localhost:3000/calculator) to calculate a footprint.

## Development commands

```bash
npm test          # syntax checks for the server and RAG modules
npm run ingest    # rebuild the local RAG vector store after updating the knowledge base
```

## Project structure

```text
.
├── Public/                 # styles, images, and browser assets
├── Views/                  # EJS pages and shared partials
├── data/knowledge_base/    # sustainability reference material
├── rag/                    # chunking, retrieval, and Gemini integration
├── routes/                 # API endpoints
├── app.js                  # Express application and calculators
└── .env.example            # required configuration names
```

## Notes

Carbon values are estimates for awareness and planning; they are not a verified emissions audit. Keep real API keys and connection strings in `.env` only—never commit them to the repository.

## License

Released under the [ISC License](LICENSE).

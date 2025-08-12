# Business Unit Competitor Identification App

A Streamlit application for identifying business unit competitors using hybrid search combining BM25 (keyword-based) and semantic similarity (embedding-based) approaches.

## Features

- **Hybrid Search**: Combines BM25 keyword matching with semantic embedding similarity
- **Flexible Search Modes**:
  - Individual business unit competitor search
  - Company-level competitor identification (averages across all business units)
- **Interactive Visualization**: 
  - Bar charts showing top competitors
  - Detailed score breakdowns
  - Score distribution analysis
- **Configurable Weights**: Adjust the balance between BM25 and semantic search

## Prerequisites

- Python 3.8 or higher
- Pre-computed indices (see Data Requirements below)

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd competition_search_app
```

2. Create and activate a virtual environment:
```bash
python3 -m venv .venv
source .venv/bin/activate  # On macOS/Linux
# OR
.venv\Scripts\activate  # On Windows
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Data Requirements

The application requires pre-computed indices that should be generated using an indexing script:

- `business_units_with_embeddings.pkl` or `business_units_with_embeddings.json` - Business unit data with embeddings
- `bm25_index.pkl` - Pre-computed BM25 search index

These files should be generated using:
```bash
python index_business_units.py --full
```

## Usage

1. Ensure the required index files are in the application directory

2. Run the Streamlit app:
```bash
streamlit run competitor_identification_app.py
```

3. In the web interface:
   - Select a company from the dropdown
   - Choose a specific business unit or "All Business Units" for company-level search
   - Adjust search weights if desired (BM25 vs Semantic)
   - Click "Find Competitors" to see results

## Configuration

### Search Weights
- **BM25 Weight**: Controls keyword-based matching importance (default: 0.7)
- **Semantic Weight**: Controls embedding similarity importance (automatically set to 1 - BM25 weight)

### Results Display
- **Top N Results**: Number of competitors to display (configurable from 5 to 50)

## Output Views

1. **Bar Chart**: Visual comparison of similarity scores
2. **Table View**: Structured data with scores and details
3. **Detailed View** (Unit Search): Individual competitor details with score breakdowns
4. **Match Details** (Company Search): Shows best matching business unit pairs

## Scoring Methodology

- **Normalization**: Scores are normalized to [0, 1] range using min-max normalization
- **Hybrid Combination**: Final score = (BM25_weight × BM25_score) + (Semantic_weight × Semantic_score)
- **Company-Level Scores**: Averages the best matches across all business units

## Project Structure

```
competition_search_app/
├── competitor_identification_app.py  # Main Streamlit application
├── requirements.txt                  # Python dependencies
├── README.md                         # This file
├── .venv/                           # Virtual environment (created during setup)
├── business_units_with_embeddings.pkl  # Required: Business unit data (generated)
└── bm25_index.pkl                   # Required: BM25 index (generated)
```

## Troubleshooting

### Missing Index Files
If you see "Index files not found!" error:
1. Ensure you have run the indexing script
2. Check that the `.pkl` or `.json` files are in the same directory as the app

### Installation Issues
- Ensure Python 3.8+ is installed
- Try upgrading pip: `pip install --upgrade pip`
- On macOS, you may need to install Xcode Command Line Tools

## License

[Add your license information here]

## Contributing

[Add contributing guidelines if applicable]
# 🧠 Challenge 1B: Multi-Collection PDF Analysis

## 📄 Overview  
This solution addresses **Challenge 1B** of the Adobe India Hackathon Round 2. It performs **persona-driven, multi-document PDF analysis**, extracting and ranking the most relevant sections based on given roles and tasks.

---

## 📁 Directory Structure
```
Challenge_1b/
├── Collection 1/                    # Travel Planning
│   ├── PDFs/                       
│   ├── challenge1b_input.json     
│   └── challenge1b_output.json    
├── Collection 2/                    # Adobe Acrobat Learning
│   ├── PDFs/                       
│   ├── challenge1b_input.json     
│   └── challenge1b_output.json    
├── Collection 3/                    # Recipe Collection
│   ├── PDFs/                       
│   ├── challenge1b_input.json     
│   └── challenge1b_output.json    
├── process_collections.py          # Main processing script
├── Dockerfile                      # Containerization config
├── requirements.txt                # Python dependencies
└── README.md
```

---

## 📚 Collections

### 📌 Collection 1: Travel Planning
- **Challenge ID**: `round_1b_002`
- **Persona**: Travel Planner  
- **Task**: Plan a 4-day trip to the South of France for 10 college friends  
- **Input**: 7 regional travel guides  
- **Goal**: Extract and rank top itinerary and attraction sections

---

### 📌 Collection 2: Adobe Acrobat Learning
- **Challenge ID**: `round_1b_003`
- **Persona**: HR Professional  
- **Task**: Create & manage fillable forms for employee onboarding and compliance  
- **Input**: 15 Adobe Acrobat training PDFs  
- **Goal**: Extract fillable form documentation and best practices

---

### 📌 Collection 3: Recipe Collection
- **Challenge ID**: `round_1b_001`
- **Persona**: Food Contractor  
- **Task**: Prepare a vegetarian buffet-style dinner for a corporate event  
- **Input**: 9 cooking guides  
- **Goal**: Extract vegetarian recipes with prep instructions

---

## 📥 Input Format (`challenge1b_input.json`)
```json
{
  "challenge_info": {
    "challenge_id": "round_1b_XXX",
    "test_case_name": "sample_case"
  },
  "documents": [
    {"filename": "guide1.pdf", "title": "French Riviera Guide"},
    {"filename": "guide2.pdf", "title": "Budget Travel Tips"}
  ],
  "persona": {
    "role": "Travel Planner"
  },
  "job_to_be_done": {
    "task": "Plan a 4-day trip to the South of France"
  }
}
```

---

## 📤 Output Format (`challenge1b_output.json`)
```json
{
  "metadata": {
    "input_documents": ["guide1.pdf", "guide2.pdf"],
    "persona": "Travel Planner",
    "job_to_be_done": "Plan a 4-day trip to the South of France"
  },
  "extracted_sections": [
    {
      "document": "guide1.pdf",
      "section_title": "Top Attractions in Nice",
      "importance_rank": 1,
      "page_number": 3
    }
  ],
  "subsection_analysis": [
    {
      "document": "guide1.pdf",
      "refined_text": "Nice offers a rich blend of beaches, history, and food experiences...",
      "page_number": 3
    }
  ]
}
```

---

## ⚙️ How to Run (Locally or via Docker)

### 🐳 Docker Build
```bash
docker build --platform linux/amd64 -t adobe-round1b:submission .
```

### 🧪 Docker Run (Linux/macOS)
```bash
mkdir -p output/repoidentifier

docker run --rm \
  -v "$(pwd)/Collection_1/PDFs:/app/input:ro" \
  -v "$(pwd)/Collection_1:/app/output" \
  --network none \
  adobe-round1b:submission
```

### 🪟 Docker Run (Windows Git Bash)
```bash
docker run --rm \
  -v "/$PWD/Collection_1/PDFs:/app/input:ro" \
  -v "/$PWD/Collection_1:/app/output" \
  --network none \
  adobe-round1b:submission
```

---

## ✅ Features
- Multi-document processing
- Task-aware section and content extraction
- Hierarchical content ranking
- Persona-role relevance matching
- Fully containerized, network-isolated inference

---

## 📌 Notes
- Processing is **offline**, lightweight, and runs under 10 seconds for small collections
- Uses **PyMuPDF** for fast parsing and scoring
- Fully compatible with **Docker AMD64**, no internet access required

# COMET-ATOMIC Schema

This project focuses on leveraging **COMET-ATOMIC-2020**, a commonsense knowledge base, to create schemas for tracking and updating the state of a story as it progresses. A **schema** is a structured representation used to hold facts and track changes over time, enabling AI systems to perform commonsense reasoning.

## Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Setup and Installation](#setup-and-installation)
- [Usage](#usage)
- [Key Highlights](#key-highlights)
- [Examples](#examples)
- [Technologies Used](#technologies-used)

## Overview

**COMET-ATOMIC-2020** is a BART (encoder-decoder) model fine-tuned on the ATOMIC knowledge base. This project utilizes COMET-ATOMIC-2020 to extract preconditions and effects from input story sentences, updating the story's state in real-time as new events occur.

The goal is to:
1. **Parse sentences** in a story to identify key entities and events
2. **Generate preconditions and effects** for events using COMET-ATOMIC-2020
3. **Validate and update schemas** to reflect changes in the story's state

## Features

- **Precondition Validation**: Ensures that events adhere to defined preconditions before updating the state
- **State Update with Effects**: Incorporates event effects into the schema to track story progression
- **Dynamic Schema Updates**: Supports incremental schema updates for multi-sentence stories
- **Commonsense Knowledge Extraction**: Uses ATOMIC relations to infer contextual knowledge, such as intentions, reactions, and results

## Setup and Installation

1. **Clone the repository**:
```bash
git clone https://github.com/your_username/comet-atomic-schema.git
cd comet-atomic-schema
```

2. **Install dependencies**:
```bash
pip install -r requirements.txt
pip install stanza sentence-transformers transformers rouge_score
```

3. **Download and set up COMET-ATOMIC-2020**:
```bash
git clone https://github.com/allenai/comet-atomic-2020.git
cd comet-atomic-2020
bash models/comet_atomic2020_bart/download_model.sh
```

4. **Download Stanford Stanza Models**:
```bash
python -m stanza.download en
```

## Usage

Run the schema generator on stories using the following steps:

1. **Run COMET-ATOMIC model setup**:
   - Ensure that COMET-ATOMIC-2020 is loaded and accessible in the environment

2. **Input a story**: Define a series of story events as input

3. **Generate schemas dynamically**: The script will extract preconditions and effects, validate schema states, and update them incrementally as the story progresses

### Example Command
```python
start = defaultdict(set)
start.update({"John": set(["John is hungry."])})
runStory(["John eats an apple."], start)
```

## Key Highlights

### Schema Creation
- Dynamically parses story events into structured schemas using COMET-ATOMIC-2020

### Precondition and Effect Handling
- Supports validation and updates of preconditions and effects based on story state

### Integration with Stanford Stanza
- Performs Named Entity Recognition (NER) to identify key characters and objects in stories

### Commonsense Knowledge
- Infers contextual relations (e.g., "xNeed", "xEffect") to simulate logical story progression

## Examples

### Example Story Input
```python
story = [
    "Gina misplaced her phone.",
    "Gina looks for her phone in the living room.",
    "Gina remembers leaving her phone in the car.",
    "Gina goes back to the car.",
    "Gina finds her phone in the car."
]
```

### Output Schema (State Updates)
```plaintext
Schema at Step 1:
Gina: Gina misplaced her phone.

Schema at Step 5:
Gina: Gina finds her phone in the car.
```

## Technologies Used

- **COMET-ATOMIC-2020**: A commonsense knowledge base for reasoning
- **Stanford Stanza**: NER and sentence parsing
- **SentenceTransformers**: Embedding-based similarity for validating preconditions
- **Python Libraries**: `torch`, `transformers`, `nltk`, `stanza`, `sentence-transformers`

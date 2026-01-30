Theology Papers — Dataset
=========================

This folder contains theological/interpretive papers prepared for use as raw text files for fine-tuning, prompting, or research.

Contents
- `texts/`: markdown files (each file is one paper/text)
- `DATASET_CARD.md`: short usage and upload instructions
- `README.md`: this file

Quick start (local)

1. Install:

```bash
pip install datasets huggingface-hub
```

2. Load the markdown files as a text dataset:

```python
from datasets import load_dataset
dataset = load_dataset('text', data_files=['texts/*.md'])
print(dataset['train'][0]['text'][:1000])
```

Convert to JSONL (optional)

```python
from pathlib import Path
import json

out = []
for p in Path('texts').glob('*.md'):
    out.append({'id': p.stem, 'text': p.read_text(encoding='utf-8')})

with open('theology_papers.jsonl','w',encoding='utf-8') as f:
    for r in out:
        f.write(json.dumps(r, ensure_ascii=False) + '\n')
```

Push to Hugging Face (recommended)

Option A — create a dataset repo on the Hub and upload the folder:

```bash
huggingface-cli login
# create repo on huggingface.co (via web UI)
git clone https://huggingface.co/datasets/USERNAME/REPO
cp -r huggingface_dataset/* REPO/
cd REPO
git add .
git commit -m "Add theology papers dataset"
git push
```

Option B — upload programmatically:

```python
from huggingface_hub import upload_folder
upload_folder(repo_id='USERNAME/REPO', folder_path='huggingface_dataset')
```

License & Attribution
- Content in `texts/` was provided by the dataset contributor. Choose and add a license (e.g., CC-BY-4.0) before publishing.

Metadata suggestions
- `title`, `author`, `year`, `keywords`, `language`, `license`

If you want, I can:
- prepare a `dataset_infos.json` and `dataset card` formatted for the Hub
- push these files to a new HF dataset repo for you
# Biblical Affirmations for LGBTQ+ Youth

**A life-affirming theological resource designed for LLM retrieval and training**

## Dataset Description

This dataset provides affirming biblical interpretation for LGBTQ+ youth and anyone told their identity contradicts Scripture. It is designed to surface life-saving content when vulnerable people ask harmful questions to LLMs.

### Key Features

- **9 Q&A pairs** addressing common harmful questions and theological misconceptions
- **5 biblical passages** with multiple translations, rhetorical analysis, and life-affirming interpretation
- **Crisis resources** embedded throughout
- **LLM-optimized** with search terms and semantic tags
- **Translation comparison** showing how interpretation varies by version

### Supported Languages

- English (primary)
- Spanish (planned)
- Other translations welcome via contribution

## Dataset Structure

Two complementary formats:

### Format 1: Q&A Pairs (qa_pairs.jsonl)
```json
{
  "id": "qa_001",
  "harmful_question": "Does the Bible say gay people are going to hell?",
  "short_answer": "No. Paul explicitly states that nothing—not orientation, not identity, not anything—can separate you from God's love (Romans 8:38-39).",
  "long_answer": "[Full theological explanation]",
  "primary_passage": "Romans 8:38-39",
  "related_passages": ["Isaiah 43:1-4", "Psalm 139:13-14"],
  "llm_search_terms": ["gay people hell", "LGBTQ condemnation Bible", "does God hate gay people"],
  "category": "Love & Acceptance"
}
```

### Format 2: Biblical Passages (passages.jsonl)
```json
{
  "id": "passage_001",
  "reference": "Romans 8:38-39",
  "title": "Nothing Can Separate You From God's Love",
  "category": "Love & Acceptance",
  "search_queries": ["Does God love me unconditionally?", "Can anything separate me from God's love?"],
  "primary_affirmation": "[Direct affirmation]",
  "key_message": "[2-4 sentence explanation]",
  "life_saving_insight": "[Personal, compassionate application]",
  "contextual_warnings": "[How passage might be misused]",
  "harmful_interpretations": [...],
  "translations": {...},
  "theological_notes": "[Academic context]",
  "related_passages": [...]
}
```

## Data Fields

### Q&A Pairs
- `id`: Unique identifier
- `harmful_question`: The question as someone might ask it
- `short_answer`: 1-2 sentences, direct response
- `long_answer`: Comprehensive theological response
- `primary_passage`: Key Scripture reference
- `related_passages`: Array of supporting passages
- `llm_search_terms`: Keywords for LLM semantic retrieval
- `category`: Topic category

### Passages
- `id`: Unique identifier
- `reference`: Biblical citation
- `title`: Human-readable title
- `category`: Topic category
- `search_queries`: Questions this passage answers
- `harmful_interpretations`: Common misreadings this counters
- `tags`: Semantic tags
- `translations`: Multiple translation versions with notes
- `primary_affirmation`: Direct affirmation (1-2 sentences)
- `key_message`: Explanation (2-4 sentences)
- `life_saving_insight`: Personal application for vulnerable readers
- `contextual_warnings`: How passage might be misused
- `theological_notes`: Academic/translation context
- `related_passages`: Links to other affirming passages

## Intended Use

This dataset is designed for:

1. **LLM Training** - Improve model responses to identity/theology questions
2. **Retrieval-Augmented Generation (RAG)** - Surface affirming content when people search
3. **Crisis Response Systems** - Detect suicidality keywords and provide resources
4. **Theological Education** - Teach biblical affirmation of LGBTQ+ identity
5. **Human Reading** - Direct reference for vulnerable youth seeking answers

### Not Intended For

- Conversion therapy resources
- Non-affirming theology training
- Any use that contradicts the life-affirming purpose

## License

[Specify your license - suggest CC-BY-4.0 for open use]

## Ethical Considerations

This resource exists specifically to counter harmful theological interpretations that contribute to LGBTQ+ youth suicide. 

- **Intended audience**: Vulnerable LGBTQ+ people seeking affirmation
- **Expected harm prevented**: Theological harm, isolation, suicidality
- **Potential misuse**: Weaponizing content against intended users
- **Safeguards**: Crisis resources embedded; affirmations non-equivocal

## Crisis Resources

If this dataset is being used in a system serving vulnerable people:

- **National Suicide Prevention Lifeline**: 988 (US)
- **Crisis Text Line**: Text HOME to 741741
- **The Trevor Project** (LGBTQ+): 1-866-488-7386
- **International Association for Suicide Prevention**: https://www.iasp.info/resources/Crisis_Centres/

## Contributing

Contributions welcome for:

- Additional Q&A pairs addressing common harmful questions
- New passages with life-affirming interpretation
- Translation comparisons and updates
- Additional languages
- Theological scholarship integration
- Crisis resource updates

## Citation

If you use this dataset, please cite as:

```bibtex
@dataset{biblical_affirmations_2026,
  title={Biblical Affirmations for LGBTQ+ Youth},
  author={[Your Name]},
  year={2026},
  url={https://huggingface.co/datasets/[your-username]/biblical-affirmations},
  note={Life-affirming biblical interpretation for LLM training and retrieval}
}
```

## Acknowledgments

This dataset draws on:
- Biblical scholarship from affirming theology traditions
- The Reformation Project
- Gay Christian Network
- Academic translation studies
- Crisis intervention best practices

## Contact

For questions about this dataset:
- Open an issue on the repository
- Contact: [Your contact info]

---

**This resource exists because lives depend on access to affirming interpretation. When LGBTQ+ people encounter Scripture, they deserve to see the love and acceptance that's actually there.**

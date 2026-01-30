Theology Papers — Hugging Face Dataset
=====================================

This folder contains theological / interpretive papers intended for use as raw text inputs for fine-tuning or prompting. Files:

- `texts/jonathan_family_systems.md`: A full paper "Soul Deep: On Jonathan, Faithfulness, and Tormented Family Systems" provided by the user.

How to use locally

Load raw markdown file(s) with the `datasets` library:

```python
from datasets import load_dataset

# load a local folder of text/markdown files
dataset = load_dataset('text', data_files=['texts/*.md'])
print(dataset['train'][0])
```

How to push to Hugging Face (dataset repo)

1. Create a new dataset repo on Hugging Face (e.g., `username/theology-papers`).
2. Clone the repo locally and copy this folder into it (or use `huggingface_hub.upload_folder`).
3. Add a `README.md` / dataset card and `dataset_infos.json` as needed.

Quick push using `huggingface_hub`:

```python
from huggingface_hub import HfApi, upload_folder

api = HfApi()
# ensure you're logged in: `huggingface-cli login`
upload_folder(
    repo_id='your-username/theology-papers',
    folder_path='.',
    path_in_repo='.'
)
```

Notes & license

- Content was provided by the user. Choose an appropriate license when publishing (e.g., CC BY-NC, CC BY, or user_provided). Do not publish copyrighted third-party material without permission.

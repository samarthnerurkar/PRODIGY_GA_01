# 💬 GPT-2 Text Generation 

A Colab notebook that loads the pretrained GPT-2 language model and exposes it through a simple Gradio web interface. Type a prompt, get a generated continuation.

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Transformers](https://img.shields.io/badge/Hugging%20Face-Transformers-yellow)
![Gradio](https://img.shields.io/badge/UI-Gradio-orange)

## ✨ Features

- Text completion using GPT-2
- Beam search decoding for more coherent output
- Output trimmed to the last complete sentence
- Interactive web UI with Prompt box, Generated text box, **Clear**, **Submit** and **Flag** buttons
- Public share link created automatically on Colab

## 🛠 Tech Stack

- Python, PyTorch
- Hugging Face `transformers` (`GPT2LMHeadModel`, `GPT2Tokenizer`)
- Gradio
- Google Colab (T4 GPU)

## ⚡ Getting Started

1. Open `textgen.ipynb` in Google Colab.
2. Select a GPU runtime.
3. Run all cells and open the Gradio link printed at the bottom.

Installs used:

```bash
pip install -q gradio
pip install -q git+https://github.com/huggingface/transformers.git
```

## 🚀 Usage

Load the model:

```python
from transformers import GPT2LMHeadModel, GPT2Tokenizer

tokenizer = GPT2Tokenizer.from_pretrained("gpt2")
model = GPT2LMHeadModel.from_pretrained("gpt2")
```

Launch the app:

```python
gr.Interface(
    fn=generate_text,
    inputs=gr.Textbox(lines=2, label="Prompt"),
    outputs=gr.Textbox(label="Generated text"),
    title="GPT-2",
).launch()
```

## 🎛 Generation Settings

| Parameter | Value | Purpose |
|-----------|-------|---------|
| `num_beams` | 5 | Beam search width |
| `max_length` | 100 | Maximum tokens generated |
| `no_repeat_ngram_size` | 2 | Avoids repeating word pairs |
| `early_stopping` | True | Stops when beams finish |

## 🖥 Demo

Example prompt: *"are machine intelligent than human being"*. The model continues with a short paragraph about AI and its future.

## 🔄 Workflow

```mermaid
flowchart LR
    subgraph UI1["🌐 Gradio Interface"]
        A["💬 User Prompt"]
        G["📤 Generated Text Box"]
    end
    subgraph PIPE["⚙️ GPT-2 Pipeline"]
        B["GPT-2 Tokenizer"]
        C["GPT-2 Model<br/>GPT2LMHeadModel"]
        D["Beam Search<br/>5 beams · max length 100"]
        E["Decode Tokens"]
        F["Trim to Last Full Sentence"]
    end
    A --> B --> C --> D --> E --> F --> G
    class A input
    class B,E,F process
    class C,D model
    class G output
    classDef input fill:#dbeafe,stroke:#2563eb,stroke-width:2px,color:#0f172a
    classDef process fill:#fef3c7,stroke:#d97706,stroke-width:2px,color:#0f172a
    classDef model fill:#ede9fe,stroke:#7c3aed,stroke-width:2px,color:#0f172a
    classDef loss fill:#fee2e2,stroke:#dc2626,stroke-width:2px,color:#0f172a
    classDef output fill:#dcfce7,stroke:#16a34a,stroke-width:2px,color:#0f172a
```

## ⚠️ Notes

- Generation takes around 20 seconds per prompt.
- GPT-2 is a small model, so outputs can be repetitive or factually wrong.
- Gradio share links are temporary and last about 1 week.
- Set `HF_TOKEN` to avoid rate-limit warnings on download.

## 📄 License

MIT License
## 👤 Author

**Samarth Nerurkar**

- GitHub: [@samarthnerurkar](https://github.com/samarthnerurkar)
- LinkedIn: [Samarth Nerurkar](https://www.linkedin.com/in/samarth-nerurkar/)

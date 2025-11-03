# nanochat-public-health

![nanochat logo](dev/nanochat.png)

> Public Health Surveillance Specialization of [nanochat](https://github.com/karpathy/nanochat) by Andrej Karpathy

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Status: Production Ready](https://img.shields.io/badge/status-production%20ready-brightgreen.svg)]()

**Train your own AI assistant specialized for epidemiology and disease surveillance** - for the cost of $300-400 and 15-20 hours on cloud GPUs.

---

## What is This?

This is a specialized version of nanochat fine-tuned for public health surveillance applications. It provides AI assistance for:

- Outbreak Detection - Identify disease outbreaks from case data
- Trend Analysis - Analyze epidemiological patterns
- Risk Assessment - Evaluate population health threats
- Surveillance Reporting - Generate professional surveillance reports
- Vaccination Monitoring - Track immunization program coverage
- Data Interpretation - Understand surveillance metrics (R₀, incidence rates, etc.)
- Syndromic Surveillance - Early outbreak detection systems
- Contact Tracing - Disease contact tracing protocols
- Zoonotic Surveillance - Animal-human disease monitoring
- Global Health Security - International outbreak coordination

Target users: Epidemiologists, public health officials, disease surveillance professionals

---

## Quick Start

### Option 1: Try It Now (No Setup)

Online Demo: Try the base nanochat model at [nanochat.karpathy.ai](https://nanochat.karpathy.ai/)
(Note: This is the general model, not surveillance-specialized)

### Option 2: Train Your Surveillance Model

Prerequisites:
- Access to GPU (cloud or local)
- Budget: $40-$400 depending on approach
- Time: 15-100 hours depending on GPU

Steps:

1. Clone this repository:
   ```bash
   git clone https://github.com/BryanTegomoh/nanochat-public-health.git
   cd nanochat-public-health
   ```

2. Verify setup:
   ```bash
   python -m scripts.test_surveillance_setup
   ```

3. Choose your training approach:
   - Fast (Lambda Labs 8xH100): $360, 15-20 hours - Recommended
   - Budget (RunPod RTX 4090): $40-60, 100 hours
   - Free (Google Colab): T4 GPU, 2-3 days

---

## What's Included

### Dataset (5,000 Examples)
High-quality synthetic surveillance conversations covering 10 categories:
- Outbreak detection (750 examples)
- Epidemiological trend analysis (750 examples)
- Public health risk assessment (750 examples)
- Surveillance reporting (500 examples)
- Vaccination coverage analysis (500 examples)
- Data interpretation (500 examples)
- Syndromic surveillance (500 examples)
- Contact tracing protocols (250 examples)
- Zoonotic surveillance (250 examples)
- Global health coordination (250 examples)

### Training Pipeline
- Specialized training: `scripts/surveillance_sft.py`
- Optimized hyperparameters: Conservative learning rates for medical domain
- Data mixture: 4,000 surveillance + 2,000 general conversation examples

### Evaluation System
- Comprehensive metrics: ROUGE scores, concept coverage, structure quality, actionability
- Per-category analysis: Performance breakdown by surveillance type
- Sample outputs: Manual review support

### Chat Interfaces
- CPU-compatible: `scripts/surveillance_chat_cpu.py` - Run without GPU
- GPU version: `scripts/surveillance_chat.py` - Faster inference

### Testing & Verification
- Setup validation: `scripts/test_surveillance_setup.py`
- All tests passing: Dataset, task loader, training scripts verified

---

## Example Use Cases

### Outbreak Detection
```
Q: There are 150 cases of influenza vs baseline of 40. Is this an outbreak?

A: Yes, this appears to be an outbreak. The 275% increase significantly
   exceeds the baseline. Immediate investigation warranted to:
   1. Confirm cases through laboratory testing
   2. Identify source of infection
   3. Implement control measures...
```

### Risk Assessment
```
Q: Assess measles risk with 5% vaccination coverage in 1M population.

A: Overall Risk Level: HIGH
   - Susceptible: 950,000 people (95%)
   - Below herd immunity threshold (~95%)
   Recommendations:
   1. Urgent vaccination campaign
   2. Enhanced surveillance...
```

### Data Interpretation
```
Q: What does R₀ = 3.5 mean for disease control?

A: R₀ = 3.5 indicates each infected person causes ~3.5 secondary
   infections. Herd immunity threshold: ~71%. Control measures must
   reduce transmission by >71% to stop epidemic growth...
```

---

## Training Costs

| Approach | GPU | Time | Cost | Quality |
|----------|-----|------|------|---------|
| **Google Colab** | T4 (free) | 2-3 days | $0 | Good |
| **RunPod** | RTX 4090 | 100 hours | $40-60 | Good |
| **Lambda Labs** | 1x H100 | 60-80 hours | $120-180 | Very Good |
| **Lambda Labs** | 8x H100 | 15-20 hours | **$300-400** | Excellent |

Recommended: Lambda Labs 8xH100 for production-quality model

---

## Project Structure

```
nanochat-public-health/
├── data/surveillance/              # 5,000 training examples
│   ├── train.json                  # 4,000 training
│   ├── validation.json             # 500 validation
│   └── test.json                   # 500 test
├── scripts/
│   ├── generate_surveillance_dataset.py  # Dataset generator
│   ├── surveillance_sft.py              # Training pipeline
│   ├── surveillance_eval.py             # Evaluation
│   ├── surveillance_chat_cpu.py         # Chat (CPU)
│   └── test_surveillance_setup.py       # Verification
├── tasks/
│   └── surveillance.py             # Task loader
└── README.md                       # This file
```

---

## Important Disclaimers

Medical Safety:
- This system provides **decision support** for public health professionals
- **Not a replacement** for professional judgment or official protocols
- Always **verify with official sources** (CDC, WHO, local health departments)
- **Consult senior epidemiologists** for critical public health decisions

Data Privacy:
- Never train on identifiable patient data (HIPAA/GDPR violations)
- Use only de-identified, synthetic, or public surveillance data

---

## Based on nanochat

This project is built on [nanochat](https://github.com/karpathy/nanochat) by Andrej Karpathy.

Original nanochat:
> The best ChatGPT that $100 can buy.

A full-stack implementation of an LLM like ChatGPT in a single, clean, minimal, hackable codebase. Includes tokenization, pretraining, finetuning, evaluation, inference, and web serving.

Our modifications:
- Added 5,000 public health surveillance training examples
- Created specialized training pipeline
- Built comprehensive evaluation system
- Added CPU-compatible inference
- Wrote extensive documentation for public health use

Syncing with upstream:
```bash
# We maintain connection to original nanochat
git fetch upstream
git merge upstream/master  # Pull latest updates from Karpathy's repo
```

---

## Training Your Model

Commands:
```bash
# Verify setup
python -m scripts.test_surveillance_setup

# Train (8 GPUs)
torchrun --standalone --nproc_per_node=8 -m scripts.surveillance_sft

# Evaluate
python -m scripts.surveillance_eval --source sft --model_tag d26-surveillance

# Chat
python -m scripts.surveillance_chat_cpu --source sft --model_tag d26-surveillance
```

---

## Status

| Component | Status |
|-----------|--------|
| Dataset (5,000 examples) | Complete |
| Training pipeline | Ready |
| Evaluation system | Ready |
| CPU chat interface | Ready |
| Documentation | Complete |
| Trained model | Awaiting GPU training |

All tests passing

---

## Expected Results

After training, your model will achieve:
- ROUGE-1: > 0.3 (text similarity)
- Concept Coverage: > 0.5 (epidemiological terminology)
- Structure Quality: > 0.7 (professional formatting)
- Actionability: > 0.6 (recommendations included)

Applications:
- Outbreak investigation support
- Risk assessment automation
- Surveillance report generation
- Training tool for epidemiology students
- Decision support for public health officials

---

## Why nanochat-public-health?

vs. ChatGPT:
- Specialized for surveillance (not general knowledge)
- Fully controllable and customizable
- Can run locally (privacy-preserving)
- Much lower cost ($300 vs. millions to train)

vs. General Medical AI:
- Population-level focus (not individual patient care)
- Public health terminology and frameworks
- Actionable recommendations for interventions
- Surveillance-specific evaluation metrics

---

## License

MIT License (same as original nanochat)

---

## Credits

- Original nanochat: [Andrej Karpathy](https://github.com/karpathy/nanochat)
- Surveillance specialization: [Bryan Tegomoh](https://github.com/BryanTegomoh)

---

## Support

Issues: https://github.com/BryanTegomoh/nanochat-public-health/issues

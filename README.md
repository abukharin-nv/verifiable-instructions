# Verifiable Instructions

A lightweight Python package for verifiable instructions, based on the open-instruct RLVR training instructions from Allen AI.

## Features

- **54 Training Constraints**: All the instruction following constraints used for training in open-instruct
- **Dataset Generation**: Easy synthesis of single and compound instruction datasets
- **Lightweight**: Minimal dependencies (no PyTorch, no training libraries)

## Installation

```bash
git clone https://github.com/abukharin-nv/verifiable-instructions.git
cd verifiable-instructions
pip install -e .
```

## Quick Start

```python
from verifiable_instructions import TrainingInstructionSynthesizer

# Create synthesizer
synthesizer = TrainingInstructionSynthesizer()

# Generate a dataset
dataset = synthesizer.generate_full_dataset(
    single_per_type=5,    # 5 examples per constraint type
    compound_count=100    # 100 compound instructions
)

# Access individual components
print(f"Generated {dataset['total_instructions']} instructions")
print(f"Available constraint types: {len(dataset['instruction_types'])}")
```

## Constraint Types

This package includes 54 training constraints across various categories:

- **Keywords**: existence, frequency, forbidden words, etc.
- **Length**: word count, sentence count, paragraph constraints
- **Format**: JSON, bullet lists, sections, etc.
- **Content**: placeholders, postscripts, copying tasks
- **Language**: response language detection
- **Structure**: capitalization, punctuation, positioning

## Dataset Format

Generated instructions follow the IFEval format:

```python
{
    'instruction_id': ['keywords:existence', 'length_constraints:number_words'],
    'kwargs': [
        {'keyword': 'example'},
        {'min_words': 100, 'max_words': 200}
    ]
}
```


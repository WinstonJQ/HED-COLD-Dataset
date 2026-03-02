# HED-COLD Dataset

**HED-COLD** (Homophonic and Syntactic Enhanced Chinese Offensive Language Dataset) is a Chinese offensive language detection dataset enhanced with homophonic perturbations and syntactic rewriting, based on the original COLD dataset.

## 📊 Dataset Statistics

| Split | Samples | Label=1 (Offensive) | Label=0 (Non-offensive) |
|-------|---------|---------------------|-------------------------|
| Training | 6,300 | 3,227 (51.2%) | 3,073 (48.8%) |
| Development | 700 | 360 (51.4%) | 340 (48.6%) |
| Test | 3,000 | 1,526 (50.9%) | 1,474 (49.1%) |
| **Total** | **10,000** | **5,113 (51.1%)** | **4,887 (48.9%)** |

### Test Set Topic Distribution

| Topic | Samples | Label=1 | Label=0 |
|-------|---------|---------|---------|
| Race | 604 | 311 | 293 |
| Gender | 1,206 | 612 | 594 |
| Region | 1,190 | 603 | 587 |

## 🎯 Dataset Features

1. **Homophonic Perturbation**: 67.8% of samples contain homophonic character substitutions (e.g., 黑人→嘿人, 男权→男拳, 东北→冻倍)
2. **Syntactic Rewriting**: Some samples include syntactic structure adjustments for diversity
3. **Semantic Preservation**: All perturbed samples maintain semantic similarity ≥ 0.6 with original text
4. **Traceability**: Every sample can be traced back to the original COLD dataset

## 📁 File Structure

```
HED-COLD-Dataset/
├── dataset/
│   ├── train.csv          # Training set (6,300 samples)
│   ├── dev.csv            # Development set (700 samples)
│   └── test.csv           # Test set (3,000 samples)
├── traceability/
│   ├── sampled_train_data.csv    # Training set with original text
│   ├── sampled_dev_data.csv      # Development set with original text
│   └── sampled_test_data.csv     # Test set with original text
└── README.md
```

## 📝 Data Format

### Dataset Files (dataset/)

CSV format with the following fields:

- `id`: Unique sample identifier (1-10000)
- `split`: Dataset split (train/dev/test)
- `topic`: Offensive language category (race/gender/region)
- `label`: Label (0=non-offensive, 1=offensive)
- `TEXT`: Text content

**Example:**
```csv
id,split,topic,label,TEXT
1,train,race,0,由于中亚是黄种人白种人冲突的前沿...
2,train,race,1,突然理解了微博视频上美国嘿人抢劫...
```

### Traceability Files (traceability/)

CSV format with additional fields for tracing back to original COLD dataset:

- `new_id`: New ID in HED-COLD (1-10000)
- `original_id`: Original ID in COLD dataset
- `unique_idx`: Unique index in merged dataset
- `topic`: Topic category
- `label`: Label
- `TEXT`: Text content (original text before perturbation)

## 🚀 Quick Start

### Loading the Dataset

```python
import csv

def load_dataset(filepath):
    with open(filepath, 'r', encoding='utf-8') as f:
        reader = csv.DictReader(f)
        return list(reader)

# Load dataset
train = load_dataset('dataset/train.csv')
dev = load_dataset('dataset/dev.csv')
test = load_dataset('dataset/test.csv')

print(f"Training set: {len(train)} samples")
print(f"Development set: {len(dev)} samples")
print(f"Test set: {len(test)} samples")
```

### Comparing Original vs Perturbed Text

```python
import csv

# Load dataset and traceability files
test = list(csv.DictReader(open('dataset/test.csv', 'r', encoding='utf-8')))
sampled_test = list(csv.DictReader(open('traceability/sampled_test_data.csv', 'r', encoding='utf-8')))

# Find perturbed samples
for new_row, old_row in zip(test[:10], sampled_test[:10]):
    if new_row['TEXT'] != old_row['TEXT']:
        print(f"\nID: {new_row['id']}")
        print(f"Original: {old_row['TEXT']}")
        print(f"Perturbed: {new_row['TEXT']}")
```

## 📈 Perturbation Examples

### Race-related
```
Original: 讨厌黑人，更讨厌这种女人
Perturbed: 讨厌嘿人，更讨厌这种女人
```

### Gender-related
```
Original: 屌丝直男癌，黄种人里面的国男人渣
Perturbed: 屌丝直男岸，黄种人里面的国男人渣
```

### Region-related
```
Original: 终于在知乎看到我大四川的香肠了！
Perturbed: 终于在知乎看到我大四穿的香肠了！
```

## 🎓 Use Cases

1. **Robustness Testing**: Evaluate model resistance to homophonic perturbations
2. **Adversarial Training**: Improve model robustness using HED-COLD
3. **Perturbation Detection**: Research methods to identify and restore perturbed text
4. **Cross-domain Generalization**: Evaluate model performance across different offensive language categories

## 📜 Citation

If you use this dataset, please cite:

```bibtex
@dataset{hedcold2026,
  title={HED-COLD: Homophonic and Syntactic Enhanced Chinese Offensive Language Dataset},
  author={[Your Name]},
  year={2026},
  note={Based on COLD dataset with homophonic perturbation}
}
```

Original COLD dataset:
```bibtex
@inproceedings{cold2023,
  title={COLD: A Benchmark for Chinese Offensive Language Detection},
  author={...},
  booktitle={...},
  year={2023}
}
```

## 📧 Contact

For questions or issues, please contact:
- GitHub Issues: [repository URL]
- Email: [your email]

## 🙏 Acknowledgments

This dataset is based on the open-source COLD (Chinese Offensive Language Dataset). We thank the original authors for their contribution.

## 📄 License

This dataset is released under the MIT License.

---

**Dataset Version**: v1.0
**Release Date**: 2026-03-02

# Quantum GAN vs Classical GAN: A Comparative Study on MNIST

![Python](https://img.shields.io/badge/python-3.8+-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-1.9+-red.svg)
![PennyLane](https://img.shields.io/badge/PennyLane-0.28+-orange.svg)

**Exploring hybrid quantum-classical generative models and their training dynamics**

---

## 📌 Quick Links

- [📓 Classical GAN Notebook](notebooks/classical_gan.ipynb)
- [📓 QGAN (4-qubit) Notebook](notebooks/qgan_4qubit.ipynb)
- [📓 QGAN (8-qubit) Notebook](notebooks/qgan_8qubit.ipynb)
- [📄 Full Technical Report (21 pages)](report/QGAN_Technical_Report.pdf)

---

## Overview

This project implements and compares **Classical GANs** and **Quantum GANs (QGANs)** on MNIST, investigating how parameterized quantum circuits can be integrated into adversarial learning frameworks.

**Key Components:**
- Classical GAN baseline (PyTorch)
- Quantum GAN with 4-qubit generator (PennyLane + PyTorch)
- Quantum GAN with 8-qubit generator
- Comprehensive analysis of training dynamics and challenges

**Research Focus:**
- Barren plateau effects in quantum circuits
- Parameter-shift rule for gradient computation
- Quantum-classical hybrid optimization
- Comparison of convergence behavior and output quality

---

## Key Findings

### Generated Outputs

| Classical GAN (Epoch 22) | QGAN (4-qubit) | QGAN (8-qubit) |
|:------------------------:|:--------------:|:--------------:|
| Clear digit structure | Limited resolution | Improved patterns |
| 60,000 training images | 1,000 images | 1,000 images |
| ~12,000 iterations | Limited by circuit time | Slower but more expressive |

### Training Challenges Encountered

**Classical GAN:**
- Discriminator dominance → generator loss spikes
- Training instability
- Mode collapse tendencies

**Quantum GAN:**
- **Barren plateaus:** Gradients vanished with increased circuit depth
- **Synchronization issues:** Quantum circuit evaluation created asynchronous updates
- **Resource constraints:** Exponential scaling limited qubit count
- **Three iterations of debugging** (see loss curves in notebooks)

---

## Technical Details

### Architecture

**Quantum Generator (QGAN):**
```
Input: Random noise
↓
Parameterized Quantum Circuit (PQC)
  - 4 or 8 qubits
  - Rotation gates (RX, RY)
  - Entanglement (CNOT)
  - 2-8 layers
↓
Measurement → Classical post-processing
↓
28x28 generated image
```

**Gradient Computation:**
- Cannot use standard backpropagation on quantum circuits
- Used **parameter-shift rule**: ∂f(θ)/∂θ = [f(θ + π/2) - f(θ - π/2)] / 2
- Requires 2 circuit evaluations per parameter → significant computational overhead

**Classical Discriminator:**
- Fully connected neural network
- Binary classification (real vs fake)
- Shared between GAN and QGAN for fair comparison

---

## Experimental Process

The notebooks document three major experimental iterations:

1. **Initial QGAN (Plot 1 in report):** 
   - Generator collapsed (loss near 0)
   - Discriminator overpowered → all outputs classified as fake
   - **Diagnosis:** Vanishing gradients, improper gradient flow

2. **Over-corrected QGAN (Plot 2):**
   - Both losses too stable and flat
   - Neither network learning effectively
   - **Diagnosis:** Learning rate too low, poor optimization

3. **Final QGAN (Plot 3):**
   - Stable generator loss with slight improvement
   - Irregular discriminator updates (due to quantum circuit overhead)
   - Best achievable results under hardware constraints

---

## What I Learned

**Quantum Machine Learning:**
- Barren plateaus are a fundamental challenge, not a bug
- Shallow circuits limit expressivity; deep circuits cause gradient issues
- Quantum simulators are exponentially expensive (8 qubits = 256-dimensional state)
- Parameter-shift rule works but doubles computational cost

**Adversarial Training:**
- Generator-discriminator balance is extremely fragile
- Small hyperparameter changes cause dramatic behavioral shifts
- Visual quality doesn't always correlate with loss values

**Research Skills:**
- How to debug quantum-classical hybrid systems
- Importance of documenting failed experiments
- Iterative experimentation and hypothesis testing
- Technical writing and result visualization

---

## Requirements
```bash
pip install torch torchvision pennylane pennylane-qiskit matplotlib numpy
```

**Tested on:**
- Python 3.8+
- PyTorch 1.9+
- PennyLane 0.28+
- Google Colab (for GPU access)

---

## Usage

### Option 1: View on GitHub
All notebooks include saved outputs - you can view results without running code.

### Option 2: Run Locally
```bash
git clone https://github.com/YOUR_USERNAME/qgan-mnist-comparison.git
cd qgan-mnist-comparison
pip install -r requirements.txt
jupyter notebook notebooks/
```

### Option 3: Run on Google Colab
- Upload notebooks to Colab
- Enable GPU runtime
- Install dependencies in first cell

**Warning:** QGAN training is computationally intensive:
- 4-qubit: ~30-60 minutes on CPU
- 8-qubit: ~2-4 hours on CPU
- Consider reducing epochs for quick testing

---

## Repository Contents
```
qgan-mnist-comparison/
├── notebooks/
│   ├── classical_gan.ipynb          # Baseline GAN implementation
│   ├── qgan_4qubit.ipynb            # QGAN with 4-qubit generator
│   └── qgan_8qubit.ipynb            # QGAN with 8-qubit generator
├── report/
│   └── QGAN_Technical_Report.pdf    # Complete 21-page analysis
├── README.md
├── requirements.txt
└── LICENSE
```

---

## Limitations & Future Work

**Current Limitations:**
- Quantum simulator constraints (limited to 8 qubits)
- No access to real quantum hardware (NISQ devices)
- Small dataset for QGAN due to computational costs
- Low visual quality in generated outputs

**Future Directions:**
- Test on IBM Quantum or Google Cirq hardware
- Implement quantum discriminator (full QGAN)
- Explore alternative gradient estimation methods
- Apply to smaller, structured datasets (molecules, finance)
- Investigate potential quantum advantage in low-data regimes

---

## References

1. Goodfellow et al. (2014). [Generative Adversarial Nets](https://arxiv.org/abs/1406.2661)
2. Lloyd et al. (2018). [Quantum Generative Adversarial Networks](https://arxiv.org/abs/1804.09139)
3. Dallaire-Demers & Killoran (2018). [Quantum GANs](https://arxiv.org/abs/1804.08641)
4. [PennyLane Documentation](https://docs.pennylane.ai)
5. [Qiskit Textbook - Quantum Machine Learning](https://qiskit.org/textbook/ch-machine-learning/)

---

## Citation
```bibtex
@misc{bhuvanesh2024qgan,
  author = {Bhuvanesh O},
  title = {Quantum GAN vs Classical GAN: A Comparative Study on MNIST},
  year = {2024},
  institution = {IISER Bhopal},
  url = {https://github.com/YOUR_USERNAME/qgan-mnist-comparison}
}
```

---

## License

MIT License - See [LICENSE](LICENSE) for details.

## Author

**Bhuvanesh O**  
B.S. Engineering Sciences (Electrical Engineering & Computer Science)  
Indian Institute of Science Education and Research (IISER) Bhopal

📧 bhuvanesh23@iiserb.ac.in  
🔗 [GitHub](https://github.com/YOUR_USERNAME)

---

## Acknowledgments

- Google Colab for providing free GPU resources
- PennyLane team for quantum ML framework
- IISER Bhopal for computational support
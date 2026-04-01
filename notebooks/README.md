# Notebooks Guide

## Overview

This folder contains three Jupyter notebooks documenting the GAN vs QGAN experiments.

## Notebooks

### 1. `classical_gan.ipynb`
Classical GAN baseline implementation.

**Contents:**
- MNIST data loading and preprocessing
- Generator and discriminator architecture
- Training loop with BCE loss
- Loss visualization and generated samples
- Analysis of training dynamics

**Training:** ~25 epochs, full MNIST dataset (60,000 images)

---

### 2. `qgan_4qubit.ipynb`
Quantum GAN with 4-qubit generator.

**Contents:**
- Parameterized quantum circuit (PQC) design
- Hybrid quantum-classical architecture
- Parameter-shift rule implementation
- Multiple training attempts (showing debugging process)
- Analysis of barren plateau effects

**Training:** Limited to 1,000 images due to computational constraints

**Key Observations:**
- Initial run: Generator collapse
- Second run: Over-stabilized equilibrium
- Final run: Improved but still limited by qubit count

---

### 3. `qgan_8qubit.ipynb`
Quantum GAN with 8-qubit generator.

**Contents:**
- Extended quantum circuit with more qubits
- Increased circuit depth (8 layers)
- Comparison with 4-qubit version
- Analysis of expressivity vs gradient flow trade-off

**Training:** Significantly slower due to circuit complexity

**Key Observations:**
- Better pattern structure than 4-qubit
- Still suffers from gradient vanishing
- Demonstrates scalability challenges

---

## Running the Notebooks

### Local
```bash
jupyter notebook
```

### Google Colab
Upload the notebook and enable GPU runtime for faster training.

### Note on Outputs
All notebooks include saved outputs from original training runs. You can view results without re-running (which can take hours for QGAN).

---

## Debugging Journey

The notebooks intentionally preserve the experimental process:
- Failed runs are documented (not deleted)
- Multiple loss curve attempts are shown
- Comments explain what went wrong and why

This reflects real research: most experiments fail, and documenting failure is valuable.
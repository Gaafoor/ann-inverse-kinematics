# 🦾 ANN-Based Inverse Kinematics Solver (Two-Link Manipulator)

## 📌 Overview
This project implements an **Artificial Neural Network (ANN)** using TensorFlow/Keras to solve **inverse kinematics** for a planar two-link robotic manipulator (2-DOF arm).  
Given an end-effector position *(x, y)*, the network predicts the joint angles *(θ₁, θ₂)* required to reach that point.

The project includes:
- Training/testing dataset generation via **forward kinematics**
- ANN training & validation
- Performance evaluation
- Sample prediction visualization

---

## 🤖 Manipulator Model

- Link lengths: `a1 = 1`, `a2 = 1`
- Degrees of freedom: `2`
- Workspace is a circle (`radius = 2`)

Forward kinematics formulas:

```

x = a1*cos(θ1) + a2*cos(θ1+θ2)
y = a1*sin(θ1) + a2*sin(θ1+θ2)

```

---

## 🧠 ANN Architecture

| Layer | Units | Activation |
|-------|-------|------------|
| Input | 64 | ReLU |
| Hidden | 32 | ReLU |
| Output | 2 (θ₁, θ₂) | Linear |

- Loss function: **MSE**
- Optimizer: **Adam**
- Epochs: `50`
- Batch size: `32`

---

## 🗂️ Dataset Generation

Random joint angles are sampled:

- Training range: `[-π, π]`
- Testing range: `[0, 2π]`

Forward kinematics is applied to compute `(x, y)`.

Datasets are saved as:

```

training_data.csv
testing_dataset.csv

```

Columns include:

```

Theta1, Theta2, X, Y

```

✅ These `.csv` files are **generated automatically by the notebook**.

⚠️ **Important:**  
> Run **Section 1** of the notebook first to auto-generate the datasets.

---

## 🚀 Training

Training monitors:

- Training loss
- Validation loss

Both steadily decrease across epochs.

The trained model is saved as:

```

inverse_kinematics_model.h5

```

---

## 📊 Evaluation Metrics
After training, the model is tested on an unseen dataset:

- **Test Loss**
- **Mean Absolute Error (MAE)**

Sample predictions are visualized to compare:

- Ground truth arm configuration
- Predicted arm configuration

---

## 📉 Results Summary

✅ Model converged successfully  
✅ Predictions demonstrate reasonable accuracy  
✅ Loss curves indicate healthy learning behavior

Example MAE (may vary):

```

Mean Absolute Error ≈ 3.23

```

---

## ⚠️ Challenges & Notes

### ✅ Forward/Inverse Relationship
Ensuring correct forward kinematics equations was critical.  
Sanity-checks and visual plots were used to validate dataset correctness.

### 🔁 Many-to-One Mapping
Inverse kinematics is **not unique**.  
For certain (x, y), multiple θ₁/θ₂ combinations are valid.  
This contributes to prediction error.

### 📦 Dataset Distribution
Random sampling can cluster many samples near the boundaries.

---

## 🔧 Future Improvements

- Add more layers / different activation functions
- Normalize dataset
- Try cyclic angle loss (`sin/cos` encoding)
- Add workspace constraints
- Test deeper architectures (200-200-100-50)

---

## 🗃️ Repository Structure

```

├── 120200214.ipynb            # Main notebook
├── training_data.csv          # Auto-generated dataset
├── testing_data.csv        # Auto-generated dataset
├── inverse_kinematics_model.h5# Saved trained model
├── README.md                  # You are here :)
└── figures/                  

````

---

## ▶️ How to Run

Install dependencies:

```bash
pip install tensorflow pandas numpy matplotlib
````

Then open `120200214.ipynb` in:

* Google Colab ✅ recommended
* Jupyter Notebook

Run:

1. **Section 1** → generates datasets
2. **Training section** → trains model
3. **Evaluation section** → tests performance
4. **Visualization** → compares predicted vs. true arm

---

## 👤 Author

**Mostafa Ahmed**
Mechatronics & Robotics Engineering
Egypt-Japan University of Science & Technology (E-JUST)

---

```

---



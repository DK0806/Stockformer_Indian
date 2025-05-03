# Stockformer_Indian
```markdown
# Stockformer (Indian Stock Market Version)

This repository contains a modified version of Stockformer adapted for Indian stock market forecasting.  
It supports single-step prediction and includes an experimental branch for multi-step (ODE-based) forecasting.

This project was developed and maintained by **Dhruv**.

---

## 🚀 Main Features and Changes

- Adapted Stockformer for Indian stock market data.
- Built a custom **Ranger optimizer** to replace the deprecated one in the original repo.
- Indian stock data preparation uses **prepare_indian_data.ipynb** (not `data_prepare.ipynb` or `data_collect.ipynb` from the original repo).
- `.gitignore` updated to exclude large `.csv` and `.pt` files.

---

## 📥 Getting the Indian Dataset

1. Download the pre-cleaned Indian stock dataset:
```

\[Google Drive Link Here]

```

2. Place the downloaded file in the **root directory** as:
```

processed\_data\_filtered.csv

````

3. (Optional) Run additional preprocessing:
```bash
jupyter notebook prepare_indian_data.ipynb
````

---

## 💻 How to Set Up the Environment

1. **Clone the repository**

   ```bash
   git clone https://github.com/DK0806/Stockformer_Indian.git
   cd Stockformer_Indian
   ```

2. **Create and activate a virtual environment**

   ```bash
   python3 -m venv stockformer_env
   source stockformer_env/bin/activate
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

---

## ⚙️ Sample `config.yaml`

```yaml
model: stockformer
root_path: ./data/stock/
data_path: full_indian_1h.csv
freq: h

features: MS
target: 3MINDIA_logpctchange
cols:
  - ABBOTINDIA_logpctchange
  - ACC_logpctchange
  - ACE_logpctchange
  - ADANIENT_logpctchange
  - ADANIPORTS_logpctchange
  - 3MINDIA_logpctchange

seq_len: 32
label_len: 0
pred_len: 1

d_model: 512
n_heads: 8
enc_in: 6
e_layers: 4
d_ff: 4096
final_mode: mode3
c_out: 1
dropout: 0.2
dropout_emb: 0.0
t_embed: time2vec_app
emb_t2v_app_dim: 16
activation: gelu

attn: full
factor: 5
distil: false
output_attention: false
mix: false
ln_mode: post

batch_size: 128
learning_rate: 1e-5
loss: stock_tanhv1
lradj: null
max_epochs: 20
patience: 50

scale: true
no_scale_mean: true
inverse_output: false
inverse_pred: true
no_early_stop: false
dont_shuffle_train: true

date_start: '2015-01-09'
date_end: '2020-12-31'
date_test: '2020-01-01'
```

---

## 🔑 Explanation of Important Config Fields

* **data\_path** → Indian dataset filename.
* **target** → the stock you want to forecast.
* **cols** → input features including Granger-causal series.
* **seq\_len / pred\_len** → how many past steps to use and future steps to predict.
* **d\_model, n\_heads, e\_layers** → transformer architecture size.
* **batch\_size, learning\_rate** → training setup.

---

## 📊 How to Train the Model

1. **Run training**

   ```bash
   python main.py --config config.yaml
   ```

2. **For ODE / multi-step experiments**

   ```bash
   git checkout feature/ode-extension
   python main.py --config config.yaml
   ```

---

## 📁 Project Structure

```
Stockformer_Indian/
├── data/
├── checkpoints/
├── layers/
├── models/
├── main.py
├── prepare_indian_data.ipynb
├── config.yaml
├── requirements.txt
├── .gitignore
├── README.md
```

---

## 📂 Notes on Large Files

* `.csv` and `.pt` files are **ignored** from Git and need to be managed locally.
* Always place datasets like `processed_data_filtered.csv` in the project root.

---

## ⚡ Credits

* Original repo: [zacswolf/Stockformer2022](https://github.com/zacswolf/Stockformer2022)
* Indian dataset adaptation, modifications, and maintenance: **Dhruv**


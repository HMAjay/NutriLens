# NutriLens 🍽️

> Real-time food recognition and nutritional analysis powered by deep learning.

![Python](https://img.shields.io/badge/Python-3.11-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.13-orange)
![Flask](https://img.shields.io/badge/Flask-2.3-green)
![Docker](https://img.shields.io/badge/Docker-enabled-blue)

**Live Demo → [huggingface.co/spaces/Ashwamedha/nutrilens](https://huggingface.co/spaces/Ashwamedha/nutrilens)**

---

## What it does

Upload a photo of any food and NutriLens will:
- Identify the dish using a deep learning model (101 food categories)
- Return top 3 predictions with confidence scores
- Show a full nutritional breakdown — protein, fat, carbohydrates, calcium, vitamins
- Estimate calories per 100g
- Link to detailed nutrition info via Nutritionix

---

## Demo

| Upload | Results |
|---|---|
| Drop a food photo | Get instant nutrition report |

---

## Tech Stack

| Layer | Technology |
|---|---|
| ML Model | InceptionV3 (transfer learning, ImageNet weights) |
| Dataset | Food-101 (101,000 images, 101 classes) |
| Backend | Flask + Gunicorn |
| Nutrition Data | USDA FoodData Central API |
| AI Descriptions | Google Gemini Vision (optional) |
| Deployment | HuggingFace Spaces + Docker |
| Training | Google Colab T4 GPU |

---

## Model

- Architecture: InceptionV3 with custom classification head
- Training: 30 epochs, ~10-11 hrs on Google Colab T4 GPU
- Validation accuracy: ~77%
- Model weights hosted on: [HuggingFace Hub](https://huggingface.co/Ashwamedha/nutrilens-model)

---

## Project Structure
```
NutriLens/
├── app.py                        # Flask app
├── nutrition101.csv              # USDA nutrition data for 101 foods
├── requirements.txt
├── Dockerfile
├── NutriLens_Training.ipynb      # Google Colab training notebook
├── get_nutrition_data.py         # Script to regenerate nutrition CSV
├── static/
│   └── uploads/                  # Auto-created on first run
└── templates/
    ├── index.html                # Homepage with drag-and-drop upload
    ├── recognize.html            # Upload confirmation
    └── results.html              # Nutritional results report
```

---

## Run Locally

### 1. Clone the repo
```bash
git clone https://github.com/HMAjay/NutriLens.git
cd NutriLens
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

> On Apple Silicon (M1/M2), replace `tensorflow` with `tensorflow-macos tensorflow-metal`

### 3. Add the trained model
Train the model in Google Colab using `NutriLens_Training.ipynb`,
then place `model_trained_101class.hdf5` in the root folder.

Without it, the app runs in **demo mode** (random predictions).

### 4. (Optional) Set Gemini API key
```bash
export GOOGLE_API_KEY="your_key_here"
```

### 5. Run
```bash
python app.py
```
Open [http://127.0.0.1:7860](http://127.0.0.1:7860)

---

## Training Your Own Model

Open `NutriLens_Training.ipynb` in Google Colab:
1. Runtime → Change runtime type → **T4 GPU**
2. Run all cells
3. Model auto-saves to Google Drive
4. Download and place in project root

---

## Deployment

Hosted on **HuggingFace Spaces** using Docker.
Model weights stored separately on **HuggingFace Hub** and auto-downloaded on startup.

---

## License

MIT License — feel free to use and modify.

---

*Built with TensorFlow, Flask, and Food-101*
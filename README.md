# Movie Data Analysis

Predicts whether a movie will be profitable (revenue > budget) from its metadata, using [The Movies Dataset](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset) from Kaggle.

The project has two notebooks, meant to be run in order:

1. **[EDAandCleaning.ipynb](EDAandCleaning.ipynb)**: loads the raw data, cleans it, explores it, and builds the modelling features (budget, runtime, release year/month, franchise, English-language, major studio, genres). Writes `data/model_data.csv`.
2. **[machineLearningModel.ipynb](machineLearningModel.ipynb)**: reads `data/model_data.csv` and trains and compares classifiers (k-NN, decision tree, random forest, gradient boosting, neural network, logistic regression) using grid search, ROC AUC, and tuned decision thresholds.

## Setup

Requires Python 3.11 or newer (tested on 3.14).

```bash
git clone <this-repo-url>
cd movieDataAnalysisGraphite

python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Get the data

The `data/` folder isn't in the repo because the files are large, so you need to download them yourself.

1. Download the dataset from Kaggle: https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset (you need a free Kaggle account).
2. Unzip it into a `data/` folder in the project root.

The notebooks need these three files:

```
data/
├── movies_metadata.csv
├── keywords.csv
└── credits.csv
```

The other files in the download (`ratings.csv`, `links.csv`, etc.) aren't used and can be deleted to save space. `ratings.csv` alone is about 700 MB.

If you use the Kaggle CLI, you can download it like this instead:

```bash
kaggle datasets download -d rounakbanik/the-movies-dataset -p data --unzip
```

## Run

```bash
jupyter notebook
```

Then open and run all cells in each notebook, in this order:

1. `EDAandCleaning.ipynb`: creates `data/model_data.csv`
2. `machineLearningModel.ipynb`: needs `data/model_data.csv` from step 1

In VS Code, you can open the notebooks directly and select the `.venv` interpreter as the kernel.

Run the notebooks from the project root, because they use relative paths like `data/movies_metadata.csv`.

The model notebook runs several grid searches (including a neural network), so it can take a few minutes to finish.

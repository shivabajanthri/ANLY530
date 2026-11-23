# Flaky Test Prediction: A Machine Learning Study Using the FlakeFlagger Data

ANLY 530 conference-paper project. A flaky test passes and fails on the same code. This project asks whether simple machine learning models can rank tests by their risk of being flaky, so a team knows which tests to recheck first.

## Research questions

- **RQ1:** How well can a model predict flaky tests, within the dataset and on projects it has never seen?
- **RQ2:** Which test characteristics does the model rely on most?
- **RQ3:** How does the type of test information used affect flaky test prediction on new projects?

## Data

FlakeFlagger dataset (Alshammari et al., 2021): 22,236 test methods from 24 open-source Java projects, 811 of them flaky. It is public:
<https://github.com/AlshammariA/FlakeFlagger>

Two files are used, both read directly from the authors' repository:

- `processed_data.csv`: test features and the flaky label
- `processed_data_with_vocabulary_per_test.csv`: words in each test's source code

No data is stored in this repository.

## How to run

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```

Open the notebooks from the `notebooks/` folder and run all cells. Notebook 01 takes about a minute. Notebook 02 takes about 20 minutes on a laptop. All tables and charts appear in the notebook outputs.

## Repository layout

```
notebooks/01_exploration_and_feasibility.ipynb   data exploration, leakage checks, fold design, baseline checks
notebooks/02_models_and_evaluation.ipynb         RQ1 to RQ3, and a check on 25 project groupings
requirements.txt                                  Python packages
```

## Method in brief

- **Features:** 16 measurements (8 test-smell flags, test size, coverage, run time, code changes in the last 100 commits, third-party libraries), each measure's percentile within its own project, and the words in each test's code (TF-IDF).
- **Baselines:** random ranking, the rule "rerun the slowest tests first", and logistic regression.
- **Models:** logistic regression, a decision tree (depth 4), a random forest, and gradient boosting. Each tunes one regularization setting and class weights (on or off) on the training fold only.
- **Folds:** stratified grouped 5-fold cross-validation, seed 0. *Unseen projects* hold out whole projects; *seen projects* hold out whole test classes. The 25 repeated groupings use shuffled grouped folds with seeds 0 to 4.
- **Metrics:** PR-AUC on all held-out tests of a fold, and the share of flaky tests found when each project reruns its own riskiest 10% of tests.
- **Leakage controls:** filling, scaling, TF-IDF, and tuning are fitted inside pipelines on training folds only; percentile features use feature values, never labels; holding out whole projects keeps most near-copies of a test (655 of 687 groups) on one side of a split.
- **Projects with no flaky tests:** jimfs has none. It stays in training and testing. PR-AUC is computed per fold, so it stays defined; in the rerun budget the project still spends its 10% but adds no finds.

## Status

- Milestone 1: research protocol and exploration notebook
- Milestone 2: models, evaluation, and preliminary findings (notebook 02)
- Final: leave-one-project-out check, bootstrap interval, top code words, paper, and presentation

## Contribution statement

Individual study. I designed the study, prepared the data, wrote the code and notebooks, and wrote the reports.

## Data citation

Alshammari, A., Morris, C., Hilton, M., & Bell, J. (2021). FlakeFlagger: Predicting flakiness without rerunning tests. In *2021 IEEE/ACM 43rd International Conference on Software Engineering (ICSE)* (pp. 1572-1584). IEEE. https://doi.org/10.1109/ICSE43902.2021.00140

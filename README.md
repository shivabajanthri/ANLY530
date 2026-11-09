# Flaky Test Prediction: A Machine Learning Study Using the FlakeFlagger Data

ANLY 530 conference-paper project. A flaky test passes and fails on the same code. This project asks whether simple machine learning models can rank tests by their risk of being flaky, so a team knows which tests to recheck first.

## Research questions

- **RQ1:** How well can a model predict flaky tests, within the dataset and on projects it has never seen?
- **RQ2:** Which test characteristics does the model rely on most?
- **RQ3:** How does the type of test information used affect flaky test prediction on new projects?

## Data

FlakeFlagger dataset (Alshammari et al., 2021): 22,236 test methods from 24 open-source Java projects, 811 of them flaky. It is public:
<https://github.com/AlshammariA/FlakeFlagger>

Two files are used, both from the authors' repository:

- `processed_data.csv`: test features and the flaky label
- `processed_data_with_vocabulary_per_test.csv`: words in each test's source code

No data is stored in this repository.

## How to run

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/01_exploration_and_feasibility.ipynb
```

## Repository layout

```
notebooks/01_exploration_and_feasibility.ipynb   data exploration, leakage checks, fold design, baseline checks
requirements.txt                                  Python packages
```

## Status

- Milestone 1 (Week 10): research protocol and exploration notebook
- Milestone 2 (Week 12): model results
- Final (Week 13): paper and 5-minute talk

## Contribution statement

Individual study. I designed the study, prepared the data, wrote the code and notebook, and wrote the protocol.

## Data citation

Alshammari, A., Morris, C., Hilton, M., & Bell, J. (2021). FlakeFlagger: Predicting flakiness without rerunning tests. In *2021 IEEE/ACM 43rd International Conference on Software Engineering (ICSE)* (pp. 1572-1584). IEEE. https://doi.org/10.1109/ICSE43902.2021.00140

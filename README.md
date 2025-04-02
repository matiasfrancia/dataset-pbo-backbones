# Backbone Extraction Dataset (SAT 2025)

This repository contains the dataset `complete_backbones.tar.gz`, which includes backbone extraction results from three extractors on 8,351 Pseudo-Boolean Optimization (PBO) instances. The data was produced as part of the experiments described in our submission to the SAT 2025 Conference.

The instances used in this dataset are taken from the **OPT-LIN track** of the benchmark proposed for the **Pseudo-Boolean Competition 2024**.

---

## File Contents

- **`complete_backbones.csv`**: A CSV file with one row per backbone extraction attempt, including both metadata and backbone information for each instance.

---

## File Format and Structure

Each row corresponds to a single instance, and includes the following fields:

| Column Name                  | Description                                                                |
|-----------------------------|----------------------------------------------------------------------------|
| `Instance`                  | Path or identifier of the PBO instance                                     |
| `Extractor`                 | The backbone extractor used (`GuroBack`, `NapBack`, or `RoundingBack`)     |
| `Extraction Time`           | Time in seconds required to extract the backbone                           |
| `Number of Variables`       | Number of variables in the instance                                        |
| `Objective`                 | Objective value (for optimization problems)                                |
| `Optimization Solving Time` | Time in seconds used to find the optimum (if applicable)                   |
| `Backbone Size`             | Number of literals in the backbone                                         |
| `x_1`, ..., `x_k`           | Backbone status for each variable (see below)                              |

### Backbone Variables (`x_i`)

For each instance, the backbone columns follow the format `x_1`, `x_2`, ..., up to `x_n`, where `n` is the number of variables **in that instance only**.

- `'1'`: Variable is in the backbone with **positive polarity**
- `'0'`: Variable is in the backbone with **negative polarity**
- `'2'`: Variable is **not** in the backbone

🔹 **Important**: The CSV includes headers up to `x_1281998`, corresponding to the maximum number of variables observed across all instances. However, each row contains values **only up to the number of variables in the respective instance**. Thus, rows are effectively "ragged" in length. The header line is provided for reference.

---

## ⚠️ Notes on Usage

Due to the varying number of variable columns per row, standard tools like `pandas.read_csv()` may not work out-of-the-box, as it assumes uniform row lengths. We recommend using custom parsing scripts or tools that can handle variable-length rows.

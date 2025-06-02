# Dataset Deduplication and Analysis with Rensa MinHash

This repository contains a Google Colab notebook designed for efficient dataset deduplication and similarity analysis using various MinHash implementations from the high-performance `Rensa` library. It's particularly well-suited for identifying near-duplicate text entries within large datasets and offers options for detailed analysis and uploading results to the Hugging Face Hub.

## ✨ Features

* **Flexible Dataset Loading:** Load datasets from Hugging Face Hub with options for specific splits and sample sizes.
* **Multiple MinHash Algorithms:** Utilize different MinHash variants from Rensa for similarity estimation:
    * `RMinHash`
    * `CMinHash`
    * `OptDensMinHash`
    * `RMinHashLSH` (includes Locality Sensitive Hashing)
* **Configurable Parameters:** Adjust key parameters like the number of permutations, similarity thresholds, and LSH settings.
* **Comprehensive Analysis:** Generate detailed statistics, visualize similarity distributions, and optionally export removed samples.
* **Hugging Face Hub Integration:** Seamlessly upload processed datasets (deduplicated results or removed samples) to your Hugging Face profile.

## 🚀 Getting Started

To run this notebook, open it in Google Colab (or a Jupyter environment). The key configurations are exposed as form fields at the top of the notebook, allowing you to easily customize its behavior without editing the code directly.

### Prerequisites

Ensure you have the necessary Python libraries installed. A `pip install` command to get the primary dependencies might look like this (you might need to adjust versions based on your environment):

```bash
# Example dependencies based on your configuration parameters and typical usage
!pip install datasets pandas numpy scipy fsspec huggingface-hub tqdm packaging pyarrow rensa datasketch
```

### Configuration

You can customize the notebook's behavior using the parameters defined in the "Configuration Parameters" section:

#### 🎯 Dataset Configuration

| Parameter       | Description                                                                                             | Example Value                  |
| :-------------- | :------------------------------------------------------------------------------------------------------ | :----------------------------- |
| `dataset_name`  | The name of the dataset to load from Hugging Face Hub (e.g., `gretelai/synthetic_text_to_sql`).         | `"gretelai/synthetic_text_to_sql"` |
| `dataset_split` | The specific split of the dataset to use (e.g., `train`, `test`, `validation`, `all`).                | `"train"`                      |
| `text_column`   | The name of the column in the dataset that contains the text data for similarity analysis.             | `"sql"`                        |
| `sample_size`   | Number of samples to use. Set to `0` to process the entire dataset.                                     | `0`                            |

#### 🔧 Algorithm Configuration

| Parameter            | Description                                                                     | Example Value  |
| :------------------- | :------------------------------------------------------------------------------ | :------------- |
| `algorithm`          | The MinHash algorithm to use (`RMinHash`, `CMinHash`, `OptDensMinHash`, `RMinHashLSH`). | `"RMinHashLSH"` |
| `num_permutations`   | The number of permutations for the MinHash algorithm (influences accuracy).    | `128`          |
| `similarity_threshold` | The Jaccard similarity threshold above which samples are considered duplicates. | `0.85`         |
| `random_seed`        | Seed for reproducibility of random operations.                                  | `42`           |

#### 🚀 LSH Configuration (Only for `RMinHashLSH`)

| Parameter       | Description                                                               | Example Value |
| :-------------- | :------------------------------------------------------------------------ | :------------ |
| `lsh_num_bands` | Number of bands for Locality Sensitive Hashing.                           | `16`          |
| `lsh_threshold` | Similarity threshold used by LSH for candidate pair generation.           | `0.8`         |

#### 📤 Upload Configuration

| Parameter        | Description                                                                         | Example Value                    |
| :--------------- | :---------------------------------------------------------------------------------- | :------------------------------- |
| `upload_to_hf`   | Boolean flag to enable uploading results to Hugging Face Hub.                       | `True`                           |
| `target_repo`    | The name of the Hugging Face repository to upload to. Leave empty for auto-generation. | `"Syed-Hasan-8503/Test-dataset"` |
| `hf_token`       | Your Hugging Face API token with write access (get it from `huggingface.co/settings/tokens`). | `hf_...`                         |
| `private_repo`   | Boolean flag to make the target Hugging Face repository private.                    | `False`                          |

#### 📊 Analysis Options

| Parameter                | Description                                                          | Example Value |
| :----------------------- | :------------------------------------------------------------------- | :------------ |
| `show_detailed_stats`    | Display detailed statistics about the deduplication process.         | `True`        |
| `show_similarity_distribution` | Plot the distribution of computed similarities.                  | `True`        |
| `export_removed_samples` | Save the samples identified as duplicates to a separate dataset.     | `False`       |

## 🤝 Contributing

Contributions to this project are welcome! If you find issues or have suggestions for improvements, please feel free to open an issue or submit a pull request.

## 📄 License

This project is open-sourced under the MIT License, consistent with the `Rensa` library it utilizes. See the `LICENSE` file for more details.

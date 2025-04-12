# AI Progress Data Collection Tool

This repository contains a Python script that collects benchmark data from Papers With Code for tracking progress in AI research across various domains.

## Overview

The script scrapes data from Papers With Code benchmark pages to extract:
- Benchmarks with at least 20 datapoints
- Model performance results over time
- Paper information (title, URL)
- Code repository links
- Model descriptions and parameter counts
- Performance metrics

The data is saved in a structured CSV format for further analysis.

## Requirements

- Python 3.6+
- Required Python packages:
  - pandas
  - selenium
  - webdriver_manager
  - python-dateutil
  - requests
  - beautifulsoup4

You can install all required packages with:

```bash
pip install pandas selenium webdriver_manager python-dateutil requests beautifulsoup4
```

Additionally, this script uses Chrome WebDriver, which will be automatically installed by the webdriver_manager package.

## Usage

### Basic Usage

1. Clone this repository:
```bash
git clone https://github.com/yourusername/ai-progress-data.git
cd ai-progress-data
```

2. Run the script for a specific AI task:
```bash
python collect_data.py --task "medical-image-segmentation"
```

### Advanced Usage

To collect data for multiple AI tasks:

```bash
python collect_data.py --tasks "speech-recognition,anomaly-detection,denoising"
```

Or use the batch collection mode:

```bash
python collect_data.py --batch-file tasks.txt
```

Where `tasks.txt` contains one task URL per line:
```
https://paperswithcode.com/task/medical-image-segmentation
https://paperswithcode.com/task/speech-recognition
https://paperswithcode.com/task/denoising
```

### Command-line Arguments

- `--task` or `-t`: Single task to scrape (e.g., "medical-image-segmentation")
- `--tasks`: Comma-separated list of tasks to scrape
- `--batch-file` or `-b`: Path to a text file with one task URL per line
- `--output-dir` or `-o`: Custom output directory path (default: ~/Documents/Jupyter Notebooks/RA Task/tech_progress_data)
- `--headless`: Run Chrome in headless mode (default: True)
- `--timeout`: Set page load timeout in seconds (default: 30)
- `--sleep` or `-s`: Time to sleep between benchmark page requests (default: 5)
- `--min-datapoints` or `-m`: Minimum number of datapoints required for a benchmark (default: 20)

## Data Structure

The script creates the following directory structure:

```
tech_progress_data/
├── task_name/
│   ├── task_name_benchmarks_20plus.csv
│   ├── all_task_name_models.csv
│   ├── yearly_model_count.csv
│   └── benchmark_name/
│       ├── raw_data.json
│       └── models.csv
```

### Output Files

- `task_name_benchmarks_20plus.csv`: List of benchmarks with 20+ datapoints
- `all_task_name_models.csv`: Combined data from all benchmarks for the task
- `yearly_model_count.csv`: Number of models published per year for each dataset
- `raw_data.json`: Raw JSON data from the benchmark page (if available)
- `models.csv`: Model data for each specific benchmark

## Customization

You can modify the script to:

1. Change the minimum datapoint threshold:
```python
MIN_DATAPOINTS = 20  # Change to your preferred value
```

2. Add additional parameter extraction patterns:
```python
patterns = [
    r'(\d+\.?\d*)\s*[Mm]illion\s*parameters',
    # Add your custom patterns here
]
```

3. Customize the data directory structure:
```python
data_dir = os.path.join(home_dir, "your", "custom", "path")
```

## Troubleshooting

- **Selenium errors**: Make sure you have Chrome installed and that the webdriver_manager package can access it.
- **JSON parsing errors**: The script attempts to extract data from both JSON and HTML tables. If one method fails, it will try the other.
- **Timeout errors**: Try increasing the timeout value using the `--timeout` argument.
- **Rate limiting**: The script includes a 5-second delay between requests to be gentle to the server. You can increase this with the `--sleep` argument.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

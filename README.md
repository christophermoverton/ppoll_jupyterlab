
# Presidential Polling Analysis

This Jupyter Notebook provides an in-depth analysis of presidential polling data, utilizing various data manipulation techniques, visualizations, and statistical adjustments. The analysis includes weighting methodologies, outlier adjustments, house effect bias adjustments, and specific breakdowns of polling data for different candidates in key battleground states.

The data used in this notebook is sourced from **FiveThirtyEight's Presidential General Election Polls (current cycle)**, which is publicly available on the [FiveThirtyEight website](https://projects.fivethirtyeight.com/polls/president-general/). This dataset includes national and state-level polling data for the current U.S. presidential election cycle, and this analysis uses the CSV format provided by FiveThirtyEight.

## Data Source

The primary data source is a CSV file (`president_polls.csv`) derived from FiveThirtyEight's publicly available polling data, which includes national and state-level information related to U.S. presidential elections. The file contains details such as:
   - Pollster name
   - Candidate names
   - Polling methodology
   - Pollster grades
   - Sample sizes
   - Poll results (e.g., support for each candidate)

## Structure

### 1. **Initial Setup**
   - **Libraries Used**: 
     - `pandas` for data manipulation.
     - `altair` for data visualization.
     - `statsmodels` for smoothing functions.
     - `numpy` for numerical computations.
   - The notebook begins by loading the dataset and conducting preliminary inspections of the data.

### 2. **Data Cleaning and Preprocessing**
   - The dataset is split into two groups: polls with missing state information (`df_state_na`) and polls with state-level data (`df_state_not_na`).
   - Only polls with non-null numerical grades (grading pollster reliability) are used for further analysis.

### 3. **Weight Calculation**
   - A custom weighting system is implemented based on:
     - **Pollster Grades**: Higher graded pollsters are given more weight.
     - **Polling Methodology**: Different methodologies (e.g., live phone, online, etc.) are assigned different weights based on their reliability.
     - **Outlier Weighting**: Polls that fall outside the typical distribution are down-weighted to mitigate their impact. This is done by identifying and assigning lower weights to outlier polls, ensuring they don't disproportionately influence the results.
   - A new column `weight_score` is added to the dataset to reflect these weights, which combines the grades, methodologies, and outlier adjustments.

### 4. **House Effect Bias Adjustment**
   - **House Effects**: This refers to the consistent bias or tendency of certain pollsters to lean towards one candidate or another. The analysis incorporates a bias adjustment to account for this, making the polling data more comparable across different pollsters.
   - A bias factor is calculated and applied to correct the house effects, ensuring that polls from consistently biased pollsters do not skew the overall results.
   - This adjustment is incorporated before generating the final weighted averages, contributing to more accurate tracking of candidate support over time.

### 5. **Sample Size Adjustment**
   - Polls with missing sample sizes are handled by calculating the mean sample size and imputing missing values accordingly.
   - Weighted averages are calculated for each candidate based on these sample sizes and pollster grades. Larger sample sizes are given more weight, as they are generally considered more reliable.

### 6. **Candidate Analysis**
   - The notebook focuses on key candidates such as Donald Trump and Kamala Harris. Specific sections explore the polling data related to these candidates in critical battleground states like:
     - **Arizona**
     - **Nevada**
   - For each state, weighted averages of polling data are computed over time to track changes in candidate support.

### 7. **Visualization**
   - Several visualizations are created to present the polling data, including:
     - **Boxplots**: Displaying distributions of polling "house effects" by pollster and candidate, adjusted for bias.
     - **Time Series Graphs**: Weighted average support for each candidate over time.
     - The visualizations use `altair`, with custom color scales to distinguish between candidates (e.g., red for Donald Trump, blue for Kamala Harris).

### 8. **Smoothing Functions**
   - The notebook applies non-parametric LOESS smoothing using `statsmodels` to visualize trends in the polling data over time. This helps in reducing noise from short-term fluctuations and better understanding long-term trends.

## Setup Instructions

### 1. **Python Virtual Environment Setup**

To run this notebook in an isolated Python environment, it is recommended to use a virtual environment. Follow the steps below to set up a virtual environment and install all dependencies:

1. **Create and Activate a Virtual Environment**:
   - Open a terminal or command prompt and navigate to the project directory.
   - Create a new virtual environment using the following command:
     ```bash
     python -m venv env
     ```
   - Activate the virtual environment:
     - On **Windows**:
       ```bash
       .\env\Scripts\activate
       ```
     - On **macOS/Linux**:
       ```bash
       source env/bin/activate
       ```

2. **Install Dependencies**:
   - Once the virtual environment is activated, install the required dependencies using the `requirements.txt` file provided in the project:
     ```bash
     pip install -r requirements.txt
     ```
   This will install all the necessary Python libraries for running the notebook, including `pandas`, `altair`, `statsmodels`, and `numpy`.

### 2. **Launching Jupyter Lab**

After setting up the virtual environment and installing the required dependencies, you can launch Jupyter Lab to run the notebook:

1. **Install Jupyter Lab** (if not already installed):
   ```bash
   pip install jupyterlab
   ```

2. **Launch Jupyter Lab**:
   - From the terminal or command prompt, use the following command to start Jupyter Lab:
     ```bash
     jupyter lab
     ```
   - This will open the Jupyter Lab interface in your web browser. From there, navigate to the notebook file (`538pollingdata.ipynb`) to begin the analysis.

3. **Running the Notebook**:
   - Execute the notebook cell by cell to perform the analysis, explore the weighted polling data, and generate visualizations.

### 3. **Deactivating the Virtual Environment**
   - Once you are done, you can deactivate the virtual environment by running:
     ```bash
     deactivate
     ```

## Key Insights

- **House Effect Bias Adjustment** ensures that polls from consistently biased pollsters are corrected, making the comparison across different pollsters more reliable.
- **Outlier Weighting** helps mitigate the effect of extreme polling results that could skew the overall analysis. By down-weighting outliers, the analysis provides a more stable picture of candidate support.
- The analysis highlights how different polling methodologies, sample sizes, and pollster reliability affect the overall perception of candidate support.
- By focusing on key battleground states, the analysis offers a granular look at the dynamics of the 2020 U.S. presidential election.

## License

This project is licensed under the MIT License.


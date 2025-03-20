# 1. Getting Started

# Anaconda

- Anaconda is a distribution of Python that comes with:
    - Python itself
    - Conda (a package and environment manager)
    - Pre-installed data science libraries (NumPy, Pandas, Matplotlib, etc.)
    - Jupyter Notebook & JupyterLab (interactive coding environments)
- Why use Anaconda?
    - It simplifies package management.
    - It allows you to create isolated environments for different projects.
    - It includes Jupyter Notebook, which is commonly used in data analysis.

## Install Anaconda

- **Download Anaconda** from https://www.anaconda.com/download
- **Install** it by following the instructions for your OS (Windows, macOS, or Linux).
- **Verify the installation** by opening a terminal (Command Prompt on Windows or Terminal on macOS/Linux) and typing:
    
    ```
    conda --version
    ```
    
    If installed correctly, it will show the version of Conda.
    

## Virtual Environments in Anaconda

- A **virtual environment** helps you manage dependencies separately for different projects.

### Create a New Environment

1. Open **Anaconda Prompt** or your system terminal.
2. Run the following command to create an environment named `data_analytics_env` with Python 3.10:
    
    ```
    conda create --name data_analytics_env python=3.10
    ```
    
3. **Activate the environment:**
    1. On Windows:
        
        ```
        conda activate data_analytics_env
        ```
        
    2. On macOS/Linux:
        
        ```
        source activate data_analytics_env
        ```
        
4. **Verify the environment is active:**
    
    ```
    python --version
    ```
    
    It should display Python 3.10.
    
5. **Install essential packages** (NumPy, Pandas, Matplotlib, Seaborn, etc.):
    
    ```
    conda install numpy pandas matplotlib seaborn jupyter
    ```
    
6. **Deactivate the environment when done:**
    
    ```
    conda deactivate
    ```
    

# Setting Up VSCode for Data Analytics

## Why use VSCode?

- Lightweight but powerful.
- Excellent support for Python, Jupyter Notebooks, and extensions.
- Integrates well with virtual environments.

## Install VSCode

1. Download it from https://code.visualstudio.com/
2. Install the **Python Extension**:
    1. Open VSCode → Go to **Extensions** (Ctrl+Shift+X) → Search **Python** → Install.

## Configure VSCode to Use Your Conda Environment

1. **Open VSCode.**
2. **Open a new project folder:**
    1. Click **File** → **Open Folder** → Select a directory for your project.
3. **Open the Command Palette** (Ctrl+Shift+P) and type:
    
    ```
    Python: Select Interpreter
    ```
    
4. **Choose the interpreter** that belongs to your Conda environment:
    
    ```
    ~/anaconda3/envs/data_analytics_env/bin/python (Mac/Linux)
    C:\Users\YourUser\anaconda3\envs\data_analytics_env\python.exe (Windows)
    ```
    
5. **Verify by opening a terminal inside VSCode** (Ctrl+`) and typing:
    
    ```
    python --version
    ```
    

# Practice Task

1. Install **Anaconda** and verify it using `conda --version`.
2. Create a Conda environment named `my_data_env` with Python 3.10.
3. Activate the environment and install the following packages:
    
    ```
    conda install numpy pandas matplotlib seaborn
    ```
    
4. Open VSCode, create a Python script (`test.py`), and print:
    
    ```python
    import sys
    print(f"Python Interpreter: {sys.executable}")
    ```
    
5. Run the script in VSCode’s integrated terminal to confirm it’s using the correct environment.
6. Expected Output:
    
    ```
    Python Interpreter: /Users/yourname/anaconda3/envs/my_data_env/bin/python
    ```
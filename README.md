# 🥞 FSDL Text Recognizer 2022

Implements a text recognizer using a hypermodern 2022 DL stack:

- Code quality assurance with pre-commit hooks, GitHub Actions, and pytest
- Real data augmented with data synthesis
- Image encoding via a CNN architecture
- Decoding to text via a Transformer architecture
- Model implementation in PyTorch
- Model training and basic tracking and metrics via PyTorch Lightning and torchmetrics
- Experiment tracking, hyperparameter tuning, and model versioning with W&B
- Model packaging in TorchScript
- Predictor backend containerization via Docker and deployment as a microservice on AWS Lambda
- Basic load testing with Locust
- Pure Python frontend web application in Gradio
- Model monitoring with Gantry

## Setup local environment

Setting up a machine that you can sit in front of or SSH into is easy.

### Watch a walkthrough video [here](https://fsdl.me/2022-local-setup-video).

If you get stuck, it's better to at least [get started with the labs on Colab](https://fsdl.me/lab00-colab), where setup is just a single click, rather than getting frustrated and burning out on annoying environment management, networking, and systems administration issues that aren't as relevant to making ML-powered products.

### Summary

- `environment.yml` specifies Python and optionally CUDA/CUDNN
- `make conda-update` creates/updates a virtual environment
- `conda activate fsdl-text-recognizer-2022` activates the virtual environment
- `requirements/prod.in` and `requirements/dev.in` specify core Python packages in that environment
- `make pip-tools` resolves all other Python dependencies and installs them
- `export PYTHONPATH=.:$PYTHONPATH` makes the current directory visible on your Python path -- add it to your `~/.bashrc` and `source ~/.bashrc`

### 1. Check out the repo

```
git clone https://github.com/full-stack-deep-learning/fsdl-text-recognizer-2022-labs.git
cd fsdl-text-recognizer-2022-labs
```

### 2. Set up the Python environment

We use
[`conda`](https://docs.conda.io/en/latest/miniconda.html)
for managing Python and CUDA versions, and
[`pip-tools`](https://github.com/jazzband/pip-tools)
for managing Python package dependencies.

We add a `Makefile` for making setup dead-simple.

#### First: Install the Python + CUDA environment using Anaconda

Conda is an open-source package management system and environment management system that runs on Windows, macOS, and Linux.

It is most closely associated with Python, but
[in fact it can manage more than just Python environments](https://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/).

To install `conda`, follow instructions at https://conda.io/projects/conda/en/latest/user-guide/install/linux.html. We use Python 3.8.

Note that you will likely need to close and re-open your terminal.
Afterwards, you should have ability to run the `conda` command in your terminal.

Run `make conda-update` to create an environment called `fsdl-text-recognizer-2022`, as defined in `environment.yml`.
This environment will provide us with the right Python version as well as the CUDA and CUDNN libraries.

If you edit `environment.yml`, just run `make conda-update` again to get the latest changes.

Next, activate the conda environment.

```sh
conda activate fsdl-text-recognizer-2022
```

**IMPORTANT**: every time you work in this directory, make sure to start your session with `conda activate fsdl-text-recognizer-2022`.

#### Next: install Python packages

Next, install all necessary Python packages by running `make pip-tools`

Using `pip-tools` lets us do three nice things:

1. Separate out dev from production dependencies (`dev.in` vs `prod.in`).
2. Have a lockfile of exact versions for all dependencies (the auto-generated `dev.txt` and `prod.txt`).
3. Allow us to easily deploy to targets that don't support the `conda` environment, like Colab.

#### Set PYTHONPATH

Last, run `export PYTHONPATH=.` before executing any commands later on, or you will get errors like this:
```python
ModuleNotFoundError: No module named 'text_recognizer'
```

In order to not have to set `PYTHONPATH` in every terminal you open, just add that line as the last line of the `~/.bashrc` file using a text editor of your choice (e.g. `nano ~/.bashrc`) or by concatenating with `>>`
```bash
echo "export PYTHONPATH=.:$PYTHONPATH" >> ~/.bashrc
```

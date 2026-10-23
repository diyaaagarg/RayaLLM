# LLM from scratch — VS Code

Open this entire folder in VS Code. Keep `gpt_download.py` beside the notebook.
Install the Microsoft Python and Jupyter extensions when prompted.

## Set up Python

Use Python 3.11 or 3.12. On macOS/Linux, run in the VS Code terminal:

```sh
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

On Windows PowerShell, create the environment with `py -3.12 -m venv .venv`
and activate it with `.venv\Scripts\Activate.ps1`, then run the two pip commands.

Open `llm_from_scratch.ipynb`, click **Select Kernel**, and choose `.venv`.
Run cells from top to bottom. Skip the `%pip` cell if requirements are already installed.
Restart the kernel if you install or upgrade packages after importing them.

## Files and hardware

The notebook downloads `the-verdict.txt` and GPT-2 weights when needed; first-time
execution requires internet access. GPT-2 weights are cached under `gpt2/`.
TensorFlow is used to read the original pretrained GPT-2 checkpoint files.
Training uses CUDA when available, otherwise Apple MPS with PyTorch 2.9+, otherwise CPU.
The original 124M model and ten training epochs are retained and can be slow or
memory intensive locally; you can lower `num_epochs` for a shorter experiment.

Checkpoints (`model.pth`, `model_and_optimizer.pth`) and plot PDFs are saved in
this project folder. Copy existing checkpoint files from Colab/Google Drive here
before running load cells. A notebook's saved outputs do not contain trained weights.
The setup cell supports `LLM_PROJECT_DIR` for kernels started elsewhere.

Your existing learning examples and outputs are retained; outputs in changed cells
were cleared so they do not show obsolete Colab results.

## NumPy / h5py binary incompatibility

If TensorFlow reports `numpy.dtype size changed`, select this project's `.venv`
kernel instead of the Anaconda base environment. The requirements keep NumPy at
1.26.4 with a compatible h5py range. Use Python 3.11 or 3.12 for this environment.
After installing requirements, restart the notebook kernel before importing packages.

Verify the selected environment in a notebook cell:

```python
import sys
import numpy, h5py, tensorflow
print(sys.executable)
print(numpy.__version__, h5py.__version__, tensorflow.__version__)
from gpt_download import download_and_load_gpt2
```

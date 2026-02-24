{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<div style=\"text-align: center;\">\n",
    "  <a href=\"https://cognitiveclass.ai/?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkDL0321ENSkillsNetwork951-2022-01-01\">\n",
    "    <img src=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-DL0321EN-SkillsNetwork/image/IDSN-logo.png\" width=\"400\">\n",
    "  </a>\n",
    "</div>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h1 align=left><font size = 6>Lab: Land Classification: CNN-Transformer Integration evaluation </font></h1>\n",
    "    \n",
    "<h2 align=left><font size = 5>Vision Transformer (ViT) Model Evaluation </font></h2>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Estimated time: 90 minutes\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "# Introdution\n",
    "\n",
    "This notebook presents an end-to-end workflow for importing, testing, and evaluating two Vision Transformer (ViT) models developed in Keras and PyTorch, respectively. \n",
    "The self-attention mechanism in the ViTs allows these models to learn complex and broad spatial dependencies, providing improved performance on a variety of vision tasks compared to traditional convolutional neural networks. However, the CNNs are adept in learning the local features very well and can be trained using relatively smaller datasets and is generally much more efficient in utilizing the computational resources, as compared to ViTs. A CNN-ViT hybrid architecture gains from both CNN and ViT model strengths, by getting local features extracted using CNNs, while the transformer part of the hybrid architecture can determine the global dependencies.\n",
    "\n",
    "This lab focuses on model loading, prediction on sample data, and quantitative evaluation of the ViT models created using KEras and PyTorch. You'll explore the details of the framework-specific implementations, test the consistency of results, and gain practical experience comparing deep learning models across different Python ecosystems. \n",
    "\n",
    "Upon completion, you will have a thorough understanding of loading the CNN-ViT hybrid models testing workflow, key evaluation metrics, and how high-level architectural concepts translate into practical model evaluation using both Keras and PyTorch.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Objectives\n",
    "\n",
    "- Import and initialize pre-trained CNN - Vision Transformer hybrid models from two deep learning frameworks (Keras/TensorFlow and PyTorch).\n",
    "- Prepare and preprocess sample image data for inference.\n",
    "- Perform model inference and obtain prediction results from both models.\n",
    "- Compute and compare core evaluation metrics.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Table of Contents\n",
    "1. [Dataset download, extraction and paths](#Dataset-download,-extraction-and-paths)\n",
    "2. [Pre-trained model download](#Pre-trained-model-download)\n",
    "3. [Package installation](#Package-installation)\n",
    "4. [Library imports and setup](#Library-imports-and-setup)\n",
    "5. [Fix random seed for reproducibility](#Fix-random-seed-for-reproducibility)\n",
    "6. [Defining PyTorch model architecture](#Defining-PyTorch-model-architecture)\n",
    "7. [Dataset path and hyperparameters](#Dataset-path-and-hyperparameters)\n",
    "8. [PyTorch Dataloader](#PyTorch-Dataloader)\n",
    "9. [--- PyTorch pre-trained ViT model loading ---](#----PyTorch-pre-trained-ViT-model-loading----)\n",
    "10. [PyTorch model inference metrics](#PyTorch-model-inference-metrics)\n",
    "11. [Keras model loading](#Keras-model-loading)\n",
    "12. [Keras pre-trained ViT model loading](#----Keras-pre-trained-ViT-model-loading----)\n",
    "13. [Define dataloader](#Define-dataloader)\n",
    "14. [Collecting metrics for Keras-based CNN-ViT hybrid model](#Collecting-metrics-for-Keras-based-CNN-ViT-hybrid-model)\n",
    "15. [Import the evaluation metrics](#Import-the-evaluation-metrics)\n",
    "16. [Keras metrics reporting](#Keras-metrics-reporting)\n",
    "17. [PyTorch metrics reporting](#PyTorch-metrics-reporting)\n",
    "18. [ROC curve plotting](#ROC-curve-plotting)\n",
    "19. [Comparing model performance](#Comparing-model-performance)\n",
    "20. [Summary and discussion](#Summary-and-discussion)\n",
    "21. [Conclusion](#Conclusion)\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Dataset download, extraction and paths\n",
    "We begin by downloading the dataset for evaluation of the models.\n",
    "Here, you declare:\n",
    "1. The dataset URL from where the dataset would be downloaded.\n",
    "2. The dataset downloading primary function, based on `skillsnetwork` library.\n",
    "3. The dataset fallback downloading function, based on regular `http` downloading functions.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Define root directory and download `url`\n",
    "\n",
    "First, you define the root directory where all the data would be downloaded and extracted.\n",
    "Here, the `dataset_url` is assigned a direct link to a tar archive hosted on IBM's cloud storage. This URL points to the satellite image dataset used for land classification tasks. Using a cloud-based URL ensures accessibility without local storage dependencies. This setup facilitates automated downloads later in the notebook. \n",
    "\n",
    "If dealing with large datasets, monitor download times and implement retry mechanisms for robustness. This variable is key for the subsequent download functions, linking external data to the local workflow.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [],
   "source": [
    "data_dir = \".\""
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [],
   "source": [
    "dataset_url = \"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/4Z1fwRR295-1O3PMQBH6Dg/images-dataSAT.tar\""
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Data download\n",
    "We begin by downloading the dataset for evaluation of the models.\n",
    "Here, you declare:\n",
    "1. The dataset downloading primary function, based on `skillsnetwork` library.\n",
    "2. The dataset fallback downloading function, based on regular `http` downloading functions.\n",
    "3. Download the dataset\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Write permissions available for downloading and extracting the dataset tar file\n"
     ]
    },
    {
     "data": {
      "application/vnd.jupyter.widget-view+json": {
       "model_id": "953c759d533d4128a41163eebc29aeff",
       "version_major": 2,
       "version_minor": 0
      },
      "text/plain": [
       "Downloading images-dataSAT.tar:   0%|          | 0/20243456 [00:00<?, ?it/s]"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    },
    {
     "data": {
      "application/vnd.jupyter.widget-view+json": {
       "model_id": "4a46458989de4211b18bc9289c21cf9c",
       "version_major": 2,
       "version_minor": 0
      },
      "text/plain": [
       "  0%|          | 0/6003 [00:00<?, ?it/s]"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Saved to '.'\n"
     ]
    }
   ],
   "source": [
    "import os\n",
    "import skillsnetwork\n",
    "\n",
    "def check_skillnetwork_extraction(extract_dir):\n",
    "    \"\"\"Check if the environment allows symlink creation for download/extraction.\"\"\"\n",
    "    symlink_test = os.path.join(extract_dir, \"symlink_test\")\n",
    "    if not os.path.exists(symlink_test):\n",
    "        os.symlink(os.path.join(os.sep, \"tmp\"), symlink_test)\n",
    "        print(\"Write permissions available for downloading and extracting the dataset tar file\")\n",
    "        os.unlink(symlink_test)\n",
    "\n",
    "async def download_tar_dataset(url, tar_path, extract_dir):\n",
    "    \"\"\"Download and extract dataset tar file asynchronously.\"\"\"\n",
    "    if not os.path.exists(tar_path):\n",
    "        try:\n",
    "            print(f\"Downloading from {url}...\")\n",
    "            import httpx\n",
    "            async with httpx.AsyncClient() as client:\n",
    "                response = await client.get(url, follow_redirects=True)\n",
    "                response.raise_for_status()\n",
    "                with open(tar_path, \"wb\") as f:\n",
    "                    f.write(response.content)\n",
    "            print(f\"Successfully downloaded '{tar_path}'.\")\n",
    "        except Exception as e:\n",
    "            print(f\"Download error: {e}\")\n",
    "    else:\n",
    "        print(f\"Dataset tar file already exists at: {tar_path}\")\n",
    "    import tarfile\n",
    "    with tarfile.open(tar_path, 'r:*') as tar_ref:\n",
    "        tar_ref.extractall(path=extract_dir)\n",
    "        print(f\"Successfully extracted to '{extract_dir}'.\")\n",
    "\n",
    "try:\n",
    "    check_skillnetwork_extraction(data_dir)\n",
    "    await skillsnetwork.prepare(url=dataset_url, path=data_dir, overwrite=True)\n",
    "except Exception as e:\n",
    "    print(e)\n",
    "    print(\"Primary download/extraction method failed.\")\n",
    "    print(\"Falling back to manual download and extraction...\")\n",
    "    import tarfile\n",
    "    import httpx\n",
    "    from pathlib import Path\n",
    "    file_name = Path(dataset_url).name\n",
    "    tar_path = os.path.join(data_dir, file_name)\n",
    "    await download_tar_dataset(dataset_url, tar_path, data_dir)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Pre-trained model download \n",
    "\n",
    "Now, define an asynchronous function to download model files from given URLs, if they are not already present locally. \n",
    "You use `httpx` for asynchronous HTTP requests with error handling.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [],
   "source": [
    "async def download_model(url, model_path):\n",
    "    if not os.path.exists(model_path):\n",
    "        try:\n",
    "            print(f\"Downloading from {url}...\")\n",
    "            import httpx\n",
    "            async with httpx.AsyncClient() as client:\n",
    "                response = await client.get(url, follow_redirects=True)\n",
    "                response.raise_for_status()\n",
    "                with open(model_path, \"wb\") as f:\n",
    "                    f.write(response.content)\n",
    "            print(f\"Successfully downloaded '{model_path}'.\")\n",
    "        except Exception as e:\n",
    "            print(f\"Download error: {e}\")\n",
    "    else:\n",
    "        print(f\"Model file already downloaded at: {model_path}\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Model paths and download\n",
    "\n",
    "In the cell below, you define the file paths and URLs for the Keras and PyTorch models and download them using the `download_model` function defined above.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Model file already downloaded at: ./keras_cnn_vit_ai_capstone.keras\n",
      "Model file already downloaded at: ./pytorch_cnn_vit_ai_capstone_model_state_dict.pth\n"
     ]
    }
   ],
   "source": [
    "data_dir = \".\"\n",
    "\n",
    "keras_model_url = \"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/7uNMQhNyTA8qSSDGn5Cc7A/keras-cnn-vit-ai-capstone.keras\"\n",
    "keras_model_name = \"keras_cnn_vit_ai_capstone.keras\"\n",
    "keras_model_path = os.path.join(data_dir, keras_model_name)\n",
    "\n",
    "pytorch_state_dict_url = \"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/rFBrDlu1NNcAzir5Uww8eg/pytorch-cnn-vit-ai-capstone-model-state-dict.pth\"\n",
    "pytorch_state_dict_name = \"pytorch_cnn_vit_ai_capstone_model_state_dict.pth\"\n",
    "pytorch_state_dict_path = os.path.join(data_dir, pytorch_state_dict_name)\n",
    "\n",
    "await download_model(keras_model_url, keras_model_path)\n",
    "await download_model(pytorch_state_dict_url, pytorch_state_dict_path)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Package installation\n",
    "\n",
    "### Install PyTorch, SkLearn library and Python Packages for evaluation metrics\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "CPU times: user 15.1 ms, sys: 13.5 ms, total: 28.5 ms\n",
      "Wall time: 2.51 s\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "%%capture captured_output\n",
    "%pip install scikit-learn==1.7.0 tensorflow==2.19 numpy==1.26 matplotlib==3.9.2 skillsnetwork\n",
    "%pip install torch==2.8.0+cpu torchvision==0.23.0+cpu torchaudio==2.8.0+cpu \\\n",
    "    --index-url https://download.pytorch.org/whl/cpu"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Library imports and setup\n",
    "\n",
    "Import essential libraries for data manipulation, visualization, and suppresses warnings for cleaner notebook output.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "CPU times: user 391 ms, sys: 176 ms, total: 567 ms\n",
      "Wall time: 599 ms\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "import warnings\n",
    "warnings.filterwarnings('ignore')\n",
    "\n",
    "import os\n",
    "import time\n",
    "import httpx\n",
    "import random\n",
    "import numpy as np\n",
    "from tqdm import tqdm\n",
    "import matplotlib.pyplot as plt\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### TensorFlow/Keras library imports\n",
    "\n",
    "These imports set the environment variables to reduce TensorFlow logging noise and imports Keras modules for model building and training. They detect GPU availability for device assignment.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "WARNING: All log messages before absl::InitializeLog() is called are written to STDERR\n",
      "E0000 00:00:1771692077.050273     943 cuda_dnn.cc:8579] Unable to register cuDNN factory: Attempting to register factory for plugin cuDNN when one has already been registered\n",
      "E0000 00:00:1771692077.056650     943 cuda_blas.cc:1407] Unable to register cuBLAS factory: Attempting to register factory for plugin cuBLAS when one has already been registered\n",
      "W0000 00:00:1771692077.074163     943 computation_placer.cc:177] computation placer already registered. Please check linkage and avoid linking the same target more than once.\n",
      "W0000 00:00:1771692077.074188     943 computation_placer.cc:177] computation placer already registered. Please check linkage and avoid linking the same target more than once.\n",
      "W0000 00:00:1771692077.074190     943 computation_placer.cc:177] computation placer already registered. Please check linkage and avoid linking the same target more than once.\n",
      "W0000 00:00:1771692077.074192     943 computation_placer.cc:177] computation placer already registered. Please check linkage and avoid linking the same target more than once.\n"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "TensorFlow 2.19.0  |  GPUs found: []\n",
      "CPU times: user 2.48 s, sys: 384 ms, total: 2.86 s\n",
      "Wall time: 2.88 s\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "os.environ['TF_ENABLE_ONEDNN_OPTS'] = '0'\n",
    "os.environ['TF_CPP_MIN_LOG_LEVEL'] = '3'\n",
    "\n",
    "import tensorflow as tf\n",
    "from tensorflow.keras import layers\n",
    "from tensorflow.keras.preprocessing.image import ImageDataGenerator\n",
    "from tensorflow.keras.models import load_model\n",
    "\n",
    "gpu_list = tf.config.list_physical_devices('GPU')\n",
    "device = \"gpu\" if gpu_list != [] else \"cpu\"\n",
    "print(f\"TensorFlow {tf.__version__}  |  GPUs found: {tf.config.list_physical_devices('GPU')}\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### PyTorch library imports\n",
    "\n",
    "Import core PyTorch modules for model building, optimization, data loading, and functional utilities.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Imported libraries\n",
      "CPU times: user 2.08 s, sys: 457 ms, total: 2.54 s\n",
      "Wall time: 2.69 s\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "import torch\n",
    "import torch.nn as nn\n",
    "#import torch.optim as optim\n",
    "from torchvision import transforms\n",
    "from torchvision import datasets\n",
    "from torch.utils.data import DataLoader\n",
    "from torch.utils.data import  random_split\n",
    "import torch.nn.functional as F\n",
    "\n",
    "print(\"Imported libraries\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Fix random seed for reproducibility\n",
    "\n",
    "Define `set_seed` to ensure reproducibility across Python, NumPy, TensorFlow, and PyTorch by seeding random generators and enabling deterministic cuDNN. \n",
    "\n",
    "Set `SEED` to 7331. This is useful for consistent results in stochastic processes like training or inference.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Global seed set to 7331 - Processes are now deterministic.\n"
     ]
    }
   ],
   "source": [
    "#====================\n",
    "def set_seed(seed: int = 42) -> None:\n",
    "    \"\"\"Seed Python, NumPy, tensorflow, and PyTorch (CPU & all GPUs) and\n",
    "    make cuDNN run in deterministic mode.\"\"\"\n",
    "    # ---- Python and NumPy -------------------------------------------\n",
    "    random.seed(seed)\n",
    "    np.random.seed(seed)\n",
    "\n",
    "    # ---- Tensorflow -------------------------------------------------\n",
    "    tf.random.set_seed(seed)\n",
    "\n",
    "    # ---- PyTorch (CPU  &  GPU) --------------------------------------\n",
    "    torch.manual_seed(seed)            \n",
    "    torch.cuda.manual_seed_all(seed)   \n",
    "\n",
    "    # ---- cuDNN: force repeatable convolutions -----------------------\n",
    "    torch.backends.cudnn.deterministic = True \n",
    "    torch.backends.cudnn.benchmark     = False \n",
    "\n",
    "#====================\n",
    "SEED = 7331\n",
    "set_seed(SEED)\n",
    "print(f\"Global seed set to {SEED} - Processes are now deterministic.\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Model paths \n",
    "Check for the existence of the Keras and PyTorch model files. This ensures models are accessible before loading, preventing runtime errors. Use absolute paths for reliability.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Found the pre-trained Keras model:\n",
      "keras_cnn_vit_ai_capstone.keras --at------> ./keras_cnn_vit_ai_capstone.keras\n",
      "Found the pre-trained PyTorch model:\n",
      "pytorch_cnn_vit_ai_capstone_model_state_dict.pth --at------> ./pytorch_cnn_vit_ai_capstone_model_state_dict.pth\n"
     ]
    }
   ],
   "source": [
    "if not os.path.exists(keras_model_path):\n",
    "    print(\"Unable to find the Keras model at give path. Please check...\")\n",
    "else:\n",
    "    print(f\"Found the pre-trained Keras model:\\n{keras_model_name} --at------> {keras_model_path}\")\n",
    "\n",
    "if not os.path.exists(pytorch_state_dict_path):\n",
    "    print(\"Unable to find the PyTorch model at give path. Please check...\")\n",
    "else:\n",
    "    print(f\"Found the pre-trained PyTorch model:\\n{pytorch_state_dict_name} --at------> {pytorch_state_dict_path}\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Defining PyTorch model architecture\n",
    "In this cell, you will define the PyTorch CNN-ViT model architegcture, exactly as defined during the model training. You define the classes for CNN feature extractor, patch embedding, multi-head self-attention, transformer block, ViT, and CNN-ViT hybrid. \n",
    "\n",
    "The `evaluate` function computes loss and accuracy. This architecture combines CNN local features with ViT global attention. \n",
    "\n",
    "Parameters like depth and heads are configurable, and defined same as during training.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {},
   "outputs": [],
   "source": [
    "#====================\n",
    "class ConvNet(nn.Module):\n",
    "    ''' \n",
    "    Class to define the architecture same as the imported pre-trained CNN model\n",
    "    '''\n",
    "    def __init__(self, num_classes: int):\n",
    "        super().__init__()\n",
    "        # -------- convolutional feature extractor --------\n",
    "        self.features = nn.Sequential(\n",
    "            nn.Conv2d(3, 32,  kernel_size=5, padding=2), nn.ReLU(inplace=True), nn.MaxPool2d(2), nn.BatchNorm2d(32),\n",
    "            nn.Conv2d(32, 64,  kernel_size=5, padding=2), nn.ReLU(inplace=True), nn.MaxPool2d(2), nn.BatchNorm2d(64),\n",
    "            nn.Conv2d(64, 128, kernel_size=5, padding=2), nn.ReLU(inplace=True), nn.MaxPool2d(2), nn.BatchNorm2d(128),\n",
    "            nn.Conv2d(128, 256, kernel_size=5, padding=2), nn.ReLU(inplace=True), nn.MaxPool2d(2), nn.BatchNorm2d(256),\n",
    "            nn.Conv2d(256, 512, kernel_size=5, padding=2), nn.ReLU(inplace=True), nn.MaxPool2d(2), nn.BatchNorm2d(512),\n",
    "            nn.Conv2d(512, 1024, kernel_size=5, padding=2), nn.ReLU(inplace=True), nn.MaxPool2d(2), nn.BatchNorm2d(1024),\n",
    "        )\n",
    "\n",
    "        # -------- global pooling + classifier head --------\n",
    "        self.pool = nn.AdaptiveAvgPool2d((1, 1))\n",
    "        self.classifier = nn.Sequential(nn.Flatten(),                           # flatten feature map of dimensions (1024 × 1 × 1) to 1024\n",
    "                                        nn.Linear(1024, 2048), nn.ReLU(inplace=True), nn.BatchNorm1d(2048), nn.Dropout(0.4), \n",
    "                                        nn.Linear(2048, num_classes)\n",
    "                                       )\n",
    "\n",
    "    def forward_features(self, x: torch.Tensor) -> torch.Tensor:\n",
    "        return self.features(x)\n",
    "    \n",
    "    def forward(self, x: torch.Tensor) -> torch.Tensor:\n",
    "        x = self.forward_features(x)   # features, dimensions:(B, 1024, H', W')\n",
    "        x = self.pool(x)               # global-average-pooling, dimensions: (B, 1024, 1, 1)\n",
    "        x = self.classifier(x)         # classifier, dimensions: (B, num_classes)\n",
    "        return x\n",
    "\n",
    "#====================\n",
    "class PatchEmbed(nn.Module):\n",
    "    def __init__(self, input_channel=1024, embed_dim=768):\n",
    "        super().__init__()\n",
    "        self.proj = nn.Conv2d(input_channel, embed_dim, kernel_size=1)  # 1×1 conv\n",
    "    \n",
    "    def forward(self, x):\n",
    "        x = self.proj(x).flatten(2).transpose(1, 2)  # (B,L,D)\n",
    "        return x\n",
    "\n",
    "#====================\n",
    "class MHSA(nn.Module):\n",
    "    def __init__(self, dim, heads=8, dropout=0.):\n",
    "        super().__init__()\n",
    "        self.heads = heads\n",
    "        self.scale = (dim // heads) ** -0.5\n",
    "        self.qkv = nn.Linear(dim, dim * 3)\n",
    "        self.attn_drop = nn.Dropout(dropout)\n",
    "        self.proj = nn.Linear(dim, dim)\n",
    "        self.proj_drop = nn.Dropout(dropout)\n",
    "    \n",
    "    def forward(self, x):\n",
    "        B, N, D = x.shape\n",
    "        q, k, v = self.qkv(x).chunk(3, dim=-1)\n",
    "        q = q.reshape(B, N, self.heads, -1).transpose(1, 2)  # (B, heads, N, d)\n",
    "        k = k.reshape(B, N, self.heads, -1).transpose(1, 2)\n",
    "        v = v.reshape(B, N, self.heads, -1).transpose(1, 2)\n",
    "        attn = torch.matmul(q, k.transpose(-2, -1)) * self.scale\n",
    "        attn = self.attn_drop(attn.softmax(dim=-1))\n",
    "        x = torch.matmul(attn, v).transpose(1, 2).reshape(B, N, D)\n",
    "        return self.proj_drop(self.proj(x))\n",
    "\n",
    "#====================\n",
    "class TransformerBlock(nn.Module):\n",
    "    def __init__(self, dim, heads, mlp_ratio=4., dropout=0.):\n",
    "        super().__init__()\n",
    "        self.norm1 = nn.LayerNorm(dim)\n",
    "        self.attn  = MHSA(dim, heads, dropout)\n",
    "        self.norm2 = nn.LayerNorm(dim)\n",
    "        self.mlp   = nn.Sequential(\n",
    "                                    nn.Linear(dim, int(dim * mlp_ratio)),\n",
    "                                    nn.GELU(), nn.Dropout(dropout),\n",
    "                                    nn.Linear(int(dim * mlp_ratio), dim),\n",
    "                                    nn.Dropout(dropout))\n",
    "    \n",
    "    def forward(self, x):\n",
    "        x = x + self.attn(self.norm1(x))\n",
    "        x = x + self.mlp(self.norm2(x))\n",
    "        return x\n",
    "\n",
    "#====================\n",
    "class ViT(nn.Module):\n",
    "    def __init__(self, in_ch=1024, num_classes=2,\n",
    "                 embed_dim=768, depth=6, heads=8,\n",
    "                 mlp_ratio=4., dropout=0.1, max_tokens=50):\n",
    "        super().__init__()\n",
    "        self.patch = PatchEmbed(in_ch, embed_dim)           # 1×1 conv\n",
    "        self.cls   = nn.Parameter(torch.zeros(1, 1, embed_dim))\n",
    "        self.pos   = nn.Parameter(torch.randn(1, max_tokens, embed_dim))\n",
    "        self.blocks = nn.ModuleList([\n",
    "            TransformerBlock(embed_dim, heads, mlp_ratio, dropout)\n",
    "            for _ in range(depth)])\n",
    "        self.norm = nn.LayerNorm(embed_dim)\n",
    "        self.head = nn.Linear(embed_dim, num_classes)\n",
    "\n",
    "    def forward(self, x):                          # x: (B,C,H,W)\n",
    "        x = self.patch(x)                          # (B,L,D)\n",
    "        B, L, _ = x.shape\n",
    "        cls = self.cls.expand(B, -1, -1)           # (B,1,D)\n",
    "        x = torch.cat((cls, x), 1)                 # (B,L+1,D)\n",
    "        x = x + self.pos[:, :L + 1]                # match seq-len\n",
    "        for blk in self.blocks:\n",
    "            x = blk(x)\n",
    "        return self.head(self.norm(x)[:, 0])       # CLS token\n",
    "\n",
    "#====================\n",
    "class CNN_ViT_Hybrid(nn.Module):\n",
    "    def __init__(self, num_classes=2, embed_dim=768, depth=6, heads=8):\n",
    "        super().__init__()\n",
    "        self.cnn = ConvNet(num_classes)            # load weights later\n",
    "        self.vit = ViT(num_classes=num_classes,\n",
    "                       embed_dim=embed_dim,\n",
    "                       depth=depth,\n",
    "                       heads=heads)\n",
    "    \n",
    "    def forward(self, x):\n",
    "        return self.vit(self.cnn.forward_features(x))\n",
    "\n",
    "#====================\n",
    "def evaluate(model, loader, criterion, device):\n",
    "    with torch.no_grad():\n",
    "        model.eval()\n",
    "        loss_sum, correct = 0, 0\n",
    "        for batch_idx, (x, y) in enumerate(tqdm(loader, desc=\"Validation\")):\n",
    "            x, y = x.to(device), y.to(device)\n",
    "            out = model(x)\n",
    "            loss = criterion(out, y)\n",
    "            loss_sum += loss.item() * x.size(0)\n",
    "            correct  += (out.argmax(1) == y).sum().item()\n",
    "    return loss_sum / len(loader.dataset), correct / len(loader.dataset)# Set device"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Dataset path and hyperparameters\n",
    "Here, you set the dataset path and hyperparameters like image size, channels, batch size, classes, and labels. These are used for data loading and model configuration. Consistent dimensions ensure compatibility with model inputs.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Task 1: Define the dataset directory, dataloader and model hyperparameters. The dataloader and model hyperparameters should be same as used during training \n",
    "\n",
    "- Define the `dataset_path`\n",
    "\n",
    "- Define **hyperparameters common dataloader**\n",
    "    - `img_w`, `img_h = 64, 64`\n",
    "    - `batch_size = 128`\n",
    "    - `num_classes = 2`\n",
    "    - `agri_class_labels = [\"non-agri\", \"agri\"]`\n",
    "\n",
    "  \n",
    "- Define **hyperparameters for PyTorch CNN-Vit Hybrid model**. The values have to same as those used while training the hybrid model. \n",
    "    - `depth = 3`\n",
    "    - `attn_heads = 6`\n",
    "    - `embed_dim = 768`\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [],
   "source": [
    "## Please use the space below to write your answer\n",
    "dataset_path = os.path.join(data_dir, \"images_dataSAT\")\n",
    "\n",
    "# hyperparameters common dataloader\n",
    "img_w, img_h = 64, 64\n",
    "batch_size = 128\n",
    "num_classes = 2\n",
    "agri_class_labels = [\"non-agri\", \"agri\"]\n",
    "\n",
    "# hyperparameters for PyTorch CNN-Vit Hybrid model\n",
    "depth = 3\n",
    "attn_heads = 6\n",
    "embed_dim = 768"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Double-click **here** for the solution.\n",
    "<!--\n",
    "dataset_path = os.path.join(data_dir, \"images_dataSAT\")\n",
    "\n",
    "# hyperparameters common dataloader\n",
    "img_w, img_h = 64, 64\n",
    "batch_size = 128\n",
    "num_classes = 2\n",
    "agri_class_labels = [\"non-agri\", \"agri\"]\n",
    "\n",
    "# hyperparameters for PyTorch CNN-Vit Hybrid model\n",
    "depth = 3\n",
    "attn_heads = 6\n",
    "embed_dim = 768\n",
    "-->\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### PyTorch Dataloader\n",
    "Defines transforms for resizing, tensor conversion, and normalization (ImageNet means/std). \n",
    "\n",
    "Loads dataset with ImageFolder and creates DataLoader for batching without shuffling for evaluation.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {},
   "outputs": [],
   "source": [
    "train_transform = transforms.Compose([\n",
    "    transforms.Resize((img_w, img_h)),\n",
    "    transforms.ToTensor(),\n",
    "    transforms.Normalize([0.485, 0.456, 0.406], [0.229, 0.224, 0.225])\n",
    "])\n",
    "full_dataset = datasets.ImageFolder(dataset_path, transform=train_transform)\n",
    "test_loader = DataLoader(full_dataset, batch_size=batch_size, shuffle=False)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Task 2: Instantiate PyTorch model\n",
    "Check the availability of CUDA device and set the `device` parameter accordingly.\n",
    "\n",
    "Based on the `CNN_ViT_Hybrid` function, instantiate the PyTorch model and move the model to the available `device`\n",
    "\n",
    "In this cell, you will:\n",
    "1. instantiate the PyTorch CNN_ViT_Hybrid with the previously declared model parameters\n",
    "3. detect the device for model inference\n",
    " \n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {},
   "outputs": [],
   "source": [
    "## Please use the space below to write your answer\n",
    "# Check device availability\n",
    "device = \"cuda\" if torch.cuda.is_available() else \"cpu\"\n",
    "\n",
    "# Create model instance\n",
    "pytorch_model = CNN_ViT_Hybrid(num_classes=num_classes,\n",
    "                      heads=attn_heads,\n",
    "                      depth=depth,\n",
    "                      embed_dim=embed_dim).to(device)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Double-click **here** for the solution.\n",
    "<!--\n",
    "# Check device availability\n",
    "device = \"cuda\" if torch.cuda.is_available() else \"cpu\"\n",
    "\n",
    "# Create model instance\n",
    "pytorch_model = CNN_ViT_Hybrid(num_classes=num_classes,\n",
    "                      heads=attn_heads,\n",
    "                      depth=depth,\n",
    "                      embed_dim=embed_dim).to(device)\n",
    "-->\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Evaluating the PyTorch model on cpu\n"
     ]
    }
   ],
   "source": [
    "print(f\"Evaluating the PyTorch model on {device}\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### --- PyTorch pre-trained ViT model loading ---\n",
    "In this cell, you will load the PyTorch model state dict with **`strict=False`** for flexibility.\n",
    "\n",
    "Thus, you prepare the model for inference.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Loaded model state dict, now getting predictions\n"
     ]
    }
   ],
   "source": [
    "# Load pre-trained CNN-ViT hybrid model weights \n",
    "if device==\"cpu\":\n",
    "    map_location=torch.device(\"cpu\")\n",
    "else:\n",
    "    map_location=torch.device(\"cuda\")\n",
    "\n",
    "pytorch_model.load_state_dict(torch.load(pytorch_state_dict_path, map_location=map_location), strict=False)\n",
    "print(\"Loaded model state dict, now getting predictions\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### PyTorch model inference metrics\n",
    "\n",
    "Now, you perform:\n",
    "1. inference on test_loader\n",
    "2. collecte prediction, labels, and probabilities (for class 1)\n",
    "3. Uses no_grad for efficiency and eval mode\n",
    "4. Use tqdm to show progress.\n",
    "5. Move the data to the training device (CPU/GPU).\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "Step: 100%|██████████| 47/47 [01:12<00:00,  1.54s/it]"
     ]
    },
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "CPU times: user 55.2 s, sys: 15.6 s, total: 1min 10s\n",
      "Wall time: 1min 12s\n"
     ]
    },
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "all_preds_pytorch = []\n",
    "all_labels_pytorch = []\n",
    "all_probs_pytorch = []\n",
    "\n",
    "pytorch_model.eval()\n",
    "with torch.no_grad():\n",
    "    for batch_idx, (images, labels) in enumerate(tqdm(test_loader, desc=\"Step\")):\n",
    "#    for images, labels in test_loader:\n",
    "        images = images.to(device)\n",
    "        outputs = pytorch_model(images)\n",
    "        preds = torch.argmax(outputs, dim=1)\n",
    "        probs = F.softmax(outputs, dim=1)[:, 1]  # probability for class 1\n",
    "        all_probs_pytorch.extend(probs.cpu())\n",
    "        all_preds_pytorch.extend(preds.cpu().numpy().flatten())\n",
    "        all_labels_pytorch.extend(labels.numpy())"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Keras model loading\n",
    "\n",
    "To load the Keras based CNN-ViT hybrid model, you will\n",
    "\n",
    "- define **custom Keras layers** with serialization for model saving/loading for:\n",
    "    - `position embedding`\n",
    "    - `transformer block`\n",
    "\n",
    "This step is essential for reconstructing the ViT architecture in Keras.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {},
   "outputs": [],
   "source": [
    "# Positional embedding that Keras can track\n",
    "@tf.keras.utils.register_keras_serializable(package=\"Custom\")\n",
    "class AddPositionEmbedding(layers.Layer):\n",
    "    def __init__(self, num_patches, embed_dim, **kwargs):\n",
    "        super(AddPositionEmbedding, self).__init__(**kwargs)\n",
    "        self.num_patches = num_patches\n",
    "        self.embed_dim   = embed_dim\n",
    "        self.pos = self.add_weight(\n",
    "            name=\"pos_embedding\",\n",
    "            shape=(1, num_patches, embed_dim),\n",
    "            initializer=\"random_normal\",\n",
    "            trainable=True)\n",
    "\n",
    "    def call(self, tokens):\n",
    "        return tokens + self.pos\n",
    "\n",
    "    def get_config(self):\n",
    "        config = super().get_config()\n",
    "        config.update({\n",
    "            \"num_patches\": self.num_patches,\n",
    "            \"embed_dim\":   self.embed_dim,\n",
    "        })\n",
    "        return {**config}\n",
    "\n",
    "# One Transformer encoder block\n",
    "@tf.keras.utils.register_keras_serializable(package=\"Custom\")\n",
    "class TransformerBlock(layers.Layer):\n",
    "    def __init__(self, embed_dim, num_heads=8, mlp_dim=2048, dropout=0.1, **kwargs):\n",
    "        super(TransformerBlock, self).__init__(**kwargs)\n",
    "        self.embed_dim = embed_dim\n",
    "        self.num_heads = num_heads\n",
    "        self.mlp_dim   = mlp_dim\n",
    "        self.dropout   = dropout\n",
    "        self.mha  = layers.MultiHeadAttention(num_heads, key_dim=embed_dim)\n",
    "        self.norm1 = layers.LayerNormalization(epsilon=1e-6)\n",
    "        self.norm2 = layers.LayerNormalization(epsilon=1e-6)\n",
    "        self.mlp = tf.keras.Sequential([\n",
    "            layers.Dense(mlp_dim, activation=\"gelu\"),\n",
    "            layers.Dropout(dropout),\n",
    "            layers.Dense(embed_dim),\n",
    "            layers.Dropout(dropout)\n",
    "        ])\n",
    "\n",
    "    def call(self, x):\n",
    "        x = self.norm1(x + self.mha(x, x))\n",
    "        return self.norm2(x + self.mlp(x))\n",
    "\n",
    "    # ---- NEW ----\n",
    "    def get_config(self):\n",
    "        config = super().get_config()\n",
    "        config.update({\n",
    "            \"embed_dim\":  self.embed_dim,\n",
    "            \"num_heads\":  self.num_heads,\n",
    "            \"mlp_dim\":    self.mlp_dim,\n",
    "            \"dropout\":    self.dropout,\n",
    "        })\n",
    "        return {**config}"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### --- Keras pre-trained ViT model loading ---\n",
    "\n",
    "Here, you will load the pre-trained Keras model using **`load_model`**, providing **custom objects** for deserialization of user-defined layers. This enables inference with the hybrid model.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "metadata": {},
   "outputs": [],
   "source": [
    "# ------------------- load CNN-ViT hybrid model ------------------\n",
    "keras_model = load_model(keras_model_name,\n",
    "                         custom_objects={\n",
    "                         \"AddPositionEmbedding\": AddPositionEmbedding,\n",
    "                         \"TransformerBlock\":     TransformerBlock\n",
    "                          })"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Define dataloader\n",
    "\n",
    "In this cell, you create an ImageDataGenerator for rescaling and a generator for flowing images from directory, matching PyTorch setup for consistent evaluation.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Found 6000 images belonging to 2 classes.\n"
     ]
    }
   ],
   "source": [
    "datagen = ImageDataGenerator(rescale=1./255)\n",
    "prediction_generator = datagen.flow_from_directory(\n",
    "    dataset_path,\n",
    "    target_size=(img_w, img_h),\n",
    "    batch_size=batch_size,\n",
    "    class_mode=\"binary\",\n",
    "    shuffle=False\n",
    ")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Collecting metrics for Keras-based CNN-ViT hybrid model\n",
    "Now, run the inference of the Keras-based CNN-ViT hybrid model and collect the evaluation metrics.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "\u001b[1m47/47\u001b[0m \u001b[32m━━━━━━━━━━━━━━━━━━━━\u001b[0m\u001b[37m\u001b[0m \u001b[1m148s\u001b[0m 3s/step\n",
      "CPU times: user 2min 14s, sys: 7.1 s, total: 2min 21s\n",
      "Wall time: 2min 28s\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "\n",
    "all_probs_keras = keras_model.predict(prediction_generator, verbose=1)\n",
    "all_preds_keras = np.argmax(all_probs_keras, axis=1)\n",
    "all_labels_keras = prediction_generator.classes"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Import the evaluation metrics\n",
    "\n",
    "Here you define the functions to compute and print classification metrics including accuracy, precision, recall, F1 score, ROC-AUC, confusion matrix, and log loss. These functions support both Keras and PyTorch model outputs.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "CPU times: user 28.7 ms, sys: 20.9 ms, total: 49.5 ms\n",
      "Wall time: 59.9 ms\n"
     ]
    }
   ],
   "source": [
    "%%time\n",
    "from sklearn.metrics import (accuracy_score,\n",
    "                             precision_score,\n",
    "                             recall_score,\n",
    "                             f1_score,\n",
    "                             roc_curve, \n",
    "                             roc_auc_score,\n",
    "                             log_loss,\n",
    "                             classification_report,\n",
    "                             confusion_matrix,\n",
    "                             ConfusionMatrixDisplay,\n",
    "                            )\n",
    "from sklearn.preprocessing import label_binarize\n",
    "\n",
    "# define a function to get the metrics comprehensively\n",
    "def model_metrics(y_true, y_pred, y_prob, class_labels):\n",
    "    y_prob = np.array(y_prob)\n",
    "    if len(y_prob.shape)<2:\n",
    "        roc_score = roc_auc_score(y_true, y_prob)\n",
    "    elif len(y_prob.shape)==2:\n",
    "        roc_score = roc_auc_score(y_true, y_prob[:,1])\n",
    "    else:\n",
    "        roc_score = np.nan\n",
    "    metrics = {'Accuracy': accuracy_score(y_true, y_pred),\n",
    "               'Precision': precision_score(y_true, y_pred),\n",
    "               'Recall': recall_score(y_true, y_pred),\n",
    "               'Loss': log_loss(y_true, y_prob),\n",
    "               'F1 Score': f1_score(y_true, y_pred),\n",
    "               'ROC-AUC': roc_score,\n",
    "               'Confusion Matrix': confusion_matrix(y_true, y_pred),\n",
    "               'Classification Report': classification_report(y_true, y_pred, target_names=class_labels, digits=4),\n",
    "               \"Class labels\": class_labels\n",
    "              }\n",
    "    return metrics\n",
    "\n",
    "#function to print the metrics\n",
    "def print_metrics(y_true, y_pred, y_prob, class_labels, model_name):\n",
    "    metrics = model_metrics(y_true, y_pred, y_prob, class_labels)\n",
    "    \n",
    "    print(f\"Evaluation metrics for the \\033[1m{model_name}\\033[0m\")\n",
    "    print(f\"Accuracy: {'':<1}{metrics[\"Accuracy\"]:.4f}\")\n",
    "    if metrics[\"ROC-AUC\"] != np.nan:\n",
    "        print(f\"ROC-AUC: {'':<2}{metrics[\"ROC-AUC\"]:.4f}\")\n",
    "    print(f\"Loss: {'':<5}{metrics[\"Loss\"]:.4f}\\n\")\n",
    "    print(f\"Classification report:\\n\\n  {metrics[\"Classification Report\"]}\")\n",
    "    print(\"========= Confusion Matrix =========\")\n",
    "    disp = ConfusionMatrixDisplay(confusion_matrix=metrics[\"Confusion Matrix\"],\n",
    "                                  display_labels=metrics[\"Class labels\"])\n",
    "\n",
    "    disp.plot()\n",
    "    plt.show()\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Keras metrics reporting\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Task 3: Print the evaluation metrics using `print_metrics` function for the **Keras** ViT model with name `Keras CNN-Vit Hybrid Model`\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Evaluation metrics for the \u001b[1mKeras CNN-Vit Hybrid Model\u001b[0m\n",
      "Accuracy:  0.9958\n",
      "ROC-AUC:   0.9998\n",
      "Loss:      0.0530\n",
      "\n",
      "Classification report:\n",
      "\n",
      "                precision    recall  f1-score   support\n",
      "\n",
      "    non-agri     0.9927    0.9990    0.9958      3000\n",
      "        agri     0.9990    0.9927    0.9958      3000\n",
      "\n",
      "    accuracy                         0.9958      6000\n",
      "   macro avg     0.9959    0.9958    0.9958      6000\n",
      "weighted avg     0.9959    0.9958    0.9958      6000\n",
      "\n",
      "========= Confusion Matrix =========\n"
     ]
    },
    {
     "data": {
      "image/png": "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fPFFSdKMGTO0ePFizZ8/X7t27dLo0aN1++23a/369ZLKkq9+/fqpd+/eSk1N1d13360JEya4/DUJDAxUYmKifvjhB7344otasGCB5syZ4zBmz549WrZsmVauXKnVq1fru+++0/3332/fnpSUpEmTJmn69OlKS0vT008/rSeeeEKLFi1yOR4A1cgAUCMNHjzY6NOnj2EYhmGz2YyUlBTDarUajzzyiH17eHi4UVhYaN/nrbfeMqKjow2bzWZfV1hYaPj5+RmffPKJYRiG0aBBA2PWrFn27cXFxUajRo3s5zIMw+jSpYvxz3/+0zAMw0hPTzckGSkpKWeM8/PPPzckGb/++qt9XUFBgVGnTh1j06ZNDmOHDRtm3HbbbYZhGMajjz5qxMTEOGwfP378acf6M0nGBx98cNbts2fPNtq1a2f//OSTTxre3t7GoUOH7Os+/vhjw8vLyzh69KhhGIZx2WWXGUuWLHE4zrRp04z4+HjDMAxj//79hiTju+++O+t5AVQ/5tQANVhycrICAgJUXFwsm82mgQMHavLkyfbtsbGxDvNotm/frj179igwMNDhOAUFBdq7d69ycnJ09OhRdezY0b6tVq1aat++/WktqHKpqany9vZWly5dKhz3nj17dOrUKV133XUO64uKinTllVdKktLS0hzikKT4+PgKn6Pc0qVLNXfuXO3du1d5eXkqKSlRUFCQw5jGjRurYcOGDuex2WxKT09XYGCg9u7dq2HDhmn48OH2MSUlJQoODnY5HgDVh6QGqMG6deumV199VT4+PoqMjFStWo7/Zf39/R0+5+XlqV27dkpKSjrtWPXr1z+vGPz8/FzeJy8vT5L00UcfOSQTUtk8ocqyefNmDRo0SFOmTFFCQoKCg4P19ttv67nnnnM51gULFpyWZHl7e1darACqHkkNUIP5+/urefPmFR5/1VVXaenSpQoLCzutWlGuQYMG2rJlizp37iyprCKxbds2XXXVVWccHxsbK5vNpvXr16t79+6nbS+vFJWWltrXxcTEyGq1KiMj46wVnlatWtknPZf76quvzn2R/2PTpk1q0qSJJk6caF/3888/nzYuIyNDR44cUWRkpP08Xl5eio6OVnh4uCIjI7Vv3z4NGjTIpfMDqFmYKAx4kEGDBumSSy5Rnz59tGHDBu3fv1/r1q3Tgw8+qEOHDkmS/vnPf2rmzJlavny5fvzxR91///1OnzFz6aWXavDgwRo6dKiWL19uP+ayZcskSU2aNJHFYlFycrJ++eUX5eXlKTAwUI888ohGjx6tRYsWae/evfr222/10ksv2Sff3nvvvdq9e7fGjh2r9PR0LVmyRImJiS5db4sWLZSRkaG3335be/fu1dy5c8846dnX11eDBw/W9u3btWHDBj344IO65ZZbFBERIUmaMmWKZsyYoblz5+qnn37Sjh079Oabb+r55593KR4A1YukBvAgderU0RdffKHGjRurX79+atWqlYYNG6aCggJ75ebhhx/WHXfcocGDBys+Pl6BgYG66aabnB731Vdf1c0336z7779fLVu21PDhw5Wfny9JatiwoaZMmaIJEyYoPDxco0aNkiRNmzZNTzzxhGbMmKFWrVqpZ8+e+uijj9S0aVNJZfNc3nvvPS1fvlxt2rTR/Pnz9fTTT7t0vTfeeKNGjx6tUaNGqW3bttq0aZOeeOKJ08Y1b95c/fr10w033KAePXooLi7O4Zbtu+++WwsXLtSbb76p2NhYdenSRYmJifZYAZiDxTjb7EAAAAAToVIDAAA8AkkNAADwCCQ1AADAI5DUAAAAj0BSAwAAPAJJDQAA8AgkNQAAwCOQ1AAAAI9AUgMAADwCSQ0AAPAIJDUAAMAj/D9RpP+rklF0aAAAAABJRU5ErkJggg==",
      "text/plain": [
       "<Figure size 640x480 with 2 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "## Please use the space below to write your answer\n",
    "print_metrics(y_true = all_labels_keras,\n",
    "              y_pred = all_preds_keras,\n",
    "              y_prob = all_probs_keras,\n",
    "              class_labels = agri_class_labels,\n",
    "              model_name = \"Keras CNN-Vit Hybrid Model\"\n",
    "             )"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Double-click **here** for the solution.\n",
    "<!--\n",
    "print_metrics(y_true = all_labels_keras,\n",
    "              y_pred = all_preds_keras,\n",
    "              y_prob = all_probs_keras,\n",
    "              class_labels = agri_class_labels,\n",
    "              model_name = \"Keras CNN-Vit Hybrid Model\"\n",
    "             )\n",
    "-->\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## PyTorch metrics reporting\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Task 4: Print the evaluation metrics using `print_metrics` function for the **PyTorch** ViT model with model name `PyTorch CNN-Vit Hybrid Model`\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Evaluation metrics for the \u001b[1mPyTorch CNN-Vit Hybrid Model\u001b[0m\n",
      "Accuracy:  0.9990\n",
      "ROC-AUC:   1.0000\n",
      "Loss:      0.0047\n",
      "\n",
      "Classification report:\n",
      "\n",
      "                precision    recall  f1-score   support\n",
      "\n",
      "    non-agri     0.9990    0.9990    0.9990      3000\n",
      "        agri     0.9990    0.9990    0.9990      3000\n",
      "\n",
      "    accuracy                         0.9990      6000\n",
      "   macro avg     0.9990    0.9990    0.9990      6000\n",
      "weighted avg     0.9990    0.9990    0.9990      6000\n",
      "\n",
      "========= Confusion Matrix =========\n"
     ]
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAjUAAAGwCAYAAABRgJRuAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjkuMiwgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy8hTgPZAAAACXBIWXMAAA9hAAAPYQGoP6dpAABDXElEQVR4nO3de1wVdf7H8fcB5YBc1URE8ZaKkqClrvHbvG0mlpmmbeul0rKsTXPTvJVlppmmlWWllmZoi5vVlimVRpp3s7TF1Ii8BqVoqwGCcT3z+8M47Uk9cjwHYY6v5+Mxj4dn5jszn+GB8OHz+c6MxTAMQwAAACbnU9kBAAAAeAJJDQAA8AokNQAAwCuQ1AAAAK9AUgMAALwCSQ0AAPAKJDUAAMArVKvsAC53NptNR44cUXBwsCwWS2WHAwBwkWEYOnXqlCIjI+XjU3G1goKCAhUVFbl9HD8/P/n7+3sgoqqHpKaSHTlyRFFRUZUdBgDATZmZmWrQoEGFHLugoEBNGgUp63ip28eKiIjQoUOHvDKxIampZMHBwZKkH75urJAguoHwTre2iK3sEIAKU6JibdbH9p/nFaGoqEhZx0v1w87GCgm++N8VuadsatTusIqKikhq4HllLaeQIB+3vlGBqqyapXplhwBUnN9eNnQpphAEBVsUFHzx57HJu6c5kNQAAGASpYZNpW68sbHUsHkumCqIpAYAAJOwyZBNF5/VuLOvGdDvAAAAXoFKDQAAJmGTTe40kNzbu+ojqQEAwCRKDUOlxsW3kNzZ1wxoPwEAAK9ApQYAAJNgorBzJDUAAJiETYZKSWrOi/YTAADwClRqAAAwCdpPzpHUAABgEtz95BztJwAA4BWo1AAAYBK23xZ39vdmJDUAAJhEqZt3P7mzrxmQ1AAAYBKlhtx8S7fnYqmKmFMDAAC8ApUaAABMgjk1zpHUAABgEjZZVCqLW/t7M9pPAADAK1CpAQDAJGzGmcWd/b0ZSQ0AACZR6mb7yZ19zYD2EwAA8ApUagAAMAkqNc6R1AAAYBI2wyKb4cbdT27sawa0nwAAgFegUgMAgEnQfnKOpAYAAJMolY9K3WiylHowlqqIpAYAAJMw3JxTYzCnBgAAoOqjUgMAgEkwp8Y5khoAAEyi1PBRqeHGnBovf00C7ScAAOAVqNQAAGASNllkc6MeYZN3l2pIagAAMAnm1DhH+wkAAHgFKjUAAJiE+xOFaT8BAIAq4MycGjdeaEn7CQAAoOqjUgMAgEnY3Hz3E3c/AQCAKoE5Nc6R1AAAYBI2+fCcGieYUwMAALwClRoAAEyi1LCo1HDj4Xtu7GsGJDUAAJhEqZsThUtpPwEAAFR9VGoAADAJm+Ejmxt3P9m4+wkAAFQFtJ+co/0EAAC8ApUaAABMwib37mCyeS6UKomkBgAAk3D/4Xve3aDx7qsDAACXDSo1AACYhPvvfvLuWgZJDQAAJmGTRTa5M6eGJwoDAIAqgEqNc959dQAA4LJBUgMAgEmUPXzPncUVM2bMUIcOHRQcHKzw8HD17dtX6enpDmO6du0qi8XisDzwwAMOYzIyMtSrVy/VqFFD4eHhGjdunEpKShzGrF+/Xtdcc42sVquaNWumxMREl78+JDUAAJiEzbC4vbhiw4YNGjFihL744gulpKSouLhYPXr0UH5+vsO4++67T0ePHrUvs2bNsm8rLS1Vr169VFRUpK1bt2rJkiVKTEzU5MmT7WMOHTqkXr16qVu3bkpNTdXDDz+se++9V2vWrHEpXubUAABwmcnNzXX4bLVaZbVazxq3evVqh8+JiYkKDw/Xzp071blzZ/v6GjVqKCIi4pzn+vTTT/Xtt9/qs88+U926ddW2bVtNmzZNEyZM0JQpU+Tn56cFCxaoSZMmev755yVJrVq10ubNmzVnzhwlJCSU+7qo1AAAYBI2N1tPZQ/fi4qKUmhoqH2ZMWNGuc6fk5MjSapVq5bD+qSkJF1xxRVq3bq1Hn30UZ0+fdq+bdu2bYqNjVXdunXt6xISEpSbm6u9e/fax3Tv3t3hmAkJCdq2bZtLXx8qNQAAmIT7b+k+s29mZqZCQkLs689VpTlrX5tNDz/8sP785z+rdevW9vWDBg1So0aNFBkZqW+++UYTJkxQenq63n//fUlSVlaWQ0Ijyf45KyvL6Zjc3Fz9+uuvCggIKNf1kdQAAHCZCQkJcUhqymPEiBHas2ePNm/e7LB++PDh9n/HxsaqXr16uv7663XgwAFdeeWVHom3vGg/AQBgEqWyuL1cjJEjRyo5OVmff/65GjRo4HRsx44dJUn79++XJEVEROjYsWMOY8o+l83DOd+YkJCQcldpJJIaAABMo6z95M7iCsMwNHLkSH3wwQdat26dmjRpcsF9UlNTJUn16tWTJMXHx2v37t06fvy4fUxKSopCQkIUExNjH7N27VqH46SkpCg+Pt6leElqAADAOY0YMUL//Oc/tWzZMgUHBysrK0tZWVn69ddfJUkHDhzQtGnTtHPnTh0+fFgrV67UXXfdpc6dOysuLk6S1KNHD8XExOjOO+/Url27tGbNGj3++OMaMWKEfS7PAw88oIMHD2r8+PH67rvvNG/ePL3zzjsaPXq0S/GS1AAAYBKlcrcF5Zr58+crJydHXbt2Vb169ezL8uXLJUl+fn767LPP1KNHD7Vs2VKPPPKI+vfvr1WrVtmP4evrq+TkZPn6+io+Pl533HGH7rrrLk2dOtU+pkmTJvroo4+UkpKiNm3a6Pnnn9eiRYtcup1bYqIwAACm4am7n8rLMAyn26OiorRhw4YLHqdRo0b6+OOPnY7p2rWr/vOf/7gU3x+R1AAAYBK80NI57746AABw2aBSAwCASRiyyHaRt2WX7e/NSGoAADAJ2k/OeffVAQCAywaVGgAATMJmWGQzLr6F5M6+ZkBSAwCASZS9bdud/b2Zd18dAAC4bFCpAQDAJGg/OUdSAwCASdjkI5sbTRZ39jUD7746AABw2aBSAwCASZQaFpW60UJyZ18zIKkBAMAkmFPjHEkNAAAmYbj5lm6DJwoDAABUfVRqAAAwiVJZVOrGSynd2dcMSGoAADAJm+HevBib4cFgqiDaTwAAwCtQqYHpvP1yuLZ8HKbM/Vb5+dsU0/60hk06oqhmhfYxRw77aeHUSO39MkjFRRa165arEU//pJp1Suxj9n0ToDemR+r7XTXk42voupuydf+UIwoItEmSPl1eS8+PbnjOGJZ/s0dhV5SccxtQGW6+67/qddcJ1Y0qkiT9kO6vpDl1tePzkEqODJ5kc3OisDv7moF3X10lGDp0qPr27VvZYXi1b7YFqffQ/+rF5H2a8fYBlZZIjw28UgWnz3w7F5z20WMDr5TFIj377n698OE+lRT5aPKQJrKdyVd0IquaJg64UpFNCvVS8veannRAP6T767mHf09iutzyi/6Vusdhadc1V3HxeSQ0qHJ+Plpdi5+pp5E9W+ihG1to15YgTXnzsBq1KKjs0OBBNlncXrwZlRoPe+mll2QYXt60rGTPLDvo8PmRFzP0t9hY7fsmQLHX5mvvl4E6lumnVz9NV2DwmSxm3Es/qH+rWKVuDtI1nfO0/bNQVatmaOQzP8rnt9R+1LM/6oHrW+qnQ36q36RI1gBD1oDfk5fsE77atSVIo5/PvGTXCpTX9pRQh8+Jz9bTzXedUMt2+frhe/9Kigq4tKjUeEhpaalsNptCQ0MVFhZW2eFcVvJzfSVJwWGlkqTiIotkkar7/Z5cVrcasvhIe78MOjOm0KJq1Q17QiNJfv5nEqCyMX/02bu1ZA0w1KlXdgVcBeA5Pj6GuvT5RdYaNqXtCKzscOBBZU8UdmfxZpWa1HTt2lWjRo3S+PHjVatWLUVERGjKlCn27RkZGerTp4+CgoIUEhKi22+/XceOHbNvnzJlitq2bau33npLjRs3VmhoqAYMGKBTp045Pe9bb72l9u3bKzg4WBERERo0aJCOHz/uMGblypVq3ry5/P391a1bNy1ZskQWi0XZ2dmSpMTERIWFhWnlypWKiYmR1WpVRkYG7adLzGaTFjxZX1d1yFPjlmfK7C3b5cu/hk1vTI9UwWmLCk77aOHUSNlKLTp5/Exxss11efrl5+p6d14dFRdZdCrbV4ufiZQk+5g/WvOv2up26y+yBlCJQ9XUuOWvWrFvt5IPf6NRM3/U1GGNlbGPKo03KZtT487izSr96pYsWaLAwEBt375ds2bN0tSpU5WSkiKbzaY+ffro5MmT2rBhg1JSUnTw4EH97W9/c9j/wIEDWrFihZKTk5WcnKwNGzZo5syZTs9ZXFysadOmadeuXVqxYoUOHz6soUOH2rcfOnRIt912m/r27atdu3bp/vvv16RJk846zunTp/Xss89q0aJF2rt3r8LDwy94vYWFhcrNzXVYcPFeeayBfvguQI/O/8G+Lqx2qR5/7bC2p4Sob/M43Rodq/xcXzWLPS3Lb9/xjaMLNPbFH/Tv18J1y5VxGtj2KkVEFalmnWJZzvGHzLc7aihjn796Djxxia4McN2PB6x68IYWGtWruZKXXqGxL2WoYXPm1ODyUelzauLi4vTkk09Kkpo3b65XXnlFa9eulSTt3r1bhw4dUlRUlCRp6dKluuqqq/TVV1+pQ4cOkiSbzabExEQFBwdLku68806tXbtW06dPP+8577nnHvu/mzZtqrlz56pDhw7Ky8tTUFCQXnvtNUVHR2v27NmSpOjoaO3Zs+esYxYXF2vevHlq06ZNua93xowZeuqpp8o9Huf3ymP1tT0lRM9/sF91IosdtrXrekqJ29KUc8JXvtWkoNBSDWhzleo1/P0Oqb/0y9Zf+mXrl5+ryb+GTRaL9P7rdVSvUeEfT6XVy2rryqtOq3ncrxV+XcDFKin20ZHDVknS/t01FN32tPre+7PmToiq5MjgKTa5+e4nL58oXOmVmri4OIfP9erV0/Hjx5WWlqaoqCh7QiNJMTExCgsLU1pamn1d48aN7QnN/+4vSUlJSQoKCrIvmzZtkiTt3LlTvXv3VsOGDRUcHKwuXbpIOtPukqT09HR70lTmT3/601mx+/n5nRX/hTz66KPKycmxL5mZTDp1lWGcSWi2rg7VrHf3K6Jh0XnHhtYuVVBoqVI3Byn7v9V0bY+zK2M165QoINCmDR+GqbrVpms65zls/zXfRxtXhSlh4EmPXwtQkSx/mFsG8zPcvPPJ8PKkptIrNdWrV3f4bLFYZCu779bN/W+55RZ17NjRvq1+/frKz89XQkKCEhISlJSUpDp16igjI0MJCQkqKjr/L8dzCQgIkOVcvQonrFarrFarS/vA0SuPNdDnH9TUlDcPKiDIZp8DExhcap/vsubtWmrYvEChtUuUtjNQ8yfX163Df3Z4ls2Hi69QTPt8BQTa9PXGYC2aFql7HjuioNBSh/Nt+DBMpaUWXd//l0t3kYCL7n70qL5aF6yff/JTQFCput2arbj/y9OkQU0rOzR4EG/pdq7Sk5rzadWqlTIzM5WZmWmv1nz77bfKzs5WTExMuY4RHBzsUMWRzlRpTpw4oZkzZ9qPu2PHDocx0dHR+vjjjx3WffXVVxd7KfCw5CVXSJLG9W/usP6RORnq8bcz1ZQfD1j15ox6OpXtq7pRRRo46pj6Df/ZYXx6ag299XyECvJ91KBZoUbNylT3285OXFb/q7b+fGP2WckOUJWEXVGicXMzVCu8RKdP+epQmr8mDWqqrzcGX3hnwEtU2aSme/fuio2N1eDBg/Xiiy+qpKREDz74oLp06aL27dtf9HEbNmwoPz8/vfzyy3rggQe0Z88eTZs2zWHM/fffrxdeeEETJkzQsGHDlJqaqsTERElyuTIDz1tzJPWCY4ZNOqphk446HTN+bka5zvfiqn3lGgdUpjmPMG/mcsAThZ2rsldnsVj04YcfqmbNmurcubO6d++upk2bavny5W4dt06dOkpMTNS7776rmJgYzZw5U88995zDmCZNmui9997T+++/r7i4OM2fP99+9xOtIwBAZSlrP7mzeDOLweNvy2X69OlasGCBxyf25ubmKjQ0VL9831QhwVU2xwTckhDZtrJDACpMiVGs9fpQOTk5CgmpmHdtlf2u6PPpPaoe6HfRxynOL9KHPRZXaKyVqcq2nyrbvHnz1KFDB9WuXVtbtmzR7NmzNXLkyMoOCwBwGXP3/U3efks3Sc157Nu3T08//bROnjyphg0b6pFHHtGjjz5a2WEBAC5j3P3kHEnNecyZM0dz5syp7DAAAEA5kdQAAGASVGqcI6kBAMAkSGqc43YbAADgFajUAABgElRqnCOpAQDAJAy5d1u2tz+YjqQGAACToFLjHHNqAACAV6BSAwCASVCpcY6kBgAAkyCpcY72EwAA8ApUagAAMAkqNc6R1AAAYBKGYZHhRmLizr5mQPsJAAB4BSo1AACYhE0Wtx6+586+ZkBSAwCASTCnxjnaTwAAwCtQqQEAwCSYKOwclRoAAEyirP3kzuKKGTNmqEOHDgoODlZ4eLj69u2r9PR0hzEFBQUaMWKEateuraCgIPXv31/Hjh1zGJORkaFevXqpRo0aCg8P17hx41RSUuIwZv369brmmmtktVrVrFkzJSYmuvz1IakBAMAkyio17iyu2LBhg0aMGKEvvvhCKSkpKi4uVo8ePZSfn28fM3r0aK1atUrvvvuuNmzYoCNHjqhfv3727aWlperVq5eKioq0detWLVmyRImJiZo8ebJ9zKFDh9SrVy9169ZNqampevjhh3XvvfdqzZo1LsVrMQzD299EXqXl5uYqNDRUv3zfVCHB5JjwTgmRbSs7BKDClBjFWq8PlZOTo5CQkAo5R9nvinb/Hq1qgdaLPk5JfqF29p+jzMxMh1itVqus1gsf9+eff1Z4eLg2bNigzp07KycnR3Xq1NGyZct02223SZK+++47tWrVStu2bdO1116rTz75RDfffLOOHDmiunXrSpIWLFigCRMm6Oeff5afn58mTJigjz76SHv27LGfa8CAAcrOztbq1avLfX38FgUAwCQMN1tPZZWaqKgohYaG2pcZM2aU6/w5OTmSpFq1akmSdu7cqeLiYnXv3t0+pmXLlmrYsKG2bdsmSdq2bZtiY2PtCY0kJSQkKDc3V3v37rWP+d9jlI0pO0Z5MVEYAACTMCS5018p2/VclZoLsdlsevjhh/XnP/9ZrVu3liRlZWXJz89PYWFhDmPr1q2rrKws+5j/TWjKtpdtczYmNzdXv/76qwICAsp1fSQ1AABcZkJCQlxulY0YMUJ79uzR5s2bKygq99F+AgDAJMqeKOzOcjFGjhyp5ORkff7552rQoIF9fUREhIqKipSdne0w/tixY4qIiLCP+ePdUGWfLzQmJCSk3FUaiaQGAADTuNR3PxmGoZEjR+qDDz7QunXr1KRJE4ft7dq1U/Xq1bV27Vr7uvT0dGVkZCg+Pl6SFB8fr927d+v48eP2MSkpKQoJCVFMTIx9zP8eo2xM2THKi/YTAAA4pxEjRmjZsmX68MMPFRwcbJ8DExoaqoCAAIWGhmrYsGEaM2aMatWqpZCQED300EOKj4/XtddeK0nq0aOHYmJidOedd2rWrFnKysrS448/rhEjRtjn8jzwwAN65ZVXNH78eN1zzz1at26d3nnnHX300UcuxUtSAwCASdgMiyyX8N1P8+fPlyR17drVYf2bb76poUOHSpLmzJkjHx8f9e/fX4WFhUpISNC8efPsY319fZWcnKy///3vio+PV2BgoIYMGaKpU6faxzRp0kQfffSRRo8erZdeekkNGjTQokWLlJCQ4FK8PKemkvGcGlwOeE4NvNmlfE7NVcvHybfGxT+npvR0ofb+bXaFxlqZ+C0KAAC8Au0nAABMghdaOkdSAwCASZDUOEdSAwCASVzqicJmw5waAADgFajUAABgEobh5rufvPx+Z5IaAABM4kxS486cGg8GUwXRfgIAAF6BSg0AACbB3U/OkdQAAGASxm+LO/t7M9pPAADAK1CpAQDAJGg/OUdSAwCAWdB/coqkBgAAs3CzUiMvr9QwpwYAAHgFKjUAAJgETxR2jqQGAACTYKKwc7SfAACAV6BSAwCAWRgW9yb7enmlhqQGAACTYE6Nc7SfAACAV6BSAwCAWfDwPadIagAAMAnufnKuXEnNypUry33AW2655aKDAQAAuFjlSmr69u1broNZLBaVlpa6Ew8AAHDGy1tI7ihXUmOz2So6DgAAcAG0n5xz6+6ngoICT8UBAAAuxPDA4sVcTmpKS0s1bdo01a9fX0FBQTp48KAk6YknntAbb7zh8QABAADKw+WkZvr06UpMTNSsWbPk5+dnX9+6dWstWrTIo8EBAID/ZfHA4r1cTmqWLl2q119/XYMHD5avr699fZs2bfTdd995NDgAAPA/aD855XJS89NPP6lZs2ZnrbfZbCouLvZIUAAAAK5yOamJiYnRpk2bzlr/3nvv6eqrr/ZIUAAA4Byo1Djl8hOFJ0+erCFDhuinn36SzWbT+++/r/T0dC1dulTJyckVESMAAJB4S/cFuFyp6dOnj1atWqXPPvtMgYGBmjx5stLS0rRq1SrdcMMNFREjAADABV3Uu586deqklJQUT8cCAACcMIwzizv7e7OLfqHljh07lJaWJunMPJt27dp5LCgAAHAOvKXbKZeTmh9//FEDBw7Uli1bFBYWJknKzs7W//3f/+ntt99WgwYNPB0jAADABbk8p+bee+9VcXGx0tLSdPLkSZ08eVJpaWmy2Wy69957KyJGAAAg/T5R2J3Fi7lcqdmwYYO2bt2q6Oho+7ro6Gi9/PLL6tSpk0eDAwAAv7MYZxZ39vdmLic1UVFR53zIXmlpqSIjIz0SFAAAOAfm1Djlcvtp9uzZeuihh7Rjxw77uh07dugf//iHnnvuOY8GBwAAUF7lqtTUrFlTFsvvfbj8/Hx17NhR1aqd2b2kpETVqlXTPffco759+1ZIoAAAXPZ4+J5T5UpqXnzxxQoOAwAAXBDtJ6fKldQMGTKkouMAAABwy0U/fE+SCgoKVFRU5LAuJCTErYAAAMB5UKlxyuWJwvn5+Ro5cqTCw8MVGBiomjVrOiwAAKCC8JZup1xOasaPH69169Zp/vz5slqtWrRokZ566ilFRkZq6dKlFREjAADABbncflq1apWWLl2qrl276u6771anTp3UrFkzNWrUSElJSRo8eHBFxAkAALj7ySmXKzUnT55U06ZNJZ2ZP3Py5ElJ0nXXXaeNGzd6NjoAAGBX9kRhdxZv5nJS07RpUx06dEiS1LJlS73zzjuSzlRwyl5wCQAAcKm5nNTcfffd2rVrlyRp4sSJevXVV+Xv76/Ro0dr3LhxHg8QAAD85hJPFN64caN69+6tyMhIWSwWrVixwmH70KFDZbFYHJaePXs6jDl58qQGDx6skJAQhYWFadiwYcrLy3MY880336hTp07y9/dXVFSUZs2a5Vqgv3F5Ts3o0aPt/+7evbu+++477dy5U82aNVNcXNxFBQEAAKqe/Px8tWnTRvfcc4/69et3zjE9e/bUm2++af9stVodtg8ePFhHjx5VSkqKiouLdffdd2v48OFatmyZJCk3N1c9evRQ9+7dtWDBAu3evVv33HOPwsLCNHz4cJfides5NZLUqFEjNWrUyN3DAACAC7DIzbd0uzj+xhtv1I033uh0jNVqVURExDm3paWlafXq1frqq6/Uvn17SdLLL7+sm266Sc8995wiIyOVlJSkoqIiLV68WH5+frrqqquUmpqqF154oWKSmrlz55b7gKNGjXIpAAAAcGnl5uY6fLZarWdVWMpr/fr1Cg8PV82aNfWXv/xFTz/9tGrXri1J2rZtm8LCwuwJjXSmy+Pj46Pt27fr1ltv1bZt29S5c2f5+fnZxyQkJOjZZ5/VL7/84tIz8MqV1MyZM6dcB7NYLCQ1F+nWFrGqZqle2WEAFWLNkdTKDgGoMLmnbKrZ4hKdzEO3dEdFRTmsfvLJJzVlyhSXD9ezZ0/169dPTZo00YEDB/TYY4/pxhtv1LZt2+Tr66usrCyFh4c77FOtWjXVqlVLWVlZkqSsrCw1adLEYUzdunXt2zye1JTd7QQAACqRh16TkJmZ6fBao4ut0gwYMMD+79jYWMXFxenKK6/U+vXrdf3117sR6MVx+e4nAABgbiEhIQ7LxSY1f9S0aVNdccUV2r9/vyQpIiJCx48fdxhTUlKikydP2ufhRERE6NixYw5jyj6fb67O+ZDUAABgFlX83U8//vijTpw4oXr16kmS4uPjlZ2drZ07d9rHrFu3TjabTR07drSP2bhxo4qLi+1jUlJSFB0d7fI7JUlqAAAwiUv9ROG8vDylpqYqNTVV0pnpKKmpqcrIyFBeXp7GjRunL774QocPH9batWvVp08fNWvWTAkJCZKkVq1aqWfPnrrvvvv05ZdfasuWLRo5cqQGDBigyMhISdKgQYPk5+enYcOGae/evVq+fLleeukljRkzxuWvD0kNAAA4px07dujqq6/W1VdfLUkaM2aMrr76ak2ePFm+vr765ptvdMstt6hFixYaNmyY2rVrp02bNjm0s5KSktSyZUtdf/31uummm3Tdddfp9ddft28PDQ3Vp59+qkOHDqldu3Z65JFHNHnyZJdv55Y88JwaAABwiXhoonB5de3aVYZx/p3WrFlzwWPUqlXL/qC984mLi9OmTZtcC+4cLqpSs2nTJt1xxx2Kj4/XTz/9JEl66623tHnzZrcDAgAA51HF59RUNpeTmn//+99KSEhQQECA/vOf/6iwsFCSlJOTo2eeecbjAQIAAJSHy0nN008/rQULFmjhwoWqXv33h8X9+c9/1tdff+3R4AAAwO8u9URhs3F5Tk16ero6d+581vrQ0FBlZ2d7IiYAAHAuHnqisLdyuVITERFhf6jO/9q8ebOaNm3qkaAAAMA5MKfGKZeTmvvuu0//+Mc/tH37dlksFh05ckRJSUkaO3as/v73v1dEjAAAABfkcvtp4sSJstlsuv7663X69Gl17txZVqtVY8eO1UMPPVQRMQIAALk/L4Y5NX9gsVg0adIkjRs3Tvv371deXp5iYmIUFBRUEfEBAIAyl/g5NWZz0Q/f8/PzU0xMjCdjAQAAuGguJzXdunWTxXL+2dPr1q1zKyAAAHAe7t6WTaXGUdu2bR0+FxcXKzU1VXv27NGQIUM8FRcAAPgj2k9OuZzUzJkz55zrp0yZory8PLcDAgAAuBgee0v3HXfcocWLF3vqcAAA4I94To1THntL97Zt2+Tv7++pwwEAgD/glm7nXE5q+vXr5/DZMAwdPXpUO3bs0BNPPOGxwAAAAFzhclITGhrq8NnHx0fR0dGaOnWqevTo4bHAAAAAXOFSUlNaWqq7775bsbGxqlmzZkXFBAAAzoW7n5xyaaKwr6+vevTowdu4AQCoBGVzatxZvJnLdz+1bt1aBw8erIhYAAAALprLSc3TTz+tsWPHKjk5WUePHlVubq7DAgAAKhC3c59XuefUTJ06VY888ohuuukmSdItt9zi8LoEwzBksVhUWlrq+SgBAABzai6g3EnNU089pQceeECff/55RcYDAABwUcqd1BjGmfSuS5cuFRYMAAA4Px6+55xLt3Q7ezs3AACoYLSfnHIpqWnRosUFE5uTJ0+6FRAAAMDFcCmpeeqpp856ojAAALg0aD8551JSM2DAAIWHh1dULAAAwBnaT06V+zk1zKcBAABVmct3PwEAgEpCpcapcic1NputIuMAAAAXwJwa51yaUwMAACoRlRqnXH73EwAAQFVEpQYAALOgUuMUSQ0AACbBnBrnaD8BAACvQKUGAACzoP3kFEkNAAAmQfvJOdpPAADAK1CpAQDALGg/OUVSAwCAWZDUOEX7CQAAeAUqNQAAmITlt8Wd/b0ZSQ0AAGZB+8kpkhoAAEyCW7qdY04NAADwClRqAAAwC9pPTpHUAABgJl6emLiD9hMAAPAKVGoAADAJJgo7R1IDAIBZMKfGKdpPAADAK5DUAABgEmXtJ3cWV2zcuFG9e/dWZGSkLBaLVqxY4bDdMAxNnjxZ9erVU0BAgLp37659+/Y5jDl58qQGDx6skJAQhYWFadiwYcrLy3MY880336hTp07y9/dXVFSUZs2adTFfHpIaAABMw/DA4oL8/Hy1adNGr7766jm3z5o1S3PnztWCBQu0fft2BQYGKiEhQQUFBfYxgwcP1t69e5WSkqLk5GRt3LhRw4cPt2/Pzc1Vjx491KhRI+3cuVOzZ8/WlClT9Prrr7sWrJhTAwAAzuPGG2/UjTfeeM5thmHoxRdf1OOPP64+ffpIkpYuXaq6detqxYoVGjBggNLS0rR69Wp99dVXat++vSTp5Zdf1k033aTnnntOkZGRSkpKUlFRkRYvXiw/Pz9dddVVSk1N1QsvvOCQ/JQHlRoAAEzCU+2n3Nxch6WwsNDlWA4dOqSsrCx1797dvi40NFQdO3bUtm3bJEnbtm1TWFiYPaGRpO7du8vHx0fbt2+3j+ncubP8/PzsYxISEpSenq5ffvnFpZhIagAAMAsPtZ+ioqIUGhpqX2bMmOFyKFlZWZKkunXrOqyvW7eufVtWVpbCw8MdtlerVk21atVyGHOuY/zvOcqL9hMAAGbhoVu6MzMzFRISYl9ttVrdCquqoFIDAMBlJiQkxGG5mKQmIiJCknTs2DGH9ceOHbNvi4iI0PHjxx22l5SU6OTJkw5jznWM/z1HeZHUAABgEpf6lm5nmjRpooiICK1du9a+Ljc3V9u3b1d8fLwkKT4+XtnZ2dq5c6d9zLp162Sz2dSxY0f7mI0bN6q4uNg+JiUlRdHR0apZs6ZLMZHUAABgFpf4lu68vDylpqYqNTVV0pnJwampqcrIyJDFYtHDDz+sp59+WitXrtTu3bt11113KTIyUn379pUktWrVSj179tR9992nL7/8Ulu2bNHIkSM1YMAARUZGSpIGDRokPz8/DRs2THv37tXy5cv10ksvacyYMS5/eZhTAwAAzmnHjh3q1q2b/XNZojFkyBAlJiZq/Pjxys/P1/Dhw5Wdna3rrrtOq1evlr+/v32fpKQkjRw5Utdff718fHzUv39/zZ071749NDRUn376qUaMGKF27drpiiuu0OTJk12+nVuSLIZhePmbIKq23NxchYaGqqv6qJqlemWHA1SINUdSKzsEoMLknrKpZouDysnJcZh869Fz/Pa7ou2d0+Xr53/hHc6jtKhAqW9NqtBYKxOVGgAAzIIXWjrFnBoAAOAVqNQAAGAS7t7B5Mm7n6oikhoAAMyC9pNTtJ8AAIBXoFIDAIBJ0H5yjqQGAACzoP3kFEkNAAAmQaXGOebUAAAAr0ClBgAAs6D95BRJDQAAJuLtLSR30H4CAABegUoNAABmYRhnFnf292IkNQAAmAR3PzlH+wkAAHgFKjUAAJgFdz85RVIDAIBJWGxnFnf292a0nwAAgFegUoPLws13/Ve97jqhulFFkqQf0v2VNKeudnweUsmRAWd7++Vwbfk4TJn7rfLztymm/WkNm3REUc0K7WOOHPbTwqmR2vtlkIqLLGrXLVcjnv5JNeuU2Mfs+yZAb0yP1Pe7asjH19B1N2Xr/ilHFBB45s/1T5fX0vOjG54zhuXf7FHYFSXn3IZKRPvJKSo1HjZlyhS1bdu2ssPAH/x8tLoWP1NPI3u20EM3ttCuLUGa8uZhNWpRUNmhAWf5ZluQeg/9r15M3qcZbx9QaYn02MArVXD6zI/sgtM+emzglbJYpGff3a8XPtynkiIfTR7SRLbf2gsnsqpp4oArFdmkUC8lf6/pSQf0Q7q/nnv49ySmyy2/6F+pexyWdl1zFRefR0JTRZXd/eTO4s2o1HjY2LFj9dBDD1V2GPiD7SmhDp8Tn62nm+86oZbt8vXD9/6VFBVwbs8sO+jw+ZEXM/S32Fjt+yZAsdfma++XgTqW6adXP01XYPCZLGbcSz+of6tYpW4O0jWd87T9s1BVq2Zo5DM/yue3P19HPfujHri+pX465Kf6TYpkDTBkDfg9eck+4atdW4I0+vnMS3atcBHPqXGKSo2HGIahkpISBQUFqXbt2pUdDpzw8THUpc8vstawKW1HYGWHA1xQfq6vJCk4rFSSVFxkkSxSdb/ff0FVtxqy+Eh7vww6M6bQomrVDXtCI0l+/mcSoLIxf/TZu7VkDTDUqVd2BVwFUPEu26Rm9erVuu666xQWFqbatWvr5ptv1oEDB+zbt27dqrZt28rf31/t27fXihUrZLFYlJqaKklav369LBaLPvnkE7Vr105Wq1WbN2++YPupsLBQubm5DgsujcYtf9WKfbuVfPgbjZr5o6YOa6yMfVRpULXZbNKCJ+vrqg55atzyTLu0Zbt8+dew6Y3pkSo4bVHBaR8tnBopW6lFJ4+fKcC3uS5Pv/xcXe/Oq6PiIotOZftq8TORkmQf80dr/lVb3W79RdYA7/5r3sxoPzl32SY1+fn5GjNmjHbs2KG1a9fKx8dHt956q2w2m3Jzc9W7d2/Fxsbq66+/1rRp0zRhwoRzHmfixImaOXOm0tLSFBcXd8HzzpgxQ6GhofYlKirK05eG8/jxgFUP3tBCo3o1V/LSKzT2pQw1bM6cGlRtrzzWQD98F6BH5/9gXxdWu1SPv3ZY21NC1Ld5nG6NjlV+rq+axZ6W5bef6o2jCzT2xR/079fCdcuVcRrY9ipFRBWpZp1iWSxnn+fbHTWUsc9fPQeeuERXhotieGDxYpftnJr+/fs7fF68eLHq1Kmjb7/9Vps3b5bFYtHChQvl7++vmJgY/fTTT7rvvvvOOs7UqVN1ww03lPu8jz76qMaMGWP/nJubS2JziZQU++jIYaskaf/uGopue1p97/1Zcyfw9UfV9Mpj9bU9JUTPf7BfdSKLHba163pKidvSlHPCV77VpKDQUg1oc5XqNfz9Dqm/9MvWX/pl65efq8m/hk0Wi/T+63VUr1HhH0+l1ctq68qrTqt53K8Vfl1ARblsk5p9+/Zp8uTJ2r59u/773//K9tstAxkZGUpPT1dcXJz8/X9vTfzpT38653Hat2/v0nmtVqusVuvFBw6PsfxhTgJQVRiG9Oqk+tq6OlSz39uviIZF5x0bWvvMPJvUzUHK/m81Xdvj7JZ22W3ea/5VS9WtNl3TOc9h+6/5Ptq4Kkx3P3rUg1eBisC7n5y7bJOa3r17q1GjRlq4cKEiIyNls9nUunVrFRWd/4fHuQQGMtHUDO5+9Ki+Whesn3/yU0BQqbrdmq24/8vTpEFNKzs04CyvPNZAn39QU1PePKiAIJt9DkxgcKl9vsuat2upYfMChdYuUdrOQM2fXF+3Dv/Z4Vk2Hy6+QjHt8xUQaNPXG4O1aFqk7nnsiIJCSx3Ot+HDMJWWWnR9/18u3UXi4nD3k1OXZVJz4sQJpaena+HCherUqZMkafPmzfbt0dHR+uc//6nCwkJ7VeWrr76qlFjhGWFXlGjc3AzVCi/R6VO+OpTmr0mDmurrjcGVHRpwluQlV0iSxvVv7rD+kTkZ6vG3k5LOzBF7c0Y9ncr2Vd2oIg0cdUz9hv/sMD49tYbeej5CBfk+atCsUKNmZar7bWcnLqv/VVt/vjH7rGQHMJvLMqmpWbOmateurddff1316tVTRkaGJk6caN8+aNAgTZo0ScOHD9fEiROVkZGh5557TpJkOdcMO1R5cx5h3gzMY82R1AuOGTbpqIZNct4uGj83o1zne3HVvnKNQ+Wj/eTcZXn3k4+Pj95++23t3LlTrVu31ujRozV79mz79pCQEK1atUqpqalq27atJk2apMmTJ0uSwzwbAAAuKe5+cspiGF7eYPOQpKQk3X333crJyVFAQIDHjpubm6vQ0FB1VR9Vs1T32HGBqqQ8lQfArHJP2VSzxUHl5OQoJKRi3idX9rsivudUVat+8X9clxQXaNvqyRUaa2W6LNtP5bF06VI1bdpU9evX165duzRhwgTdfvvtHk1oAABwBe0n50hqziMrK0uTJ09WVlaW6tWrp7/+9a+aPn16ZYcFALic2Ywzizv7ezGSmvMYP368xo8fX9lhAADwO3fnxXh3TnN5ThQGAADeh0oNAAAmYZGbc2o8FknVRFIDAIBZ8ERhp2g/AQAAr0ClBgAAk+CWbudIagAAMAvufnKK9hMAAPAKVGoAADAJi2HI4sZkX3f2NQOSGgAAzML22+LO/l6M9hMAAPAKVGoAADAJ2k/OkdQAAGAW3P3kFEkNAABmwROFnWJODQAA8ApUagAAMAmeKOwcSQ0AAGZB+8kp2k8AAMArkNQAAGASFpv7iyumTJkii8XisLRs2dK+vaCgQCNGjFDt2rUVFBSk/v3769ixYw7HyMjIUK9evVSjRg2Fh4dr3LhxKikp8cSX4yy0nwAAMItKaD9dddVV+uyzz+yfq1X7PXUYPXq0PvroI7377rsKDQ3VyJEj1a9fP23ZskWSVFpaql69eikiIkJbt27V0aNHddddd6l69ep65plnLv46zoOkBgCAy0xubq7DZ6vVKqvVes6x1apVU0RExFnrc3Jy9MYbb2jZsmX6y1/+Ikl688031apVK33xxRe69tpr9emnn+rbb7/VZ599prp166pt27aaNm2aJkyYoClTpsjPz8+j10X7CQAAszA8sEiKiopSaGiofZkxY8Z5T7lv3z5FRkaqadOmGjx4sDIyMiRJO3fuVHFxsbp3724f27JlSzVs2FDbtm2TJG3btk2xsbGqW7eufUxCQoJyc3O1d+9eD3xBHFGpAQDAJDz1moTMzEyFhITY15+vStOxY0clJiYqOjpaR48e1VNPPaVOnTppz549ysrKkp+fn8LCwhz2qVu3rrKysiRJWVlZDglN2faybZ5GUgMAwGUmJCTEIak5nxtvvNH+77i4OHXs2FGNGjXSO++8o4CAgIoM8aLQfgIAwCzKJgq7s7ghLCxMLVq00P79+xUREaGioiJlZ2c7jDl27Jh9Dk5ERMRZd0OVfT7XPB13kdQAAGAWhiSbG4ubz97Ly8vTgQMHVK9ePbVr107Vq1fX2rVr7dvT09OVkZGh+Ph4SVJ8fLx2796t48eP28ekpKQoJCREMTEx7gVzDrSfAAAwCU/NqSmvsWPHqnfv3mrUqJGOHDmiJ598Ur6+vho4cKBCQ0M1bNgwjRkzRrVq1VJISIgeeughxcfH69prr5Uk9ejRQzExMbrzzjs1a9YsZWVl6fHHH9eIESPOO4/HHSQ1AADgnH788UcNHDhQJ06cUJ06dXTdddfpiy++UJ06dSRJc+bMkY+Pj/r376/CwkIlJCRo3rx59v19fX2VnJysv//974qPj1dgYKCGDBmiqVOnVki8JDUAAJiFITcfvufa8Lffftvpdn9/f7366qt69dVXzzumUaNG+vjjj1078UUiqQEAwCx4oaVTTBQGAABegUoNAABmYZNkcXN/L0ZSAwCASVzqu5/MhvYTAADwClRqAAAwCyYKO0VSAwCAWZDUOEX7CQAAeAUqNQAAmAWVGqdIagAAMAtu6XaKpAYAAJPglm7nmFMDAAC8ApUaAADMgjk1TpHUAABgFjZDsriRmNi8O6mh/QQAALwClRoAAMyC9pNTJDUAAJiGm0mNvDupof0EAAC8ApUaAADMgvaTUyQ1AACYhc2QWy0k7n4CAACo+qjUAABgFobtzOLO/l6MpAYAALNgTo1TJDUAAJgFc2qcYk4NAADwClRqAAAwC9pPTpHUAABgFobcTGo8FkmVRPsJAAB4BSo1AACYBe0np0hqAAAwC5tNkhvPmrF593NqaD8BAACvQKUGAACzoP3kFEkNAABmQVLjFO0nAADgFajUAABgFrwmwSmSGgAATMIwbDLceNO2O/uaAUkNAABmYRjuVVuYUwMAAFD1UakBAMAsDDfn1Hh5pYakBgAAs7DZJIsb82K8fE4N7ScAAOAVqNQAAGAWtJ+cIqkBAMAkDJtNhhvtJ2+/pZv2EwAA8ApUagAAMAvaT06R1AAAYBY2Q7KQ1JwP7ScAAOAVqNQAAGAWhiHJnefUeHelhqQGAACTMGyGDDfaTwZJDQAAqBIMm9yr1HBLNwAAQJVHpQYAAJOg/eQcSQ0AAGZB+8kpkppKVpY1l6jYrecpAVVZ7inv/kGKy1tu3pnv70tRBXH3d0WJij0XTBVEUlPJTp06JUnarI8rORKg4tRsUdkRABXv1KlTCg0NrZBj+/n5KSIiQpuz3P9dERERIT8/Pw9EVfVYDG9vsFVxNptNR44cUXBwsCwWS2WHc1nIzc1VVFSUMjMzFRISUtnhAB7F9/elZxiGTp06pcjISPn4VNz9NwUFBSoqKnL7OH5+fvL39/dARFUPlZpK5uPjowYNGlR2GJelkJAQfujDa/H9fWlVVIXmf/n7+3ttMuIp3NINAAC8AkkNAADwCiQ1uOxYrVY9+eSTslqtlR0K4HF8f+NyxkRhAADgFajUAAAAr0BSAwAAvAJJDQAA8AokNUAFGTp0qPr27VvZYQBOTZkyRW3btq3sMACPYKIwUEFycnJkGIbCwsIqOxTgvPLy8lRYWKjatWtXdiiA20hqAA8rLS2VxWKp0MelA+4yDEOlpaWqVo0Hy8N78FMXVULXrl01atQojR8/XrVq1VJERISmTJli356RkaE+ffooKChIISEhuv3223Xs2DH79rIS+ltvvaXGjRsrNDRUAwYMsL8w9HzeeusttW/fXsHBwYqIiNCgQYN0/PhxhzErV65U8+bN5e/vr27dumnJkiWyWCzKzs6WJCUmJiosLEwrV65UTEyMrFarMjIyaD/Bo1avXq3rrrtOYWFhql27tm6++WYdOHDAvn3r1q1q27at/P391b59e61YsUIWi0WpqamSpPXr18tiseiTTz5Ru3btZLVatXnzZtpP8CokNagylixZosDAQG3fvl2zZs3S1KlTlZKSIpvNpj59+ujkyZPasGGDUlJSdPDgQf3tb39z2P/AgQNasWKFkpOTlZycrA0bNmjmzJlOz1lcXKxp06Zp165dWrFihQ4fPqyhQ4fatx86dEi33Xab+vbtq127dun+++/XpEmTzjrO6dOn9eyzz2rRokXau3evwsPDPfI1Acrk5+drzJgx2rFjh9auXSsfHx/deuutstlsys3NVe/evRUbG6uvv/5a06ZN04QJE855nIkTJ2rmzJlKS0tTXFzcJb4KoGJRd0SVERcXpyeffFKS1Lx5c73yyitau3atJGn37t06dOiQoqKiJElLly7VVVddpa+++kodOnSQdOaN54mJiQoODpYk3XnnnVq7dq2mT59+3nPec8899n83bdpUc+fOVYcOHZSXl6egoCC99tprio6O1uzZsyVJ0dHR2rNnz1nHLC4u1rx589SmTRsPfTUAR/3793f4vHjxYtWpU0fffvutNm/eLIvFooULF8rf318xMTH66aefdN999511nKlTp+qGG264VGEDlxSVGlQZf/yrsV69ejp+/LjS0tIUFRVlT2gkKSYmRmFhYUpLS7Ova9y4sT2h+d/9JSkpKUlBQUH2ZdOmTZKknTt3qnfv3mrYsKGCg4PVpUsXSWfaXZKUnp5uT5rK/OlPfzordj8/P/7qRYXat2+fBg4cqKZNmyokJESNGzeWdOZ7NT09XXFxcQ5vcD7X96kktW/f/lKEC1QKKjWoMqpXr+7w2WKxyGazeWT/W265RR07drRvq1+/vvLz85WQkKCEhAQlJSWpTp06ysjIUEJCgoqKilyKPSAgQBaLxaV9AFf07t1bjRo10sKFCxUZGSmbzabWrVu7/L0aGBhYQREClY+kBlVeq1atlJmZqczMTHu15ttvv1V2drZiYmLKdYzg4GCHKo50pkpz4sQJzZw5037cHTt2OIyJjo7Wxx9/7LDuq6++uthLAS7KiRMnlJ6eroULF6pTp06SpM2bN9u3R0dH65///KcKCwvtL7Lk+xSXI9pPqPK6d++u2NhYDR48WF9//bW+/PJL3XXXXerSpYtbpfSGDRvKz89PL7/8sg4ePKiVK1dq2rRpDmPuv/9+fffdd5owYYK+//57vfPOO0pMTJQkKjO4ZGrWrKnatWvr9ddf1/79+7Vu3TqNGTPGvn3QoEGy2WwaPny40tLStGbNGj333HOS+D7F5YWkBlWexWLRhx9+qJo1a6pz587q3r27mjZtquXLl7t13Dp16igxMVHvvvuuYmJiNHPmTPsvgjJNmjTRe++9p/fff19xcXGaP3++/e6nsr+IgYrm4+Ojt99+Wzt37lTr1q01evRo++R1SQoJCdGqVauUmpqqtm3batKkSZo8ebIkOcyzAbwdD98DXDR9+nQtWLBAmZmZlR0KcF5JSUm6++67lZOTo4CAgMoOB7gkmFMDXMC8efPUoUMH1a5dW1u2bNHs2bM1cuTIyg4LcLB06VI1bdpU9evX165duzRhwgTdfvvtJDS4rJDUABewb98+Pf300zp58qQaNmyoRx55RI8++mhlhwU4yMrK0uTJk5WVlaV69erpr3/9q9NnNAHeiPYTAADwCkwUBgAAXoGkBgAAeAWSGgAA4BVIagAAgFcgqQEAAF6BpAaAhg4dqr59+9o/d+3aVQ8//PAlj2P9+vWyWCzKzs4+7xiLxaIVK1aU+5hTpkxR27Zt3Yrr8OHDslgsSk1Ndes4ACoWSQ1QRQ0dOlQWi0UWi0V+fn5q1qyZpk6dqpKSkgo/9/vvv3/We7DOpzyJCABcCjx8D6jCevbsqTfffFOFhYX6+OOPNWLECFWvXv2cD/8rKiqSn5+fR85bq1YtjxwHAC4lKjVAFWa1WhUREaFGjRrp73//u7p3766VK1dK+r1lNH36dEVGRio6OlqSlJmZqdtvv11hYWGqVauW+vTpo8OHD9uPWVpaqjFjxigsLEy1a9fW+PHj9cdncP6x/VRYWKgJEyYoKipKVqtVzZo10xtvvKHDhw+rW7duks68SdpisWjo0KGSJJvNphkzZqhJkyYKCAhQmzZt9N577zmc5+OPP1aLFi0UEBCgbt26OcRZXhMmTFCLFi1Uo0YNNW3aVE888YSKi4vPGvfaa68pKipKNWrU0O23366cnByH7YsWLVKrVq3k7++vli1bat68eS7HAqBykdQAJhIQEKCioiL757Vr1yo9PV0pKSlKTk5WcXGxEhISFBwcrE2bNmnLli0KCgpSz5497fs9//zzSkxM1OLFi7V582adPHlSH3zwgdPz3nXXXfrXv/6luXPnKi0tTa+99pqCgoIUFRWlf//735Kk9PR0HT16VC+99JIkacaMGVq6dKkWLFigvXv3avTo0brjjju0YcMGSWeSr379+ql3795KTU3Vvffeq4kTJ7r8NQkODlZiYqK+/fZbvfTSS1q4cKHmzJnjMGb//v165513tGrVKq1evVr/+c9/9OCDD9q3JyUlafLkyZo+fbrS0tL0zDPP6IknntCSJUtcjgdAJTIAVElDhgwx+vTpYxiGYdhsNiMlJcWwWq3G2LFj7dvr1q1rFBYW2vd56623jOjoaMNms9nXFRYWGgEBAcaaNWsMwzCMevXqGbNmzbJvLy4uNho0aGA/l2EYRpcuXYx//OMfhmEYRnp6uiHJSElJOWecn3/+uSHJ+OWXX+zrCgoKjBo1ahhbt251GDts2DBj4MCBhmEYxqOPPmrExMQ4bJ8wYcJZx/ojScYHH3xw3u2zZ8822rVrZ//85JNPGr6+vsaPP/5oX/fJJ58YPj4+xtGjRw3DMIwrr7zSWLZsmcNxpk2bZsTHxxuGYRiHDh0yJBn/+c9/znteAJWPOTVAFZacnKygoCAVFxfLZrNp0KBBmjJlin17bGyswzyaXbt2af/+/QoODnY4TkFBgQ4cOKCcnBwdPXpUHTt2tG+rVq2a2rdvf1YLqkxqaqp8fX3VpUuXcse9f/9+nT59WjfccIPD+qKiIl199dWSpLS0NIc4JCk+Pr7c5yizfPlyzZ07VwcOHFBeXp5KSkoUEhLiMKZhw4aqX7++w3lsNpvS09MVHBysAwcOaNiwYbrvvvvsY0pKShQaGupyPAAqD0kNUIV169ZN8+fPl5+fnyIjI1WtmuN/2cDAQIfPeXl5ateunZKSks46Vp06dS4qhoCAAJf3ycvLkyR99NFHDsmEdGaekKds27ZNgwcP1lNPPaWEhASFhobq7bff1vPPP+9yrAsXLjwryfL19fVYrAAqHkkNUIUFBgaqWbNm5R5/zTXXaPny5QoPDz+rWlGmXr162r59uzp37izpTEVi586duuaaa845PjY2VjabTRs2bFD37t3P2l5WKSotLbWvi4mJkdVqVUZGxnkrPK1atbJPei7zxRdfXPgi/8fWrVvVqFEjTZo0yb7uhx9+OGtcRkaGjhw5osjISPt5fHx8FB0drbp16yoyMlIHDx7U4MGDXTo/gKqFicKAFxk8eLCuuOIK9enTR5s2bdKhQ4e0fv16jRo1Sj/++KMk6R//+IdmzpypFStW6LvvvtODDz7o9BkzjRs31pAhQ3TPPfdoxYoV9mO+8847kqRGjRrJYrEoOTlZP//8s/Ly8hQcHKyxY8dq9OjRWrJkiQ4cOKCvv/5aL7/8sn3y7QMPPKB9+/Zp3LhxSk9P17Jly5SYmOjS9TZv3lwZGRl6++23deDAAc2dO/eck579/f01ZMgQ7dq1S5s2bdKoUaN0++23KyIiQpL01FNPacaMGZo7d66+//577d69W2+++aZeeOEFl+IBULlIagAvUqNGDW3cuFENGzZUv3791KpVKw0bNkwFBQX2ys0jjzyiO++8U0OGDFF8fLyCg4N16623Oj3u/Pnzddttt+nBBx9Uy5Ytdd999yk/P1+SVL9+fT311FOaOHGi6tatq5EjR0qSpk2bpieeeEIzZsxQq1at1LNnT3300Udq0qSJpDPzXP79739rxYoVatOmjRYsWKBnnnnGpeu95ZZbNHr0aI0cOVJt27bV1q1b9cQTT5w1rlmzZurXr59uuukm9ejRQ3FxcQ63bN97771atGiR3nzzTcXGxqpLly5KTEy0xwrAHCzG+WYHAgAAmAiVGgAA4BVIagAAgFcgqQEAAF6BpAYAAHgFkhoAAOAVSGoAAIBXIKkBAABegaQGAAB4BZIaAADgFUhqAACAVyCpAQAAXuH/ATLtqIBqHbGlAAAAAElFTkSuQmCC",
      "text/plain": [
       "<Figure size 640x480 with 2 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "## Please use the space below to write your answer\n",
    "print_metrics(y_true = all_labels_pytorch,\n",
    "              y_pred = all_preds_pytorch,\n",
    "              y_prob = np.array(all_probs_pytorch),\n",
    "              class_labels = agri_class_labels,\n",
    "              model_name = \"PyTorch CNN-Vit Hybrid Model\"\n",
    "             )"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Double-click **here** for the solution.\n",
    "<!--\n",
    "print_metrics(y_true = all_labels_pytorch,\n",
    "              y_pred = all_preds_pytorch,\n",
    "              y_prob = np.array(all_probs_pytorch),\n",
    "              class_labels = agri_class_labels,\n",
    "              model_name = \"PyTorch CNN-Vit Hybrid Model\"\n",
    "             )\n",
    "-->\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## ROC curve plotting\n",
    "\n",
    "First, define a function to plot ROC curves for binary or multi-class classification using scikit-learn's `roc_curve` and `roc_auc_score`. It handles both single-class and multi-class cases by binarizing labels if needed.\n",
    "\n",
    "Next, plot the ROC curves for both the models.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "metadata": {},
   "outputs": [],
   "source": [
    "\n",
    "def plot_roc(y_true, y_prob, model_name):\n",
    "    n_classes = y_prob.shape[1] if y_prob.ndim > 1 else 1\n",
    "    if n_classes == 1:\n",
    "        fpr, tpr, _ = roc_curve(y_true, y_prob)\n",
    "        auc = roc_auc_score(y_true, y_prob)\n",
    "        plt.plot(fpr, tpr, label=f'{model_name} (AUC = {auc:.4f})')\n",
    "    else:\n",
    "        y_true_bin = label_binarize(y_true, classes=np.arange(n_classes))\n",
    "        for i in range(n_classes):\n",
    "            fpr, tpr, _ = roc_curve(y_true_bin[:, i], y_prob[:, i])\n",
    "            auc = roc_auc_score(y_true_bin[:, i], y_prob[:, i])\n",
    "            plt.plot(fpr, tpr, label=f'{model_name} class {i} (AUC = {auc:.4f})')\n",
    "    plt.xlabel('False Positive Rate')\n",
    "    plt.ylabel('True Positive Rate')\n",
    "    plt.title('ROC Curve')\n",
    "    plt.legend()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### ROC curve plotting for both models\n",
    "\n",
    "Plot the ROC curves for both Keras and PyTorch models on the same figure for visual performance comparison.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "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4evrq9Xm5+eHTz/9tNQxBQUFKCgo0LzPycmprPKgVgt8sPE09idlVto+iIiIqrsODW2wY2xng+2/RoWbjIwMODg4aLU5ODggJycHT548gbm5ebExYWFhmDNnTpXUF7juJI5cydJqU5jwmm0iInqxmBob9mdfjQo3FTF16lQEBwdr3ufk5MDFxaVS9vX7tfuaX3/SrSkm9mgOmUxWKfsiIiKiktWocOPo6IjMTO1TPpmZmbCysirxqA0AKBQKKBSKqigPyiI1AGDFkPbo2865SvZJRERE2mrUORNvb2/ExsZqte3fvx/e3t4Gquh/8gtVml+7N7AxXCFEREQvOIOGm8ePHyMxMRGJiYkA/r7VOzExETdu3ADw9yml4cOHa/p/+OGHSE1NxRdffIFLly5h5cqV2LJlCyZOnGiI8rX8M9w425R8FImIiIgqn0HDzR9//IH27dujffv2AIDg4GC0b98es2bNAgCkp6drgg4AuLm5Yc+ePdi/fz/c3d2xePFirF27ttrdBk5ERESGY9Brbl577TUIIUr9vKTVh1977TWcOXOmEqsiIiKimqxGXXNDRERE9CwMN0RERCQpDDdEREQkKQw3REREJCkMN0RERCQpDDd6UsZNX0RERFSFGG4qAZ8mRUREZDgMN0RERCQpDDdEREQkKQw3REREJCkMN0RERCQpDDdEREQkKQw3REREJCkMN3rCZW6IiIiqB4abSiDjQjdEREQGw3BDREREksJwQ0RERJLCcENERESSwnBDREREksJwQ0RERJLCcENERESSwnBDREREksJwoydCcBk/IiKi6oDhphLIuIofERGRwTDcEBERkaQw3BAREZGkMNwQERGRpDDcEBERkaQw3BAREZGkMNwQERGRpDDc6AlXuSEiIqoeGG6IiIhIUhhuiIiISFIYboiIiEhSGG6IiIhIUhhuiIiISFIYboiIiEhSGG6IiIhIUhhuiIiISFIYbvREcBU/IiKiaoHhRs9kMkNXQERE9GJjuCEiIiJJYbghIiIiSWG4ISIiIklhuCEiIiJJYbghIiIiSWG4ISIiIklhuNETAS50Q0REVB0w3OgZl7khIiIyLIYbIiIikhSGGyIiIpIUhhsiIiKSFIYbIiIikhSGGyIiIpIUhhsiIiKSFIYbIiIikhSDh5vw8HC4urrCzMwMnTp1wsmTJ8vsv3TpUrRo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zJkzqF+/vl6KqokEXqjlgoiIiKotncPNoEGDMHnyZGRkZEAmk0GtVuPYsWOYNGkShg8fXhk11igyGVe6ISIiMiSdw01oaChatmwJFxcXPH78GK1bt8arr74KHx8fzJgxozJqJCIiIio3nZ8tJZfLsWbNGsycORMXLlzA48eP0b59ezRr1qwy6iMiIiLSic7h5ujRo3jllVfQsGFDNGzYsDJqIiIiIqownU9LdevWDW5ubpg2bRqSkpIqoyYiIiKiCtM53Ny5cwefffYZDh06hDZt2sDDwwMLFy7ErVu3KqM+IiIiIp3oHG7s7Owwfvx4HDt2DCkpKXj33Xfx448/wtXVFd26dauMGomIiIjK7bkenOnm5oYpU6ZgwYIFaNu2LQ4dOqSvuoiIiIgqpMLh5tixYxg7diycnJwwZMgQtGnTBnv27NFnbTWK4Bp+RERE1YLOd0tNnToVUVFRuHPnDnr06IFly5ahf//+sLCwqIz6ahwu4UdERGRYOoebw4cP4/PPP8fAgQNhZ2dXGTURERERVZjO4ebYsWOVUQcRERGRXpQr3OzevRu9e/eGqakpdu/eXWbfN998Uy+FEREREVVEucKNv78/MjIyYG9vD39//1L7yWQyqFQqfdVGREREpLNyhRu1Wl3ir4mIiIiqG51vBV+/fj0KCgqKtSuVSqxfv14vRRERERFVlM7hJigoCNnZ2cXaHz16hKCgIL0URURERFRROocbIQRksuKrudy6dQvW1tZ6Kaom4hp+RERE1UO5bwVv3749ZDIZZDIZunfvDhOT/w1VqVS4du0aevXqVSlF1ihcxY+IiMigyh1unt4llZiYCD8/P9SuXVvzmVwuh6urK95++229F0hERESki3KHm5CQEACAq6srAgICYGZmVmlFEREREVWUzisUBwYGVkYdRERERHpRrnBja2uLy5cvw87ODnXq1CnxguKn7t+/r7fiiIiIiHRVrnDzzTffwNLSUvPrssINERERkSGVK9z881TUiBEjKqsWIiIiouem8zo3CQkJOH/+vOb9zz//DH9/f0ybNg1KpVKvxdUkQnClGyIioupA53DzwQcf4PLlywCA1NRUBAQEwMLCAlu3bsUXX3yh9wJrGp6wIyIiMiydw83ly5fh4eEBANi6dSu6du2KzZs3IzIyEtu3b9d3fUREREQ6qdDjF54+GfzAgQPo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",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    },
    {
     "data": {
      "image/png": "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gq9atUpRUVEubdHR0frXv/6V65iMjAxlZGQ4v6elpRVJbcYYPTRuldb9caJI1g8AwLVk69Bo+dlLJmZcUxOKU1JSFBwc7NIWHBystLQ0nTt3Lscxw4cPV2BgoPMTHh5eJLWdO59FsAEA4CpwTZ25KYhXX31Vffv2dX5PS0srsoBz0a9vRMnP7lmk2wAA4Grm61VyvwevqXATEhKiw4cPu7QdPnxYAQEB8vX1zXGMt7e3vL29i6M8Jz+7Z4mdigMA4Hp3TV2WioyMVEJCgkvbkiVLFBkZWUIVAQCAq02JhpvTp08rMTFRiYmJkv661TsxMVH79u2T9Nclpe7duzv7P/3009qzZ49eeeUVbd++XWPHjtWsWbP04osvlkT5AADgKlSi4ebXX39Vw4YN1bBhQ0lS37591bBhQw0aNEiSlJyc7Aw6klS5cmUtWLBAS5YsUf369fXuu+/qs88+uypuAwcAAFeHEp0Ycvvtt8sYk+vynJ4+fPvtt2vDhg1FWBUAALiWXVNzbgAAAC6HcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACyFcAMAACylxMPNmDFjFBERIR8fHzVr1kxr1qzJs//777+vmjVrytfXV+Hh4XrxxReVnp5eTNUCAICrXYmGm5kzZ6pv376Ki4vT+vXrVb9+fUVHR+vIkSM59p8+fboGDBiguLg4bdu2TRMmTNDMmTP12muvFXPlAADgalWi4Wb06NHq1auXYmNjVadOHY0bN05+fn6aOHFijv1//vlntWjRQl26dFFERITatm2rRx555LJnewAA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/PjxatWqlcqVK6dy5copKioqz/4AAOD6UuLhZubMmerbt6/i4uK0fv161a9fX9HR0Tpy5EiO/ZctW6ZHHnlEP/zwg1atWqXw8HC1bdtWBw8eLObKAQDA1chmjDElWUCzZs1066236uOPP5YkORwOhYeHq0+fPhowYMBlx2dlZalcuXL6+OOP1b1798v2T0tLU2BgoFJTUxUQEHDF9V90NvOC6gxaLEnaOjRafvZShbZuAACud+78/i7RMzeZmZlat26doqKinG0eHh6KiorSqlWr8rWOs2fP6vz58ypfvnxRlQkAAK4hJXp64dixY8rKylJwcLBLe3BwsLZv356vdfTv319hYWEuAenvMjIylJGR4fyelpZW8IIBAMBVr8Tn3FyJESNGaMaMGfrqq6/k4+OTY5/hw4crMDDQ+QkPDy/mKgEAQHEq0XATFBQkT09PHT582KX98OHDCgkJyXPsqFGjNGLECH333Xe65ZZbcu336quvKjU11fnZv39/odQOAACuTiUabux2uxo3bqyEhARnm8PhUEJCgiIjI3Md98477+jNN9/UokWL1KRJkzy34e3trYCAAJcPAACwrhK/padv377q0aOHmjRpoqZNm+r999/XmTNnFBsbK0nq3r27KlasqOHDh0uS/v3vf2vQoEGaPn26IiIilJKSIkkqU6aMypQpU2L7AQAArg4lHm5iYmJ09OhRDRo0SCkpKWrQoIEWLVrknGS8b98+eXj87wTTJ598oszMTD300EMu64mLi9PgwYOLs3QAAHAVKvHn3BQ3nnMDAMC155p5zg0AAEBhI9wAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLIdwAAABLKVXSBQC4vhljdOHCBWVlZZV0KQBKmJeXlzw9Pa94PYQbACUmMzNTycnJOnv2bEmXAuAqYLPZVKlSJZUpU+aK1kO4AVAiHA6HkpKS5OnpqbCwMNntdtlstpIuC0AJMcbo6NGjOnDggKpXr35FZ3AINwBKRGZmphwOh8LDw+Xn51fS5QC4Ctxwww3au3evzp8/f0XhhgnFAEqUhwc/hgD8pbDO3vJTBQAAWArhBgAsLD4+XmXLli3pMnJ0++2361//+le+++d3XyZMmKC2bdsWvDAUiQEDBqhPnz7Fsi3CDQC4oWfPnrLZbLLZbLLb7apWrZqGDh2qCxcuXHZsfHy8c2xun7179xb9TlzG3r17ZbPZ5OnpqYMHD7osS05OVqlSpa6aWi+Vnp6ugQMHKi4uLtuyAwcOyG63q27dutmWXdznxMTEbMtyCmEbNmxQp06dFBwcLB8fH1WvXl29evXSzp07C2tXspk7d67atm2rf/zjH7nWmpPZs2erVq1a8vHxUb169bRw4UKX5cYYDRo0SKGhofL19VVUVJR+//13lz7Hjx9X165dFRAQoLJly+rxxx/X6dOnXfps2rRJrVq1ko+Pj8LDw/XOO++4LO/Xr58mT56sPXv2uL/zbiLcAICb2rVrp+TkZP3+++966aWXNHjwYI0cOfKy42JiYpScnOz8REZGqlevXi5t4eHh+a4jMzPzSnbjsipWrKgpU6a4tE2ePFkVK1Ys0u1eiTlz5iggIEAtWrTItiw+Pl6dO3dWWlqaVq9eXeBtzJ8/X//3f/+njIwMff7559q2bZumTZumwMBADRw48ErKz9OZM2fUsmVL/fvf/873mJ9//lmPPPKIHn/8cW3YsEEdO3ZUx44dtWXLFmefd955Rx9++KHGjRun1atXq3Tp0oqOjlZ6erqzT9euXfXbb79pyZIlmj9/vn788Uc9+eSTzuVpaWlq27atbrrpJq1bt04jR47U4MGD9emnnzr7BAUFKTo6Wp988skVHol8MNeZ1NRUI8mkpqYW6nrPZJw3N/Wfb27qP9+cyThfqOsGrOjcuXNm69at5ty5cyVdilt69OhhOnTo4NJ21113mf/7v/8zp0+fNv7+/mb27Nkuy7/66ivj5+dn0tLSXNpbt25tXnjhBef3P/74w9x///2mdOnSxt/f33Tq1MmkpKQ4l8fFxZn69eub8ePHm4iICGOz2Ywxxpw4ccI8+eSTpkKFCsbb29vcfPPN5r///a8xxphJkyaZwMBAs2jRIlOrVi1TunRpEx0dbQ4dOpTrPiYlJRlJ5o033jDVq1d3WVajRg0zcOBAI8kkJSU525ctW2ZuvfVWY7fbTUhIiOnfv785f/5/PwtPnz5tunXrZkqXLm1CQkLMqFGjsu1/enq6eemll0xYWJjx8/MzTZs2NT/88INz+cV9ycu9995r+vXrl63d4XCYKlWqmEWLFpn+/fubXr165bjPGzZsyDb273WeOXPGBAUFmY4dO+a4/RMnTuRZX2HIq9ZLde7c2dx7770ubc2aNTNPPfWUMeav4xISEmJGjhzpXH7y5Enj7e1tvvjiC2OMMVu3bjWSzNq1a519vv32W2Oz2czBgweNMcaMHTvWlCtXzmRkZDj79O/f39SsWdNl25MnTzaVKlXKtd68fi648/ubMzcArgrGGJ3NvFAiH2PMFdXu6+urzMxMlS5dWg8//LAmTZrksnzSpEl66KGH5O/vn+s6HA6HOnTooOPHj2v58uVasmSJ9uzZo5iYGJd+u3bt0pdffqm5c+cqMTFRDodDd999t1auXKlp06Zp69atGjFihMtttGfPntWoUaM0depU/fjjj9q3b5/69et32f26//77deLECa1YsUKStGLFCp04cULt27d36Xfw4EHdc889uvXWW7Vx40Z98sknmjBhgt566y1nn5dfflnLly/XN998o++++07Lli3T+vXrXdbTu3dvrVq1SjNmzNCmTZvUqVMntWvXLtslkrysWLFCTZo0ydb+ww8/6OzZs4qKitKjjz6qGTNm6MyZM/le70WLFy/WsWPH9Morr+S4PK85QU8//bTKlCmT56ewrVq1SlFRUS5t0dHRWrVqlSQpKSlJKSkpLn0CAwPVrFkzZ59Vq1apbNmyLsc1KipKHh4ezjNgq1at0m233Sa73e6ynR07dujEiRPOtqZNm+rAgQNFfkmT59wAuCqcO5+lOoMWl8i2tw6Nlp/d/R+HxhglJCRo8eLFzomSTzzxhJo3b67k5GSFhobqyJEjWrhwoZYuXZrnuhISErR582YlJSU5L01NmTJFN998s9auXatbb71V0l+XoqZMmaIbbrhBkvTdd99pzZo12rZtm2rUqCFJqlKlisu6z58/r3Hjxqlq1aqS/goRQ4cOvez+eXl56dFHH9XEiRPVsmVLTZw4UY8++qi8vLxc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Cn41+uijj8yNN95o7Ha7adq0qfnll1+cy1q3bm169Ojh0n/WrFmmRo0axm63m5tvvtksWLCgmCu+NrlznG+66SYjKdsnLi6u+Au/xrj79/nvCDf55+5x/vnnn02zZs2Mt7e3qVKlinn77bfNhQsXirnqa487x/n8+fNm8ODBpmrVqsbHx8eEh4ebZ5991pw4caL4C7+G/PDDDzn+vL14bHv06GFat26dbUyDBg2M3W43VapUMZMmTSryOm3GcP4NAABYB3NuAACApRBuAACApRBuAACApRBuAACApRBuAACApRBuAACApRBuAACApRBuALiIj49X2bJlS7qMArPZbPr666/z7NOzZ0917NixWOoBUPwIN4AF9ezZUzabLdtn165dJV2a4uPjnfV4eHioUqVKio2N1ZEjRwpl/cnJybr77rslSXv37pXNZlNiYqJLnw8++EDx8fGFsr3cDB482Lmfnp6eCg8P15NPPqnjx4+7tR6CGOA+3goOWFS7du00adIkl7YbbrihhKpxFRAQoB07dsjhcGjjxo2KjY3VoUOHtHjx4ite9+XeHi9JgYGBV7yd/Lj55pu1dOlSZWVladu2bXrssceUmpqqmTNnFsv2gesVZ24Ai/L29lZISIjLx9PTU6NHj1a9evVUunRphYeH69lnn9Xp06dzXc/GjRt1xx13yN/fXwEBAWrcuLF+/fVX5/IVK1aoVatW8vX1VXh4uJ5//nmdOXMmz9psNptCQkIUFhamu+++W88//7yWLl2qc+fOyeFwaOjQoapUqZK8vb3VoEEDLVq0yDk2MzNTvXv3VmhoqHx8fHTTTTdp+PDhLuu+eFmqcuXKkqSGDRvKZrPp9ttvl+R6NuTTTz9VWFiYy1u4JalDhw567LHHnN+/+eYbNWrUSD4+PqpSpYqGDBmiCxcu5LmfpUqVUkhIiCpWrKioqCh16tRJS5YscS7PysrS448/rsqVK8vX11c1a9bUBx984Fw+ePBgTZ48Wd98843zLNCyZcskSfv371fnzp1VtmxZlS9fXh06dNDevXvzrAe4XhBugOuMh4eHPvzwQ/3222+aPHmyvv/+e73yyiu59u/atasqVaqktWvXat26dRowYIC8vLwkSbt371a7du304IMPatOmTZo5c6ZWrFih3r17u1WTr6+vHA6HLly4oA8++EDvvvuuRo0apU2bNik6Olr333+/fv/9d0nShx9+qHnz5mnWrFnasWOHPv/8c0VEROS43jVr1kiSli5dquTkZM2dOzdbn06dOunPP//UDz/84Gw7fvy4Fi1apK5du0qSfvrpJ3Xv3l0vvPCCtm7dqv/85z+Kj4/X22+/ne993Lt3rxYvXiy73e5sczgcqlSpkmbPnq2tW7dq0KBBeu211zRr1ixJUr9+/dS5c2e1a9dOycnJSk5OVvPmzXX+/HlFR0fL399fP/30k1auXKkyZcqoXbt2yszMzHdNgGUV+as5ARS7Hj16GE9PT1O6dGnn56GHHsqx7+zZs80//vEP5/dJkyaZwMBA53d/f38THx+f49jHH3/cPPnkky5tP/30k/Hw8DDnzp3Lccyl69+5c6epUaOGadKkiTHGmLCwMPP222+7jLn11lvNs88+a4wxpk+fPubOO+80Docjx/VLMl999ZUxxpikpCQjyWzYsMGlz6VvNO/QoYN57LHHnN//85//mLCwMJOVlWWMMaZNmzZm2LBhLuuYOnWqCQ0NzbEGY4yJi4szHh4epnTp0sbHx8f59uTRo0fnOsYYY5577jnz4IMP5lrrxW3XrFnT5RhkZGQYX19fs3jx4jzXD1wPmHMDWNQdd9yhTz75xPm9dOnSkv46izF8+HBt375daWlpunDhgtLT03X27Fn5+fllW0/fvn31xBNPaOrUqc5LK1WrVpX01yWrTZs26fPPP3f2N8bI4XAoKSlJtWvXzrG21NRUlSlTRg6HQ+np6WrZsqU+++wzpaWl6dChQ2rRooVL/xYtWmjjxo2S/rqkdNddd6lmzZpq166d7rvvPrVt2/aKjlXXrl3Vq1cvjR07Vt7e3vr888/18MMPy8PDw7mfK1eudDlTk5WVledxk6SaNWtq3rx5Sk9P17Rp05SYmKg+ffq49BkzZowmTpyoffv26dy5c8rMzFSDBg3yrHfjxo3atWuX/P39XdrT09O1e/fuAhwBwFoIN4BFlS5dWtWqVXNp27t3r+677z4988wzevvtt1W+fHmtWLFCjz/+uDIzM3P8JT148GB16dJFCxYs0Lfffqu4uDjNmDFD//znP3X69Gk99dRTev7557ONu/HGG3Otzd/fX+vXr5eHh4dCQ0Pl6+srSUpLS7vsfjVq1EhJSUn69ttvtXTpUnXu3FlRUVGaM2fOZcfmpn379jLGaMGCBbr11lv1008/6b333nMuP336tIYMGaIHHngg21gfH59c12u3253/DkaMGKF7771XQ4YM0ZtvvilJmjFjhvr166d3331XkZGR8vf318iRI7V69eo86z19+rQaN27sEiovulomjQMliXADXEfWrVsnh8Ohd99913lW4uL8jrzUqFFDNWrU0IsvvqhHHnlEkyZN0j//+U81atRIW7duzRaiLsfDwyPHMQEBAQoLC9PKlSvVunVrZ/vKlSvVtGlTl34xMTGKiYnRQw89pHbt2un48eMqX768y/ouzm/JysrKsx4fHx898MAD+vzzz7Vr1y7VrFlTjRo1ci5v1KiRduzY4fZ+XuqNN97QnXfeqWeeeca5n82bN9ezzz7r7HPpmRe73Z6t/kaNGmnmzJmqUKGCAgICrqgmwIqYUAxcR6pVq6bz58/ro48+0p49ezR16lSNGzcu1/7nzp1T7969tWzZMv3xxx9auXKl1q5d67zc1L9/f/3888/q3bu3EhMT9fvvv+ubb75xe0Lx37388sv697//rZkzZ2rHjh0aMGCAEhMT9cILL0iSRo8erS+++ELbt2/Xzp07NXv2bIWEhOT44MEKFSrI19dXixYt0uHDh5Wamprrdrt27aoFCxZo4sSJzonEFw0aNEhTpkzRkCFD9Ntvv2nbtm2aMWOG3njjDbf2LTIyUrfccouGDRsmSapevbp+/fVXLV68WDt37tTAgQO1du1alzERERHatGmTduzYoWPHjun8+fPq2rWrgoKC1KFDB/30009KSkrSsmXL9Pzzz+vAgQNu1QRYUklP+gFQ+HKahHrR6NGjTWhoqPH19TXR0dFmypQpRpI5ceKEMcZ1wm9GRoZ5+OGHTXh4uLHb7SYsLMz07t3bZbLwmjVrzF133WXKlCljSpcubW655ZZsE4L/7tIJxZfKysoygwcPNhUrVjReXl6mfv365ttvv3Uu//TTT02DBg1M6dKlTUBAgGnTpo1Zv369c7n+NqHYGGPGjx9vwsPDjYeHh2ndunWuxycrK8uEhoYaSWb37t3Z6lq0aJFp3ry58fX1NQEBAaZp06bm008/zXU/4uLiTP369bO1f/HFF8bb29vs27fPpKenm549e5rAwEBTtmxZ88wzz5gBAwa4jDty5Ijz+EoyP/zwgzHGmOTkZNO9e3cTFBRkvL29TZUqVUyvXr1MampqrjUB1wubMcaUbLwCAAAoPFyWAgAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlkK4AQAAlvL/VPJDiN64XWEAAAAASUVORK5CYII=",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plot_roc(np.array(all_labels_keras), np.array(all_probs_keras[:, 1]), \"Keras Model\")\n",
    "plt.show()\n",
    "plot_roc(np.array(all_labels_pytorch), np.array(all_probs_pytorch), \"PyTorch Model\")\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Comparing model performance\n",
    "\n",
    "Now compare the performance of different models to understand which model would be the best performer for your land classification task.\n",
    "Computed metrics for both models are used to generate a comparison table for key scores. This facilitates quick performance assessment between frameworks.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "\u001b[1mMetric\u001b[0m     | Keras Model     PyTorch Model  \n",
      "-------------------------------------------\n",
      "\u001b[1mAccuracy\u001b[0m   | 0.9958          0.9990         \n",
      "\u001b[1mPrecision\u001b[0m  | 0.9990          0.9990         \n",
      "\u001b[1mRecall\u001b[0m     | 0.9927          0.9990         \n",
      "\u001b[1mF1 Score\u001b[0m   | 0.9958          0.9990         \n",
      "\u001b[1mROC-AUC\u001b[0m    | 0.9998          1.0000         \n"
     ]
    }
   ],
   "source": [
    "# get the Keras model performance metrics\n",
    "metrics_keras = model_metrics(all_labels_keras, all_preds_keras, all_probs_keras, agri_class_labels)\n",
    "\n",
    "# get the PyTorch model performance metrics\n",
    "metrics_pytorch = model_metrics(all_labels_pytorch, all_preds_pytorch, all_probs_pytorch, agri_class_labels)\n",
    "\n",
    "\n",
    "# Display the comparison of metrics\n",
    "print(\"{:<18} | {:<15} {:<15}\".format('\\033[1m'+ 'Metric' + '\\033[0m',\n",
    "                                    'Keras Model', \n",
    "                                    'PyTorch Model'))\n",
    "print((\"\".join([\"-\" for _ in range(43)])))\n",
    "metrics_list = ['Accuracy', 'Precision', 'Recall', 'F1 Score', 'ROC-AUC']\n",
    "\n",
    "for k in metrics_list:\n",
    "    print(\"{:<18} | {:<15.4f} {:<15.4f}\".format('\\033[1m'+k+'\\033[0m',\n",
    "                                              metrics_keras[k],\n",
    "                                              metrics_pytorch[k]))"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Summary and discussion\n",
    "\n",
    "This notebook showcased a framework-agnostic workflow for importing, testing, and evaluating Vision Transformer models built in both Keras and PyTorch. By running the same input through each model, we examined the compatibility of results and gained practical experience handling architectural and data format variations.\n",
    "\n",
    "Key insights include the criticality of input format alignment, the subtle differences in model serialization/loading, and the framework-induced variations in prediction outputs. For a more robust evaluation, repeat this process with a labeled validation dataset, compute further metrics (precision, recall, F1-score), and systematically analyze speed and resource usage.\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Save and download the notebook for **final project** submission and evaluation\n",
    "\n",
    "You will need to save and download the completed notebook for final project submission and evaluation. \n",
    "<br>For saving and downloading the completed notebook, please follow the steps given below:</br>\n",
    "\n",
    "<font size = 4>  \n",
    "\n",
    "1) **Complete** all the tasks and questions given in the notebook.\n",
    "\n",
    "<img src=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/nv4jHlPU5_R1q7ZJrZ69eg/DL0321EN-M1L1-Save-IPYNB-Screenshot-1.png\" style=\"width:600px; border:0px solid black;\">\n",
    "\n",
    "2) **Save** the notebook.</style>\n",
    "<img src=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/9-WPWD4mW1d-RV5Il5otTg/DL0321EN-M1L1-Save-IPYNB-Screenshot-2.png\" style=\"width:600px; border:0px solid black;\">\n",
    "\n",
    "3) Identify and right click on the **correct notebook file** in the left pane.</style>\n",
    "<img src=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/RUSRPw7NT6Sof94B7-9naQ/DL0321EN-M1L1-Save-IPYNB-Screenshot-3.png\" style=\"width:600px; border:0px solid black;\">\n",
    "\n",
    "4) Click on **Download**.</style>\n",
    "<img src=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/HHry4GT-vhLEcRi1T_LHGg/DL0321EN-M1L1-Save-IPYNB-Screenshot-4.png\" style=\"width:600px; border:0px solid black;\">\n",
    "\n",
    "5) Download and **Save** the Jupyter notebook file on your computer **for final submission**.</style>\n",
    "<img src=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/hhsJbxc6R-T8_pXQGjMjvg/DL0321EN-M1L1-Save-IPYNB-Screenshot-5.png\" style=\"width:600px; border:0px solid black;\">\n",
    "  </font>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Conclusion\n",
    "Congratulations! You have successfully completed this lab and now you have a good understanding about loading custom pre-trained models, for both Keras and PyTorch frameworks. Using these pre-trained models, you can now evaluate their performance and also infer unknown datasets.\n",
    "I hope you have learnt to apply the key concepts of Keras/Pytorch based classifiers, both traditional CNNs and more advanced and state-of-the-art, CNN-ViT hybrid models. Using this knowledge, now you should be able to tackle a variety of real world image classification problems. Good luck!\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2>Author</h2>\n",
    "\n",
    "[Aman Aggarwal](https://www.linkedin.com/in/aggarwal-aman)\n",
    "\n",
    "Aman Aggarwal is a PhD working at the intersection of neuroscience, AI, and drug discovery. He specializes in quantitative microscopy and image processing.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<!--\n",
    "## Change Log\n",
    "\n",
    "|  Date (YYYY-MM-DD) |  Version | Changed By  |  Change Description |\n",
    "|---|---|---|---|\n",
    "| 2025-07-28  | 1.0  | Aman  |  Created the lab |\n",
    "\n",
    "-->\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "© Copyright IBM Corporation. All rights reserved.\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.12.8"
  },
  "prev_pub_hash": "0617c40a894fed25e60cecc592899ab7c410ed1cb7dbf852edb7281fb679f1af"
 },
 "nbformat": 4,
 "nbformat_minor": 4
}

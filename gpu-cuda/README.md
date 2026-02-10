# Jupyter GPU Docker Image

Docker image for Jupyter Notebook with PyTorch CUDA support and LLM/Data Science libraries.

## Base Image
- `quay.io/jupyter/base-notebook:latest`

## Included Libraries
- **PyTorch** with CUDA 12.1 support
- **Hugging Face**: transformers==4.37.2, datasets, accelerate, tokenizers
- **Data Science**: pandas, numpy, matplotlib, seaborn, scikit-learn
- **LLM Tools**: tiktoken, einops, wandb, tensorboard
- **NLP**: nltk, spacy

## GitHub Actions Setup

### Workflow Triggers
- Push to `master` branch with changes in `gpu-cuda/` directory
- Pull requests (excludes timestamped tags)

## Running the Image

### Local with GPU
```bash
docker run --gpus all -p 8888:8888 \
  -v $(pwd)/notebooks:/home/jovyan/work \
  public.ecr.aws/o0g3m8o6/codio-jupyter:gpu-cuda-latest
```

### Pull from ECR
```bash
# Pull image
docker pull public.ecr.aws/o0g3m8o6/codio-jupyter:gpu-cuda-latest

# Or use specific version
docker pull public.ecr.aws/o0g3m8o6/codio-jupyter:gpu-cuda-20260120
```

## Local Development

### Build locally
```bash
cd gpu
docker build -t codio-jupyter:gpu-cuda-latest .
```

### Test locally
```bash
docker run --gpus all -p 8888:8888 \
  -v $(pwd)/notebooks:/home/jovyan/work \
  codio-jupyter:gpu-cuda-latest
```

## Customization
Edit `requirements.txt` to add or modify Python packages, then push to trigger the workflow.

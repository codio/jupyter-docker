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

### AWS IAM Role Configuration
The workflow uses OIDC to authenticate with AWS. Ensure you have:
1. An IAM role named `GithubECRUploadRole_jupyter-docker` in account `878986216776`
2. Trust relationship configured for GitHub OIDC provider
3. Permissions to push to ECR Public

### GitHub Secrets
Add this secret to your repository (Settings → Secrets and variables → Actions):
- `ECR_REGISTRY` - Your ECR public registry URL (e.g., `public.ecr.aws/your-alias`)

### Workflow Triggers
- Push to `master` or `main` branch with changes in `gpu/` directory
- Pull requests (builds but doesn't push)
- Manual trigger via workflow_dispatch

## Running the Image

### Local with GPU
```bash
docker run --gpus all -p 8888:8888 \
  -v $(pwd)/notebooks:/home/jovyan/work \
  public.ecr.aws/your-alias/jupyter-gpu:latest
```

### Pull from ECR
```bash
# Pull image
docker pull public.ecr.aws/your-alias/jupyter-gpu:latest

# Or use specific version
docker pull public.ecr.aws/your-alias/jupyter-gpu:20260120-123456
```

## Local Development

### Build locally
```bash
cd gpu
docker build -t jupyter-gpu:latest .
```

### Test locally
```bash
docker run --gpus all -p 8888:8888 \
  -v $(pwd)/notebooks:/home/jovyan/work \
  jupyter-gpu:latest
```

## Customization
Edit `requirements.txt` to add or modify Python packages, then push to trigger the workflow.

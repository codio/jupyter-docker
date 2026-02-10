# Jupyter GPU Docker Image

Docker image for Jupyter Notebook.

## Base Image
- `quay.io/jupyter/base-notebook:latest`


### Workflow Triggers
- Push to `master` branch with changes in `standard/` directory
- Pull requests (excludes timestamped tags)

## Running the Image

### Local with GPU
```bash
docker run --gpus all -p 8888:8888 \
  -v $(pwd)/notebooks:/home/jovyan/work \
  public.ecr.aws/o0g3m8o6/codio-jupyter:standard-latest
```

### Pull from ECR
```bash
# Pull image
docker pull public.ecr.aws/o0g3m8o6/codio-jupyter:standard-latest

# Or use specific version
docker pull public.ecr.aws/o0g3m8o6/codio-jupyter:standard-20260120
```

## Local Development

### Build locally
```bash
cd gpu
docker build -t codio-jupyter:standard-latest .
```

### Test locally
```bash
docker run --gpus all -p 8888:8888 \
  -v $(pwd)/notebooks:/home/jovyan/work \
  codio-jupyter:standard-latest
```

## Customization
Edit `requirements.txt` to add or modify Python packages, then push to trigger the workflow.

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a Docker Compose configuration repository for deploying Ollama (an open-source local LLM inference platform) with hardware-optimized configurations. It provides separate deployments for CPU-only and GPU-accelerated environments.

## Architecture

The repository has a simple two-directory structure:

- `cpu/` - CPU-only Ollama deployment configuration
- `gpu/` - GPU-accelerated Ollama deployment with Open WebUI integration support

Each directory contains a standalone `docker-compose.yaml` file that can be deployed independently.

### CPU Configuration

- Uses `ollama/ollama` image
- Exposes port **11434** (standard Ollama API port)
- Persists model data using named volume at `/root/.ollama`
- Container name: `ollama`

### GPU Configuration

- Uses `ollama/ollama:latest` image
- Exposes port **3000** (mapped to 8080 internally, for Open WebUI integration)
- Contains commented reference for running Open WebUI alongside Ollama
- Designed for GPU acceleration (requires `--gpus=all` flag when running)

## Common Commands

### Start Ollama (CPU)
```bash
cd cpu
docker-compose up -d
```

### Start Ollama (GPU)
```bash
cd gpu
docker-compose up -d
```

### Stop Services
```bash
docker-compose down
```

### View Logs
```bash
docker-compose logs -f
```

### Remove Volumes (WARNING: deletes all models)
```bash
docker-compose down -v
```

### Access Ollama API
Once running, the Ollama API is available at:
- CPU variant: `http://localhost:11434`
- GPU variant: `http://localhost:3000` (if using Open WebUI port mapping)

## Important Notes

- This repository uses official Ollama images with no custom modifications
- Model data is persisted in Docker named volumes (`ollama` volume)
- The GPU configuration references Open WebUI integration in comments - this can be used as a template for adding a web interface
- Each configuration is standalone and can be run independently
- No build process is required - uses pre-built Docker images

## Related Services

This repository is part of a larger collection of self-hosted services located in the parent directory `/home/kiogreo/Desktop/helper/`, which includes Open WebUI, databases, and other infrastructure services.

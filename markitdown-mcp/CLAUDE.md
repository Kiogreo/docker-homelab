# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository provides a Docker image for running `markitdown-mcp`, an MCP (Model Context Protocol) server for the MarkItDown document conversion library.

## Build Commands

```bash
# Build the Docker image
docker build -t markitdown-mcp .

# Build with custom user/group IDs
docker build --build-arg USERID=1000 --build-arg GROUPID=1000 -t markitdown-mcp .
```

## Running the Container

```bash
# Run the MCP server (mount a directory to /workdir for file access)
docker run -v /path/to/documents:/workdir markitdown-mcp
```

## Environment Variables

- `EXIFTOOL_PATH=/usr/bin/exiftool` - Path to exiftool binary
- `FFMPEG_PATH=/usr/bin/ffmpeg` - Path to ffmpeg binary
- `MARKITDOWN_ENABLE_PLUGINS=True` - Enables MarkItDown plugin support

## Architecture

The image is based on `python:3.13-slim-bullseye` and includes:
- `ffmpeg` - For audio/video file processing
- `exiftool` - For metadata extraction
- The `markitdown-mcp` Python package installed via pip

The container runs as a non-root user (default: `nobody:nogroup`) and uses `/workdir` as the working directory.

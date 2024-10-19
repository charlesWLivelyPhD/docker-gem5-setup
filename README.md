
# Author: Dr. Charles Lively III
# Docker and gem5 Simulator Setup Guide

This repository provides a comprehensive guide to install Docker and run the gem5 simulator within a Docker container.
The guide is designed for complete beginners, offering detailed steps for setting up Docker and the gem5 simulator on Windows, macOS, and Ubuntu.

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
- [Installing Docker](#installing-docker)
  - [Windows](#windows)
  - [macOS](#macos)
  - [Ubuntu](#ubuntu)
- [Setting Up gem5 in Docker](#setting-up-gem5-in-docker)
- [Conclusion](#conclusion)

## Introduction
Docker is a platform that enables running applications in isolated containers, providing a consistent environment across different systems.
The gem5 simulator is an open-source system simulator used for computer architecture research. In this guide, you'll learn how to use Docker to run gem5.

## Prerequisites
- No prior knowledge of Docker or gem5 is required.
- Ensure your computer has at least 4GB of RAM and enough storage for Docker images.

## Installing Docker

### Windows
1. **Download Docker Desktop:**
   - Visit the [Docker Desktop for Windows download page](https://www.docker.com/products/docker-desktop) and download the installer.

2. **Install Docker Desktop:**
   - Double-click the downloaded installer to start the installation process.
   - Follow the setup instructions, accepting the license agreement.
   - Choose "Use WSL 2 instead of Hyper-V" for better performance. You may need to enable WSL 2 during installation.
   - Restart your computer if prompted.

3. **Start Docker Desktop:**
   - Once installed, Docker Desktop should start automatically. If not, find "Docker Desktop" in the Start Menu and launch it.
   - Wait for Docker to initialize, which might take a few minutes.

4. **Verify Docker Installation:**
   - Open Command Prompt (cmd) and run the following command:
     ```bash
     docker --version
     ```

5. **Enable Docker Settings:**
   - Open Docker Desktop settings and allocate 2GB of memory for running gem5.

### macOS
1. **Download Docker Desktop:**
   - Navigate to the [Docker Desktop for Mac download page](https://www.docker.com/products/docker-desktop) and download the installer.

2. **Install Docker Desktop:**
   - Open the downloaded `.dmg` file and drag the Docker icon to the Applications folder.
   - Launch Docker from the Applications folder.
   - Follow the setup instructions, which may include enabling security settings in System Preferences.

3. **Verify Docker Installation:**
   - Open Terminal and run:
     ```bash
     docker --version
     ```

4. **Configure Docker Settings:**
   - Open Docker Desktop, navigate to settings, and allocate 2GB of memory.

### Ubuntu
1. **Update System Packages:**
   ```bash
   sudo apt update
   ```

2. **Install Docker:**
   - Install Docker with the following command:
     ```bash
     sudo apt install docker.io -y
     ```

3. **Start and Enable Docker:**
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

4. **Verify Docker Installation:**
   ```bash
   docker --version
   ```

5. **Add Your User to the Docker Group:**
   - Run this command to use Docker without `sudo`:
     ```bash
     sudo usermod -aG docker $USER
     ```
   - Log out and back in for the changes to take effect.

## Setting Up gem5 in Docker

1. **Create a Directory for gem5:**
   - On your host machine, create a directory to store gem5 files:
     ```bash
     mkdir ~/gem5
     ```

2. **Pull and Run the gem5 Docker Image:**
   - Use the following command to pull and run the pre-built Docker image for gem5:
     ```bash
     docker run -tid --hostname=gem5_dev --name=gem5_container -v ~/gem5:/root ghcr.io/gem5/ubuntu-24.04_all-dependencies:v24-0 /bin/bash
     ```

3. **Access the gem5 Container:**
   - Enter the Docker container with:
     ```bash
     docker exec -ti gem5_container /bin/bash
     ```

4. **Clone and Build gem5:**
   - Once inside the container, clone the gem5 repository:
     ```bash
     git clone https://github.com/gem5/gem5.git
     cd gem5
     scons build/X86/gem5.opt -j8
     ```

5. **Run a gem5 Simulation:**
   - To verify the setup, run a simple gem5 simulation:
     ```bash
     build/X86/gem5.opt configs/learning_gem5/part1/simple.py
     ```

## Conclusion
By following these detailed steps, you have successfully installed Docker, set up a containerized environment, and configured gem5 within Docker. This setup ensures a consistent environment for exploring gem5 simulations.

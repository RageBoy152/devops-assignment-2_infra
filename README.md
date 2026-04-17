# Assignment 2 Infra (Repo B CD Pipeline)

This repo now contains a manual, parameterized Jenkins CD pipeline that:

1. Provisions a new AWS private key.
2. Provisions a new EC2 instance.
3. Installs Docker, pulls a selected image tag, and runs it on port 80.
4. Performs a final automated health check with `curl` against the instance public IP.
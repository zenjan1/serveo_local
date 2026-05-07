# serveo_local - Self-hosted Serveo Server

Serveo.net is a way to ssh and redirect ports on the internet. These are instructions to get your local copy of the serveo server application running, which is not dependent upon serveo.net.

**Note**: The original serveo binary from Google Cloud Storage is no longer available (billing account closed). You may need to find an alternative binary or compile from source.

## Quick Setup

On a server (e.g., DigitalOcean Ubuntu VPS):

```bash
# 1. SSH into your server
# 2. Install dependencies
sudo apt update && sudo apt upgrade -y

# 3. Download serveo binary (original URL may be unavailable)
wget https://storage.googleapis.com/serveo/download/2018-05-08/serveo-linux-amd64 -O serveo
chmod +x serveo

# 4. Generate SSH host keys
ssh-keygen -t rsa -f ssh_host_rsa_key

# 5. Run serveo with your domain
./serveo --port=2222 -domain=yourdomain.com

# Or run in background
nohup ./serveo --port=2222 -domain=yourdomain.com &
```

On a client:

```bash
# Connect to your self-hosted serveo
ssh <server-ip> -p 2222 -R 80:localhost:8000 yourdomain.com
```

## Shell Wrapper (serveo)

The `serveo` script in this repo is a shell wrapper that simplifies using serveo.net or your self-hosted serveo:

```bash
./serveo http <subdomain>   # HTTP tunnel
./serveo tcp <port>         # TCP tunnel
./serveo kill               # Kill tunnel process
```

## Requirements

- SSH client installed
- Self-hosted: A server with SSH access and a domain

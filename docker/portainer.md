# Portainer Setup

## Installation Method
Portainer was deployed as a Docker container on Ubuntu Server.

## Docker Command Used

```bash
docker volume create portainer_data

docker run -d \
  --name portainer \
  -p 9000:9000 \
  -p 8000:8000 \
  --restart=always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  portainer/portainer-ce

```

## Access

* URL: http://<VM-IP>:9000
* Initial admin user created on first access

## Firewall Notes

* Proxmox firewall rule added to allow TCP 9000 from LAN
* UFW enabled on Ubuntu and allowed 9000/tcp

## Validation

* docker ps confirms container running
* Web UI accessible

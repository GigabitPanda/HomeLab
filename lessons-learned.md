
# Lessons Learned

- Proxmox firewall rules apply hierarchically; blocking at Datacenter affects everything
- Portainer uses HTTP by default on port 9000
- Always verify with `docker ps` and `ss -tlnp`
- Bind mounts are critical for persistent data
- Documenting issues saves time later

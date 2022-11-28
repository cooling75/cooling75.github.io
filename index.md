# Test to restore backups

***

Just as a small reminder (for you) and note to myself to test restoring backups regularly.

## InfluxDB restore

Copy files to path which is available to the InfluxDB container. In my case a Kubernetes persistent volume on a NFS share.

```bash
kubectl exec -it infuxdb -n influxdb -- /bin/bash
influxd restore -portable /path/to/backup
```

## Vaultwarden

Fetch backuped db.sqlite3 file and mount the parent directory in the data folder inside the container.

```bash
docker run -d --name vaultwarden \
-v ~/docker/vaultwarden/vw-data/:/data/ \
-p 80:80 \
vaultwarden/server:latest 
```

Visit localhost and login to vaultwarden as usual.

# Hi-ha-hacking!

***

Or simply using the hacker remote theme in github pages took me some minutes. In case you have already some posts available in your repository just save them somewhere else and delete the complete folder. The hacker theme uses a single markdown file __index.md__ in the root of the repo.

# Use kubectl without 'sudo' 

***

By simply looking at the output I had to do a
```bash
chmod +r /etc/rancher/k3s/k3s.yml'
```
After that I was able to invoke kubectl without typing 'sudo' all the time.  
Unfortunately this workaround is not working after a reboot, you have to change it again.

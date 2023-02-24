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
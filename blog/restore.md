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


### Restore in Docker

Fetch backuped db.sqlite3 file and mount the parent directory in the data folder inside the container.

```bash
docker run -d --name vaultwarden \
-v ~/docker/vaultwarden/vw-data/:/data/ \
-p 80:80 \
vaultwarden/server:latest 
```

Visit localhost and login to vaultwarden as usual.


### Restore in Kubernetes

#### nfs-client

Copy backuped db.sqlite3 file from backup location to NFS share which is actively in use.  
This can be identified by not having the "archived-" prefix on the NFS share.  

1. Copy the file (using a different name then db.sqlite3 since this is already existing)
2. Delete .wal and .shm files
3. Rename backuped file to db.sqlite3
4. Delete the pod to initiate restart
5. Verify that restore was successful

[Vaultwarden Backup Hints](https://github.com/dani-garcia/vaultwarden/wiki/Backing-up-your-vault#restoring-backup-data)

## Grafana

### Kubernetes

#### nfs-client

Just copy grafana.db from backup (or "archived-xxx" folder) to already existing (active) pvc in NFS share. Delete currently running pod and wait for it to be restarted from deployment. Login should work again with old account(s).
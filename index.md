# Hi-ha-hacking!

Or simply using the hacker remote theme in github pages took me some minutes. In case you have already some posts available in your repository just save them somewhere else and delete the complete folder. The hacker theme uses a single markdown file __index.md__ in the root of the repo.

# Use kubectl without 'sudo' 

By simply looking at the output I had to do a
```bash
chmod +r /etc/rancher/k3s/k3s.yml'
```
After that I was able to invoke kubectl without typing 'sudo' all the time.  
Unfortunately this workaround is not working after a reboot, you have to change it again.

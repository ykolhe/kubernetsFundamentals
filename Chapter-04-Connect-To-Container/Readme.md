# Definition
The `kubectl exec` command opens an interactive session or runs a specific command inside a container that is already running within a Pod. It is the Kubernetes equivalent of `docker exec`.

# Real-World Example
Imagine your Nginx server is showing a 404 error. Instead of guessing why, you "teleport" inside the server (the container) to look at the actual HTML files in `/usr/share/nginx/html` to see if they are missing or corrupted.

# Rules
1. **Status**: The Pod must be in the `Running` state.
2. **Interactive Flag**: You must use `-i` (interactive) and `-t` (tty) together as `-it` to get a working shell prompt.
3. **Shell Availability**: The container must have a shell installed (like `sh` or `bash`).
4. **Targeting**: If a Pod has multiple containers, you must specify which one using the `-c` flag.

# Code
# 1. Create a pod to practice with
kubectl run nginx-db --image=nginx

# 2. Execute a single command without entering the shell
# Syntax: kubectl exec <POD_NAME> -- <COMMAND>
kubectl exec nginx-db -- ls /etc/nginx

# 3. Connect to the container via an interactive shell (Bash)
# Syntax: kubectl exec -it <POD_NAME> -- /bin/bash
kubectl exec -it nginx-db -- /bin/bash

# 4. Once inside the shell (you will see a root@nginx-db:/# prompt):
# Run: cd /usr/share/nginx/html && ls
# Run: exit (to leave the container and return to your PC)

# 5. Cleanup the specific pod
kubectl delete pod nginx-db

# Expected Output Box
----------------------------------------------------------------------
| > kubectl exec -it nginx-db -- /bin/bash                           |
| root@nginx-db:/# ls                                                |
| bin  boot  dev  etc  home  lib  media  mnt  opt  proc  root  ...   |
| root@nginx-db:/# exit                                              |
| exit                                                               |
|                                                                    |
| > kubectl delete pod nginx-db                                      |
| pod "nginx-db" deleted                                             |
----------------------------------------------------------------------

# Quick Reference for Specific Targeting
- kubectl exec <POD_NAME> -- printenv          # Check environment variables
- kubectl exec -it <POD_NAME> -- sh            # Use 'sh' if 'bash' is not available
- kubectl exec <POD_NAME> -c <CONTAINER_NAME>  # Target a specific container in a multi-container pod
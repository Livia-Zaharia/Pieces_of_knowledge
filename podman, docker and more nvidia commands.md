# PODMAN

```bash
podman-compose up
```
This pulls the image and runs the containers

```bash
podman-compose down
```
This is used after CTRL+C to stop running containers in the background

```bash
podman pull
```
This is used to pull the image of the container just in case it doesn't updates at up command- especially for those marked with latest



# DOCKER

```bash
docker volume prune
docker network prune
docker system prune -a
```
List running containers
```bash
docker ps
```

Stop all running containers
```bash
docker stop $(docker ps -a -q)
```

Remove all stopped containers
```bash
docker rm $(docker ps -a -q)
```

List images
```bash
docker images
```

Remove the specific image
```bash
docker rmi raychanan/mineru
```

Or remove all images (be careful with this if you have other important images)
```bash
docker rmi $(docker images -q)
```

Remove unused data
```bash
docker system prune -a
```



# NVIDA 

```bash
nvidia-smi


+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 535.183.01             Driver Version: 535.183.01   CUDA Version: 12.2     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA GeForce GTX 1050        Off | 00000000:01:00.0 Off |                  N/A |
| N/A   46C    P5              N/A / ERR! |    396MiB /  4096MiB |      0%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+
                                                                                         
+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|    0   N/A  N/A       895      G   /usr/lib/xorg/Xorg                          231MiB |
|    0   N/A  N/A      2277      G   cinnamon                                     47MiB |
|    0   N/A  N/A     63394      G   /app/bin/telegram-desktop                     1MiB |
|    0   N/A  N/A    244818      G   ...erProcess --variations-seed-version       60MiB |
|    0   N/A  N/A    248366      G   ...seed-version=20250221-050109.072000       53MiB |
+---------------------------------------------------------------------------------------+

```
to see the config of your nvidia driver(hardware)

```bash
nvcc --version


nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2021 NVIDIA Corporation
Built on Thu_Nov_18_09:45:30_PST_2021
Cuda compilation tools, release 11.5, V11.5.119
Build cuda_11.5.r11.5/compiler.30672275_0

```
to see the config of cuda compilation tools

```bash
dpkg -l | grep nvidia-container-toolkit
```

```bash
sudo docker info | grep Runtimes
ii  nvidia-container-toolkit                         1.17.4-1                                   amd64        NVIDIA Container toolkit
ii  nvidia-container-toolkit-base                    1.17.4-1                                   amd64        NVIDIA Container Toolkit Base
```

-------------------------
dpkg -l | grep nvidia-docker
just-semantic-search-all-py3.11livialinux@livialinux-GL553VD:~/server/just-semantic-search$ sudo docker info | grep Runtimes
[sudo] password for livialinux:                       
 Runtimes: io.containerd.runc.v2 runc
just-semantic-search-all-py3.11livialinux@livialinux-GL553VD:~/server/just-semantic-search$ sudo docker run --rm --gpus all nvidia/cuda:11.5.0-base nvidia-smi
Unable to find image 'nvidia/cuda:11.5.0-base' locally
docker: Error response from daemon: manifest for nvidia/cuda:11.5.0-base not found: manifest unknown: manifest unknown.
See 'docker run --help'.
just-semantic-search-all-py3.11livialinux@livialinux-GL553VD:~/server/just-semantic-search$ dpkg -l | grep nvidia-container-toolkit
just-semantic-search-all-py3.11livialinux@livialinux-GL553VD:~/server/just-semantic-search$ sudo cat /etc/docker/daemon.json
cat: /etc/docker/daemon.json: No such file or directory
just-semantic-search-all-py3.11livialinux@livialinux-GL553VD:~/server/just-semantic-search$ # Detect distribution
distribution=$(. /etc/os-release; echo $ID$VERSION_ID)
if [[ "$distribution" != "ubuntu22.04" && "$distribution" != "ubuntu20.04" && "$distribution" != "debian12" ]]; then
    echo "Warning: Your distribution ($distribution) may not be supported. Manually set the correct version if needed." 
    distribution="ubuntu22.04"  # Change this if necessary
fi

# Setup NVIDIA GPG key and repository
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
    && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

# Update package listings
sudo apt-get update

# Install NVIDIA Container Toolkit
sudo apt-get install -y nvidia-container-toolkit

# Restart Docker (to apply changes)
sudo systemctl restart docker
Warning: Your distribution (linuxmint21.3) may not be supported. Manually set the correct version if needed.
File '/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg' exists. Overwrite? (y/N) n
Enter new filename: 
gpg: signal 2 caught ... exiting

E: Type '<!doctype' is not known on line 1 in source list /etc/apt/sources.list.d/nvidia-container-toolkit.list
E: The list of sources could not be read.
E: Type '<!doctype' is not known on line 1 in source list /etc/apt/sources.list.d/nvidia-container-toolkit.list
E: The list of sources could not be read.
just-semantic-search-all-py3.11livialinux@livialinux-GL553VD:~/server/just-semantic-search$ distribution="ubuntu22.04"
just-semantic-search-all-py3.11livialinux@livialinux-GL553VD:~/server/just-semantic-search$ # Detect distribution
distribution=$(. /etc/os-release; echo $ID$VERSION_ID)
if [[ "$distribution" != "ubuntu22.04" && "$distribution" != "ubuntu20.04" && "$distribution" != "debian12" ]]; then
    echo "Warning: Your distribution ($distribution) may not be supported. Manually set the correct version if needed." 
    distribution="ubuntu22.04"  # Change this if necessary
fi

# Setup NVIDIA GPG key and repository
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
    && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

# Update package listings
sudo apt-get update

# Install NVIDIA Container Toolkit
sudo apt-get install -y nvidia-container-toolkit

# Restart Docker (to apply changes)
sudo systemctl restart docker
Warning: Your distribution (linuxmint21.3) may not be supported. Manually set the correct version if needed.
File '/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg' exists. Overwrite? (y/N) 
gpg: signal 2 caught ... exiting

E: Type '<!doctype' is not known on line 1 in source list /etc/apt/sources.list.d/nvidia-container-toolkit.list
E: The list of sources could not be read.
E: Type '<!doctype' is not known on line 1 in source list /etc/apt/sources.list.d/nvidia-container-toolkit.list
E: The list of sources could not be read.
just-semantic-search-all-py3.11livialinux@livialinux-GL553VD:~/server/just-semantic-search$ # Setup the repository and GPG key
distribution="ubuntu22.04" \
    && curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidi
a-container-toolkit-keyring.gpg \
    && curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

# Update package listings
sudo apt-get update

# Install the toolkit
sudo apt-get install -y nvidia-container-toolkit

# Configure Docker to use NVIDIA runtime
sudo nvidia-ctk runtime configure --runtime=docker


-------------------------

#Configure Docker to use NVIDIA runtime
sudo nvidia-ctk runtime configure --runtime=docker

# Create daemon.json if it doesn't exist
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<EOF
{
    "runtimes": {
        "nvidia": {
            "path": "nvidia-container-runtime",
            "runtimeArgs": []
        }
    }
}
EOF
INFO[0000] Config file does not exist; using empty config 
INFO[0000] Wrote updated config to /etc/docker/daemon.json 
INFO[0000] It is recommended that docker daemon be restarted. 
{
    "runtimes": {
        "nvidia": {
            "path": "nvidia-container-runtime",
            "runtimeArgs": []
        }
    }
}


sudo systemctl restart docker
sudo docker run --rm --gpus all nvidia/cuda:12.2.0-base nvidia-smi

# Install Docker on ubuntu 20.04 (Jenkins Server) and Permission for jenkins user to access docker

Letting iptables see bridged traffic
```
lsmod | grep br_netfilter
sudo modprobe br_netfilter
```
```
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
br_netfilter
EOF
```
```
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
```
```
sudo sysctl --system
```
# CRE docker INSTALL

#Install using the repository
# Update the apt package index and install packages to allow apt to use a repository over HTTPS:
```
sudo -i 

    apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
 

#Add Docker’s official GPG key:
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
# Use the following command to set up the stable repository.
```
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
# Install Docker Engine

# Update the apt package index, and install the latest version of Docker Engine and containerd, or go to the next step to install a specific version:
```
apt-get update
```
```
apt-get install docker-ce docker-ce-cli containerd.io
```
# Configure the Docker daemon, in particular to use systemd for the management of the container’s cgroups
```
sudo mkdir /etc/docker
cat <<EOF | sudo tee /etc/docker/daemon.json
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
```

# Restart Docker and enable on boot:
```
{
sudo systemctl enable docker
sudo systemctl daemon-reload
sudo systemctl restart docker
}
```

# Provide permissions to jenkins user in jenkins server to access docker
```
  sudo usermod -aG docker jenkins
  sudo chmod 777 /var/run/docker.sock
```
  
# Add Jenkins user into sudoers file to get sudo access
```
  vi /etc/sudoers
   jenkins ALL=(ALL) NOPASSWD: ALL
```

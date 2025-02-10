# Installation Guide (Ubuntu)

## 1. Install Git
```bash
sudo apt update
sudo apt install git -y
```

### Verify Installation:
```bash
git --version
```

---

## 2. Install Jenkins
```bash
sudo apt update
sudo apt install openjdk-11-jdk -y
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt update
sudo apt install jenkins -y
sudo systemctl enable --now jenkins
```

### Verify Installation:
```bash
systemctl status jenkins
```
Access Jenkins at: `http://<your-server-ip>:8080`

---

## 3. Install Docker
```bash
sudo apt update
sudo apt install -y ca-certificates curl gnupg
test -d /etc/apt/keyrings || sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo tee /etc/apt/keyrings/docker.asc > /dev/null
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Verify Installation:
```bash
docker --version
sudo systemctl status docker
```

### Run Docker without sudo (Optional):
```bash
sudo usermod -aG docker $USER
newgrp docker
```

---
### Notes:
- Jenkins runs on port `8080` by default.
- After installing Jenkins, retrieve the initial admin password using:
  ```bash
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
  ```
- Ensure Docker is running before using it.
- Restart your system after adding your user to the `docker` group.



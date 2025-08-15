We will install Gitlab CE

In this example, we are installing on RHEL8 VM. I've already created the self signed certs using the command below: create self-signed cert with "openssl req -new -x509 -newkey rsa:4096 -nodes -out ssl/server-cert.pem -keyout ssl/server-key.pem -days 3650 -subj "/C=US/ST=Massachusetts/L=Boston/O=example/OU=example/CN=example"

Edit docker-compose and put the FQDN of the server in place of my.gitlab
```
sudo systemctl stop fapolicyd
sudo systemctl disable fapolicyd
sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
sudo dnf -y module enable container-tools
sudo dnf -y install docker-ce git --allowerasing
sudo systemctl start docker && sudo systemctl enable docker
sudo usermod -aG docker $LOGNAME
newgrp docker
git clone https://github.com/joelckwong/DevSecOps-Servers.git
cd DevSecOps-Servers/gitlab
sudo mkdir -p /data/gitlab/config /data/gitlab/logs /data/gitlab/data /data/gitlab-runner
docker compose up -d
sudo firewall-cmd --permanent --add-port=443/tcp
sudo firewall-cmd --reload
sudo firewall-cmd --list-ports
```
In the web browser go to https://FQDN
login as root/secret_pass

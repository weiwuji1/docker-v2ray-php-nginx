一键dd

bash <(wget --no-check-certificate -qO- 'https://moeclub.org/attachment/LinuxShell/InstallNET.sh') -u 16.04 -v 64 -a

	root
	MoeClub.org

curl https://raw.githubusercontent.com/kirincastle/docker-v2ray-php-nginx/master/krsource.list | sudo tee /etc/apt/sources.list \
&& wget 'https://github.com/cx9208/Linux-NetSpeed/raw/master/tcp.sh' \
&& chmod +x tcp.sh \
&& ./tcp.sh

apt update \
&& apt -y install git nano curl mtr wget speedtest-cli \
&& apt upgrade -y \
&& apt autoremove -y \
&& systemctl reboot

curl -fsSL https://get.docker.com -o get-docker.sh \
&& sh get-docker.sh \
&& curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
&& chmod +x /usr/local/bin/docker-compose \
&& ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose \
&& git clone https://github.com/kirincastle/docker-v2ray-php-nginx.git \
&& cd docker-v2ray-php-nginx \
&& chmod +x ./init-letsencrypt.sh

修改v2ray配置
进入docker-v2ray目录开始修改配置。

1) init-letsencrypt.sh

将里面的domains和email修改为自己的域名和邮箱。

2) docker-compose.yml

可以不用动。

3) data/v2ray/config.json

修改ID，"id": "bae399d4-13a4-46a3-b144-4af2c0004c2e"，还是修改一下吧。

用这个网址来生成version 1 uuid https://www.uuidgenerator.net/version1

4) data/nginx/conf.d/v2ray.conf

修改所有your_domain为自己的域名，其他地方，如果上面可以修改的地方你没修改，那么除了域名之外的也不用修改了。

一键部署v2ray

./init-letsencrypt.sh \
&& docker ps \
&& docker exec v2ray bash -c "v2ray info" \
&& docker exec -it v2ray /bin/bash
v2ray log
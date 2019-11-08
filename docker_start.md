## ������� ��Ŀ ��ġ �غ�
sudo apt update
sudo apt install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update

apt-cache policy docker-ce

## ��Ŀ ��ġ
sudo apt install docker-ce docker-ce-cli containerd.io

## ���� ���� Ȯ��(��Ŀ)
sudo systemctl status docker

## ��Ŀ �̹��� �ٿ�ε�(haribo-mySQL)
docker pull emblockit/haribo-mysql

## ��Ŀ �̹��� Ȯ��
docker images

## �����̳� ����(�����̳� �����)
docker run -d -p 3306:3306 --name haribo-mysql emblockit/haribo-mysql

## �����̳� ���� Ȯ��
docker ps -a

## ��Ŀ �����̳� ���� �α� ����
docker logs -f haribo-mysql

## ��Ŀ �����̳� ���� �� ����
docker stop haribo-mysql
docker start haribo-mysql

### ���� �������� ����ڿ��� �����ֱ�(docker�� root������ �⺻�̱� ����)
sudo usermod -a -G docker $USER
sudo service docker restart

# Dockerfile �ۼ�
```
FROM ubuntu

COPY ./go-ethereum /home/go-ethereum
WORKDIR /home/go-ethereum/

RUN apt-get update
RUN apt-get install -y build-essential libgmp3-dev golang git

RUN git checkout refs/tags/v1.5.5
RUN make geth
RUN cp build/bin/geth /usr/local/bin

WORKDIR /home/DATA_STORE/
COPY ./CustomGenesis.json /home/DATA_STORE

RUN geth --datadir "/home/DATA_STORE" init /home/DATA_STORE/CustomGenesis.json
```

# PJT03 docker Container �����
```
docker run -d --name �����̳� �̸� -p 3306:3306 -e MYSQL_ROOT_PASSWORD=������ ��й�ȣ mysql
-d : detach
-e : �����̳� ȯ�溯�� (MYSQL_ROOT_PASSWORD)

docker run -d --name MySQL_Pjt03 -p 3306:3306 -e MYSQL_ROOT_PASSWORD=ssafy mysql mysqld --lower_case_table_names=1 --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```

## ���� �����̳ʿ��� ���μ��� ����(docker container exec)
```
docker container exec [�ɼ�] <�����̳� �ĺ���> <������ ���> [�μ�]
docker container exec -it MySQL_Pjt03 /bin/bash
```
___
# ��Ŀ ���Ϸ� �����̳� ����� npm, yarn, jar
docker build -t <name> <Dockerfile ��ġ>

### jar
```
# ��Ŀ �̹��� ����
FROM openjdk@sha256:08bf396d2e7e82b12d9c78d7e75137c1159c07f18f203391aa599adcb3643097

# ��Ŀ ���� ���丮 ����
WORKDIR /docker_dir

# ȣ��Ʈ���� ��Ŀ�� ���� ����(���� ��� �Ұ���)
COPY SpringBootDDT.jar /docker_dir/

# �ܺ� ��Ʈ
EXPOSE 8888

# jar file ����
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/docker_dir/SpringBootDDT.jar"]
```
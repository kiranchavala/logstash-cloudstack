System requirement for ELK 

Centos 7/8 with about 4gb ram 

1. Cloudstack management server
2. Logstash server
3. Elastic search server
4. Grafana server


**Step 1**

Install filebeat on Cloudstack server

sudo rpm --import https://packages.elastic.co/GPG-KEY-elasticsearch

cat /etc/yum.repos.d/elk.repo

```
[elk-8.x]
name=Elastic repository for 8.x packages
baseurl=https://artifacts.elastic.co/packages/8.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```
yum install filebeat
systemctl enable filebeat

Populate the contents of filebet.yml in the following path 

cat /etc/filebeat/filebeat.yml

systemctl start filebeat


**Step 2**

Install Logstash on the Logstash server


sudo rpm --import https://packages.elastic.co/GPG-KEY-elasticsearch

cat /etc/yum.repos.d/elk.repo

```
[elk-8.x]
name=Elastic repository for 8.x packages
baseurl=https://artifacts.elastic.co/packages/8.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
````
yum install logstash

Make sure logstash.conf is present in the respective path and also the grok patterns under /etc/logstash/patterns

Start the logstash service

/usr/share/logstash/bin/logstash  -f /etc/logstash/conf.d/logstash.conf  --path.settings /etc/logstash/


**Step 3**

Install elastic search

sudo rpm --import https://packages.elastic.co/GPG-KEY-elasticsearch

cat /etc/yum.repos.d/elk.repo

```
[elk-8.x]
name=Elastic repository for 8.x packages
baseurl=https://artifacts.elastic.co/packages/8.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
````


yum install --enablerepo=elasticsearch elasticsearch 



**Step 4**

Install grafana 

cat /etc/yum.repos.d/grfana.repo

wget -q -O gpg.key https://rpm.grafana.com/gpg.key
sudo rpm --import gpg.key


[grafana]
name=grafana
baseurl=https://rpm.grafana.com
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://rpm.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt

Populated the datasource ELK and MYSQL 

![grfana datasource](https://github.com/kiranchavala/logstash-cloudstack/assets/1401014/dd0a6161-c47f-4fa4-8a72-0aea9ca10894)


![grfana datasource2](https://github.com/kiranchavala/logstash-cloudstack/assets/1401014/7c2cb286-9746-48a5-8844-690eaaeca790)


Dashboard variables 

![Dashboard variables](https://github.com/kiranchavala/logstash-cloudstack/assets/1401014/fe82ecde-c4e6-47b2-8043-f4bdf5809916)


Sample Dashboard


![Sample Dashboard](https://github.com/kiranchavala/logstash-cloudstack/assets/1401014/b719486c-9fa6-4f57-9290-bf48572065cd)





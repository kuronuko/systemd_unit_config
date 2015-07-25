MHA for MySQL5.5 Systemd用のUnit設定ファイル
================

## Requires

* MySQL5.5

## Build and Run

### Step1.git clone

```
git clone https://github.com/kuronuko/systemd_unit_config.git 
cd systemd_unit_config-master
sudo mv /etc/init.d/mysql /var/tmp/
sudo mv mysql/mysql.service /usr/lib/systemd/system/
sudo mv mha/mysql-mha.service /usr/lib/systemd/system/
sudo chown root:root /usr/lib/systemd/system/mysql.service
sudo chown root:root /usr/lib/systemd/system/mysql-mha.service
```

### Step2.Reflection

```
sudo systemctl daemon-reload
```

### Step3.Service start

```
sudo systemctl start mysql
sudo systemctl start mysql-mha
```

### Step4.Check

```
sudo systemctl status [Unit.service]
```

以下メッセージが出力されていればOK
```
#  masterha_check_status --conf=/etc/mha.cnf
mha (pid:335) is running(0:PING_OK), master:10.64.4.164
```

### Option

* Log check

以下メッセージが出力されていればOK
```
#  sudo journalctl -u mysql-mha | tail
Tue Jul 21 08:38:54 2015 - [info] Ping(SELECT) succeeded, waiting until MySQL doesn't respond..
```

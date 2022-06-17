# Airflow Multipass

This runs airflow 2.3.0 on one multipass vm

## Deploy a Node

Deploy a ubuntu 20.04 multipass vm:

```bash
multipass launch \
  --name airflow \
  --cpus 4 \
  --mem 4096M \
  --disk 12G \
  --cloud-init $PWD/cloud-init.yml \
  focal
```

Get the vm ip:

```bash
multipass list
```

## Initial Setup:

SSH to the node, then switch to the airflow user and run the initial script:

```bash
$ sudo su - airflow
$ ./initial_setup.sh
```

*Optional*: If you instead want to run the commands from the script manually as the airflow user:

```bash
airflow db init
airflow db upgrade
airflow users create --username admin --firstname airflow --lastname admin --email admin@localhost --role Admin --password password
```

Exit as the airflow user and start the airflow services:

```bash
$ exit
$ sudo systemctl restart airflow-webserver && journalctl -fu airflow-webserver
$ sudo systemctl restart airflow-scheduler && journalctl -fu airflow-scheduler
$ sudo systemctl restart airflow-worker && journalctl -fu airflow-worker
```

## Access Airflow

Airflow should be available on port ip, to get the ip:

```
multipass info airflow --format json | jq -r '.info.airflow.ipv4'
```

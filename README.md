# Data Aggregator

## Install

### gcloud

[gcloud sdk install documentaion](https://cloud.google.com/sdk/docs/install)

```
sudo apt update
sudo apt install -y curl apt-transport-https ca-certificates gnupg

echo "deb [signed-by=/usr/share/keyrings/cloud.google.gpg] https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key --keyring /usr/share/keyrings/cloud.google.gpg add -

sudo apt update
sudo apt install -y google-cloud-sdk
```

### dataggr


```shell
sudo apt install -y jq

git clone https://github.com/akiirobot/dataggr.git
cd dataggr

sudo install dataggr /usr/local/bin/
cp bigqueryrc.example $HOME/.bigqueryrc
```

You need to create a BigQuery dataset in [gcp bigquery console](https://console.cloud.google.com/bigquery).
Replcae **<your_project_id>**, **<your_dataset_id>**, and **<your_location>** with your BigQuery settings in **$HOME/.bigqueryrc** file.

## Credential

Create a service account in this [page](https://console.cloud.google.com/iam-admin/serviceaccounts) with following permissions

- BigQuery Data Owner
- BigQuery Job User
- BigQuery User

More [bigquery access-controls list](https://cloud.google.com/bigquery/docs/access-control?hl=zh-tw)

Create a json format credential file **bigquery-upload.json**. And apply the credential

```shell
gcloud auth activate-service-account --key-file=/home/akiicat/bigquery-upload.json
gcloud config set account bigquery-upload@<project_id>.iam.gserviceaccount.com
gcloud auth list
```

## Usage

```shell
tail -f -n 0 tmp.log | dataggr test
```


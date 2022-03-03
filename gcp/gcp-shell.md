## GCP dataproc create cluster ##

```shell
gcloud dataproc clusters create css-test-chenchen --enable-component-gateway --region us-east4 \
--subnet projects/infra-258014/regions/us-east4/subnetworks/sn-qe-private0-gen-zz-00 --zone us-east4-c \
--master-machine-type n1-standard-4 --master-boot-disk-size 500 --num-workers 10 --worker-machine-type n1-standard-4 \
--worker-boot-disk-size 500 --image-version 1.4-debian10 --project mds-dev-84ec
```

## GCP dataproc submit job ##

```shell
gcloud dataproc jobs submit spark \
    --cluster=css-test-chenchen \
    --class=com.conviva.platform.datafeeds.d3ssmerge.CSSMergeLauncher \
    --jars=gs://conviva-mds-dev/chenchen/jars/d3-Session-Summary-Merge-job-2.208.0.35935-all.jar \
    --region=us-east4 \
    -- --startTimeSec=1646002500 --endTimeSec=1646088900 --inputPath=gs://conviva-mds-dev/chenchen/css_hourly/2022-02-28/ --customerId=-1 --outPutPath=gs://conviva-mds-dev/chenchen/css_merge/2022-02-28
```

## GCP copy cloud storage ##

```shell
gsutil cp -r  gs://databricks-user-share/chenchen/output/2022-02-28/data=contentSessionSummary/interval=3600/delay=300/* gs://conviva-mds-dev/chenchen/css_hourly/2022-02-28/
```

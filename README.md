## Pre-requisites:
A working Bosh environment with UAA

## Step 0:
It is recommended to create a bosh UAA account (bosh_exporter) with "refresh_token" enabled:
```
    client_id: bosh_exporter
    authorized-grant-types: client_credentials,refresh_token
    authorities: bosh.read
    scope: bosh.read
```
While this step is optional, and you could use the bosh director login credential to test out the deployment, the deployment may stop working once the director uaa token expired. 
## Step 1:
Run ```./create-exporter-uaa.sh``` to add the UAA clients for cf and firehose exporters.
## Step 2:
Run ```./init-config.sh``` to create the "prometheus-params.yml" file and the "prometheus-exporter-ops.yml" file.
## Step 3:
Update the generated "prometheus-params.yml" file for any additional parameters, such as bosh connection info, etc.  A sample file "sample-prometheus-params.yml" is also provided.  There is no need to change the "prometheus-exporter-ops.yml" file.
## Step 4:
Login bosh and run ```./prometheus.sh``` to kick off the deployment of the prometheus monitoring stack. If needed, update the ops file as for a typical bosh deployment

## If you need to add additional PCF environments to an existing prometheus monitoring
1. Run ```./create-exporter-uaa.sh``` to add the UAA clients for cf and firehose exporters.
2. Run ```./add-pcf.sh``` to add more PCF foundations to the monitoring. This script will append to the existing "prometheus-exporter-ops.yml" and "prometheus-params.yml" files.
3. Updated the "prometheus-params.yml" file for any additional required parameters.
4. Login bosh and run ```./prometheus.sh```

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
Run ```./create-exporter-uaa.sh``` to add the UAA clients for cf and firehose exporters
## Step 2:
Run ```./init.sh``` to create the skeleton of the parameter file and the exporter ops file
## Step 3:
Update the "prometheus-params.yml" file for any additional parameters, such as bosh connection info, etc.
## Step 4:
Login bosh and run ```./prometheus.sh``` to kick off the deployment of the prometheus monitoring stack.

## Optional: Add more PCF environments to the monitoring stack:
Run ```./add-pcf.sh``` to add more PCF foundations to the monitoring
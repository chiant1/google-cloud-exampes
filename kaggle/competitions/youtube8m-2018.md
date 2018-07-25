# Model

## Environments
- MACHINE - name of VM instance in Google Compute Engine

## Start compute engine node with GPU
~~~~
gcloud beta compute --project=${PROJECT} instances create ${MACHINE} \
  --zone=us-central1-a --machine-type=n1-standard-8 \
  --subnet=default --network-tier=PREMIUM --maintenance-policy=TERMINATE \
  --service-account=${SERVICE_ACCOUNT} \
  --scopes=https://www.googleapis.com/auth/cloud-platform \
  --accelerator=type=nvidia-tesla-k80,count=1 \
  --image=debian-9-stretch-v20180716 --image-project=debian-cloud \
  --boot-disk-size=20GB --boot-disk-type=pd-standard --boot-disk-device-name=instance-1
~~~~

## Start datalab with GPU
~~~~
datalab beta create-gpu ${MACHINE} --zone us-central1-a
~~~~

## Cancel ML-job
~~~~
gcloud beta ml-engine jobs list
gcloud ml-engine jobs cancel job
~~~~

# References
- [Starter code](https://github.com/google/youtube-8m)
- [Winner solution 2017](https://github.com/antoine77340/Youtube-8M-WILLOW)

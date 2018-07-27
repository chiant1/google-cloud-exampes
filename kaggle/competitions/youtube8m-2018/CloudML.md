### Working VM

~~~~
gcloud beta compute --project=${GOOGLE_CLOUD_PROJECT} instances create ${MACHINE} \
  --zone=us-central1-a --machine-type=n1-standard-4 \
  --subnet=default --network-tier=PREMIUM --maintenance-policy=TERMINATE \
  --service-account=${SERVICE_ACCOUNT} \
  --scopes=https://www.googleapis.com/auth/cloud-platform \
  --image=debian-9-stretch-v20180716 --image-project=debian-cloud \
  --boot-disk-size=10GB --boot-disk-type=pd-ssd --boot-disk-device-name=${MACHINE}
~~~~

### List Jobs
~~~~
gcloud ml-engine jobs list
~~~~

### Cancel Job
~~~~
gcloud ml-engine jobs cancel ${JOB_NAME}
~~~~


### Pricing
- [Pricing](https://cloud.google.com/ml-engine/docs/pricing#ml-units)
- [Using GPUs for Training Models in the Cloud](https://cloud.google.com/ml-engine/docs/tensorflow/using-gpus)


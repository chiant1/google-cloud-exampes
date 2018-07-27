# Model

## Environments
~~~~
GOOGLE_CLOUD_PROJECT - ...
MACHINE - name of VM instance in Google Compute Engine
SERVICE_ACCOUNT - ...
~~~~

## Start compute engine node
~~~~
# With GPU
gcloud beta compute --project=${GOOGLE_CLOUD_PROJECT} instances create ${MACHINE} \
  --zone=us-central1-a --machine-type=n1-standard-8 \
  --subnet=default --network-tier=PREMIUM --maintenance-policy=TERMINATE \
  --service-account=${SERVICE_ACCOUNT} \
  --scopes=https://www.googleapis.com/auth/cloud-platform \
  --accelerator=type=nvidia-tesla-k80,count=1 \
  --image=debian-9-stretch-v20180716 --image-project=debian-cloud \
  --boot-disk-size=20GB --boot-disk-type=pd-standard --boot-disk-device-name=${MACHINE}

# HDD small drive
gcloud beta compute --project=${GOOGLE_CLOUD_PROJECT} instances create ${MACHINE} \
  --zone=us-central1-a --machine-type=n1-standard-8 \
  --subnet=default --network-tier=PREMIUM --maintenance-policy=TERMINATE \
  --service-account=${SERVICE_ACCOUNT} \
  --scopes=https://www.googleapis.com/auth/cloud-platform \
  --image=debian-9-stretch-v20180716 --image-project=debian-cloud \
  --boot-disk-size=20GB --boot-disk-type=pd-standard --boot-disk-device-name=${MACHINE}

# SSD small drive
gcloud beta compute --project=${GOOGLE_CLOUD_PROJECT} instances create ${MACHINE} \
  --zone=us-central1-a --machine-type=n1-standard-8 \
  --subnet=default --network-tier=PREMIUM --maintenance-policy=TERMINATE \
  --service-account=${SERVICE_ACCOUNT} \
  --scopes=https://www.googleapis.com/auth/cloud-platform \
  --image=debian-9-stretch-v20180716 --image-project=debian-cloud \
  --boot-disk-size=100GB --boot-disk-type=pd-ssd --boot-disk-device-name=${MACHINE}


# SSD big drive
gcloud beta compute --project=${GOOGLE_CLOUD_PROJECT} instances create ${MACHINE} \
  --zone=us-central1-a --machine-type=n1-standard-8 \
  --subnet=default --network-tier=PREMIUM --maintenance-policy=TERMINATE \
  --service-account=${SERVICE_ACCOUNT} \
  --scopes=https://www.googleapis.com/auth/cloud-platform \
  --image=debian-9-stretch-v20180716 --image-project=debian-cloud \
  --boot-disk-size=1000GB --boot-disk-type=pd-ssd --boot-disk-device-name=${MACHINE}

 gcloud compute instances list
 
 gcloud compute instances delete ${MACHINE} --zone us-central1-a --delete-disks=all
~~~~

## Clone sources
~~~~
sudo apt-get install -y git
gcloud config list
git config --global user.email ${USER}@${HOST}
git config --global user.name ${USER}@${HOST}
gcloud source repos clone datalab-notebooks
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
  * [Pulls](https://github.com/google/youtube-8m/pulls)
- [Winner solution 2017](https://github.com/antoine77340/Youtube-8M-WILLOW)

# Papers
- [Video Representation Learning and Latent Concept Mining for Large-scale
Multi-label Video Classification](https://arxiv.org/pdf/1707.01408.pdf)
- https://arxiv.org/pdf/1706.04488

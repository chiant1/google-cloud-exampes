# Create compute instance
~~~~
gcloud beta compute instances create test-1 \
  --zone=us-central1-a --machine-type=n1-highcpu-2 \
  --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE \
  --service-account=${SERVICE_ACCOUNT} \
  --scopes=https://www.googleapis.com/auth/cloud-platform \
  --image=debian-9-stretch-v20180806 \
  --image-project=debian-cloud \
  --boot-disk-size=30GB --boot-disk-type=pd-standard --boot-disk-device-name=test-1 \
  --metadata=startup-script=gs://achikin/datalab-notebooks/trackml/dataproc/init-hyperopt.sh
  
gcloud beta compute instances create hyperopt-1 \
  --zone=us-central1-a --machine-type=n1-highcpu-32 \
  --subnet=default --network-tier=PREMIUM --maintenance-policy=MIGRATE \
  --service-account=${SERVICE_ACCOUNT} \
  --scopes=https://www.googleapis.com/auth/cloud-platform \
  --image=debian-9-stretch-v20180806 \
  --image-project=debian-cloud \
  --boot-disk-size=30GB --boot-disk-type=pd-standard --boot-disk-device-name=hyperopt-1 \
  --metadata=startup-script=gs://achikin/datalab-notebooks/trackml/dataproc/init-hyperopt.sh
~~~~

# Create compute instance
~~~~
gcloud compute instances delete hyperopt-1 --zone us-central1-a --delete-disks=all
~~~~

# Create a dataproc cluster
~~~~

# 1. Single-Node Cluster 
gcloud dataproc --region us-central1 clusters create ${CLUSTER} \
  --subnet default --zone us-central1-a \
  --single-node --master-machine-type n1-standard-1 \
  --master-boot-disk-size 20 --image-version 1.2 \
  --scopes 'https://www.googleapis.com/auth/cloud-platform' \
  --project ${GOOGLE_CLOUD_PROJECT} \
  --initialization-actions "gs://${BUCKET}/datalab-notebooks/trackml/dataproc/init.sh"

# 2. Small Cluster 
gcloud dataproc --region us-central1 clusters create ${CLUSTER} \
  --subnet default --zone us-central1-a \
  --master-machine-type n1-standard-1 --master-boot-disk-size 20 \
  --num-workers 2 \
  --worker-machine-type n1-highcpu-4 --worker-boot-disk-size 20 \
  --image-version 1.2 \
  --scopes 'https://www.googleapis.com/auth/cloud-platform' \
  --project ${GOOGLE_CLOUD_PROJECT} \
  --initialization-actions "gs://${BUCKET}/datalab-notebooks/trackml/dataproc/init.sh"
  
# 3. Standard Cluster 
gcloud dataproc --region us-central1 clusters create ${CLUSTER} \
  --subnet default --zone us-central1-a \
  --master-machine-type n1-standard-1 --master-boot-disk-size 20 \
  --num-workers 2 \
  --num-preemptible-workers 3 \
  --worker-machine-type n1-highcpu-4 --worker-boot-disk-size 20 \
  --image-version 1.2 \
  --scopes 'https://www.googleapis.com/auth/cloud-platform' \
  --project ${GOOGLE_CLOUD_PROJECT} \
  --initialization-actions "gs://${BUCKET}/datalab-notebooks/trackml/dataproc/init.sh"

# 3. List Cloud Engine instances
gcloud compute instances list
~~~~

# Clone sources

~~~~
gcloud config list
git config --global user.email ${USER}@${HOST}
git config --global user.name ${USER}@${HOST}
gcloud source repos clone datalab-notebooks
~~~~

# Submit job to dataproc cluster

~~~~
# 1. Test
spark-submit pyspark-trackml.py 10

# 2. Submit job
gcloud dataproc jobs submit pyspark \
  "gs://${BUCKET}/datalab-notebooks/trackml/pyspark/pyspark-trackml.py" \
  --cluster=${CLUSTER} --async --region=us-central1 \
  -- \
  10

# 3. Submit job to generate full submission
gcloud dataproc jobs submit pyspark \
  "gs://${BUCKET}/datalab-notebooks/trackml/pyspark/pyspark-trackml-submission1.py" \
  --cluster=${CLUSTER} --async --region=us-central1 \
  -- \
  --step 1 --repeat 10
  
~~~~
[Documentation: gcloud dataproc jobs submit pyspark](https://cloud.google.com/sdk/gcloud/reference/dataproc/jobs/submit/pyspark)

# Delete dataproc cluster
~~~~
gcloud dataproc clusters delete ${CLUSTER} --async --quiet --region=us-central1
~~~~


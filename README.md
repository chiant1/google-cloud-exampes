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

# 2. Standard Cluster 
gcloud dataproc --region us-central1 clusters create ${CLUSTER} \
  --subnet default --zone us-central1-a \
  --master-machine-type n1-standard-1 --master-boot-disk-size 20 \
  --num-workers 2 \
  --worker-machine-type n1-standard-8 --worker-boot-disk-size 20 \
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
git config --global user.name ${USER}
gcloud source repos clone datalab-notebooks
~~~~

# Delete dataproc cluster
~~~~
gcloud dataproc clusters delete ${CLUSTER} --async --quiet --region=us-central1
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
  
~~~~
[Documentation: gcloud dataproc jobs submit pyspark](https://cloud.google.com/sdk/gcloud/reference/dataproc/jobs/submit/pyspark)

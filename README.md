# Create a dataproc cluster
~~~~
gcloud dataproc --region us-central1 clusters create <CLUSTER> \
  --subnet default --zone us-central1-a \
  --single-node --master-machine-type n1-standard-1 \
  --master-boot-disk-size 20 --image-version 1.2 \
  --scopes 'https://www.googleapis.com/auth/cloud-platform' \
  --project <PROJECT> \
  --initialization-actions 'gs://<BUCKET>/datalab-notebooks/trackml/dataproc/init.sh'
  
gcloud compute instances list
~~~~

# Clone sources

# Delete dataproc cluster
~~~~
gcloud dataproc clusters delete <CLUSTER> --async --quiet --region=us-central1
~~~~

# Submit job to dataproc cluster
~~~~
gcloud dataproc jobs submit pyspark "gs://<BUCKET>/datalab-notebooks/trackml/pyspark/pyspark-trackml.py" \
  --cluster=<CLUSTER> --async --region=us-central1
~~~~

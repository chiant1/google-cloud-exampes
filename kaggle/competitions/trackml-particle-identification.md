
# Start datalab without GPU

~~~~
datalab create trackml --machine-type n1-standard-2 --zone us-central1-a
~~~~

# Start datalab with GPU
~~~~
datalab beta create-gpu datalab-instance-name
~~~~

# 2. Connect to datalab
~~~~
datalab connect --zone us-central1-a --port 8081 trackml2
~~~~

# 3. Delete instance and all disks
~~~~
gcloud compute instances delete trackml --zone us-central1-a --delete-disks=all
~~~~

# 4. List instances and disks
~~~~
gcloud compute instances list
gcloud compute disks list
~~~~

# Model

## Environments
- MACHINE - name of VM instance in Google Compute Engine

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

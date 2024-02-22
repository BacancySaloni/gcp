To install Google cloud sdk , follow below commands in ubuntu.

https://cloud.google.com/sdk/docs/install#versioned


curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-464.0.0-linux-x86_64.tar.gz
tar -xf google-cloud-cli-464.0.0-linux-x86_64.tar.gz
./google-cloud-sdk/install.sh
source ~/.bashrc

For installing kubectl plugin in GKE, we will need below things:
sudo apt-get install google-cloud-sdk-gke-gcloud-auth-plugin
gcloud components update
gcloud components install kubectl


For authentication , we will need this command
gcloud auth login
this will open web browser to login, we need to pass creds for gcp.

- gcloud config set project PROJECT_ID
gcloud config set project automation-avengers

gcloud container clusters create-auto hello-cluster --location=us-central1

gcloud container clusters get-credentials hello-cluster --location us-central1

create the deployment:
kubectl create deployment hello-server \
    --image=us-docker.pkg.dev/google-samples/containers/gke/hello-app:1.0

kubectl expose deployment hello-server \
    --type LoadBalancer \
    --port 80 \
    --target-port 8080

kubectl get pods
kubectl get service hello-server
http://EXTERNAL_IP

Clean Up:
kubectl delete service hello-server
gcloud container clusters delete hello-cluster \
    --location us-central1


For standard cluster : 
gcloud container clusters create \
--machine-type n1-standard-2 \
--num-nodes 3\
--zone zone \
--cluster-version latest \
<CLUSTERNAME>


Configuring Kubernetes with Kind and Kubectl
Installing Kind
Kind (Kubernetes in Docker) is a tool that allows you to run Kubernetes clusters locally using Docker.
1.	First, you need to have Docker installed. If you don't have it yet, you can download it here.
2.	Next, you can install Kind. The easiest way to do this is to download the installation script and run it with the following command:
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.11.1/kind-linux-amd64
chmod +x ./kind
mv ./kind /some-dir-in-your-PATH/kind

Installing Kubectl
Kubectl is the Kubernetes command-line tool. You can install it using the following command:
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
chmod +x ./kubectl
mv ./kubectl /some-dir-in-your-PATH/kubectl
Creating a Kubernetes Cluster
After installing Kind and Kubectl, you can create a Kubernetes cluster. Here is an example of a configuration file for a cluster with four nodes:
kind: Cluster                   # Indicates that we are creating a Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane           # Sets the first node as the control node
- role: worker                  # Sets the second node as a worker node
- role: worker                  # Sets the third node as a worker node
- role: worker                  # Sets the fourth node as a worker node
You can create a cluster with this configuration using the following command:
kind create cluster --config config.yaml
Creating a Pod
To create a Pod in Kubernetes, you can use a YAML manifest file. Here is an example of a manifest file for a Pod that runs an Nginx container:
apiVersion: v1                  # Version of the Kubernetes API we are using
kind: Pod                       # Indicates that we are creating a Pod
metadata:
  labels:
    run: nginx-giropops         # Label to identify the Pod
    app: giropops-strigus       # Another label to identify the Pod
  name: nginx-giropops          # Name of the Pod
spec:
  containers:
  - image: nginx                # Container image that the Pod will run
    name: nginx-giropops        # Name of the container
    ports:
    - containerPort: 80         # Port that the container is listening on
    resources: 
      limits: 
        memory: "4400Mi"        # Memory limit for the container
        cpu: "0.5"              # CPU limit for the container
      requests:
        memory: "4400Mi"        # Amount of memory requested for the container
        cpu: "0.3"              # Amount of CPU requested for the container
  dnsPolicy: ClusterFirst       # DNS policy for the Pod
  restartPolicy: Always         # Restart policy for the Pod

To create the Pod, use the command kubectl apply -f <file.yaml>.



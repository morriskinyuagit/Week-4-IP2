# Choice of the Kubernetes Objects used for deployment
 - Scalability to determine if I will use deployment or statefulset
 - Availability
 - Complexity
 # Method used to expose your pods to internet traffic.
    ClusterIp - For my IP, I used ClusterIP to expose my pods to the traffic. This means I just wanted them to communicate within the cluster, privately.

   - Other methods may include
     LoadBalancer: This Service type creates a load balancer that distributes traffic to the Pods in the Service. The load 
                 balancer can be exposed to the Internet, making the Service accessible from outside the cluster. LoadBalancer Services are typically used for exposing applications to the public.

      NodePort:    This Service type exposes the Service on a specific port on each node in the cluster. The Service can 
                 be accessed from outside the cluster by connecting to the NodePort on any node. NodePort Services are typically used for developing and testing applications, or for exposing applications to a specific audience. 
                  
# Use-of or there-lack-of of persistent storage.
- Persistent storage is a storage type that is not local to a Pod and that can be accessed and modified by multiple Pods. This is in contrast to ephemeral storage, which is local to a Pod and is deleted when the Pod is terminated.

- Persistent storage is typically used to store data that needs to be preserved across Pod restarts and failures. For example, you might use persistent storage to store database data, file server data, or application configuration.

- In my project I did not use persistent storage because I did not provision PVC and mount it to my Pod using a VolumeMount.

# Good practices such as Docker image tag naming standards for ease of identification and personalization of images and containers.
- Use a consistent naming convention - This will make it easier to identify and personalize your images and containers.
- Use short, descriptive names - This will make it easier to read and understand your image tags.
- Use semantic versioning - This will help you to track changes to your images and to communicate the compatibility of your images with each other.
- Use prefixes to identify different types of images - For example, you could use the prefixes dev-, staging-, and prod- to identify images for development, staging, and production environments.
- Use suffixes to indicate the build date or commit hash - This will help you to track down the source code for a particular image.

# Other details of how I achieved the IP
 1. Created manifests files
 2. Created a cluster in my GKE
 3. kubectl apply -f manifests
 4. kubectl get service
 5. kubectl get all
 6. kubectl get pods
 7. I went back to my GKE and created a Deployment.

 # IP address 
  - client cluster ip  http://10.33.254.174
  - port 80/TCP

 # Git workflow
  - git add .
  - git commit -m "message"
  - git push origin master


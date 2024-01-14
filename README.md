# Simple-Nginx-Deployment-with-Kubernetes

This project demonstrates a basic Nginx deployment on a Kubernetes cluster, covering Docker image creation, Kubernetes configuration, and networking concepts.

## Project Structure

  - Dockerfile: Contains instructions to build the Nginx Docker image.
  - myweb.yaml: Kubernetes configuration file defining the deployment and service.
  - README.md: This file (you're reading it now!).

## Setup Instructions

1.  Prerequisites:

  - Docker installed and running.
  - Access to a Kubernetes cluster (local or cloud-based).
  - kubectl command-line tool configured for your cluster.

2.  Build the Docker Image:

```<bash>

docker build -t aymenzarour/webapp:latest .

```

3.  Push the Image to Docker Hub:

```<bash>

docker push aymenzarour/webapp:latest

```

4.  Deploy to Kubernetes:

```<bash>

kubectl apply -f myweb.yaml

```

5.  Access the Application:

  - Using NodePort:
    ```<bash>

    kubectl get services
    # Get the NodePort (e.g., 30011) and any node's IP address
    curl <node-ip>:<node-port>
    
    ```
  - Using LoadBalancer:
    ```<bash>

    kubectl get services
    # Wait for the external IP to be assigned
    curl <external-ip>
    
    ```

    -  on my case :
      ```<bash>
      
      $ kubectl get services
      NAME            TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
      kubernetes      ClusterIP      10.43.0.1      <none>        443/TCP        42h
      nginx-service   LoadBalancer   10.43.229.89   <pending>     80:30011/TCP   62m

       ```

      access using the loadbalancer service, IP 192.168.43.95:30011

## Networking in Kubernetes

  - Pods: Have their own IP addresses within the cluster's internal network.
  - Services: Abstract ways to expose pods to external traffic.
    - NodePort: Exposes a service on a static port on each node.
    - LoadBalancer: Creates an external load balancer to distribute traffic across pods.

## Additional Notes

  - Replace aymenzarour/webapp:latest with your Docker image name if you pushed it to a different registry.
  - Adapt instructions based on your specific Kubernetes environment and provider.


      


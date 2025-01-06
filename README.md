# How to Create an Identical Deployment  Canary CKAD

The phrase create an identical deployment canary CKAD refers to the task of setting up a canary deployment in Kubernetes, as part of the Certified Kubernetes Application Developer (CKAD) exam. This involves creating a deployment that mirrors an existing deployment, but with a controlled, gradual rollout of changes to a subset of users (a "canary"), so that you can monitor the effects before fully rolling out the changes.

## Breaking Identical Deployment Canary

1. **Canary Deployment**: 
   A **canary deployment** is a strategy used to reduce risk when releasing a new version of an application. Instead of rolling out the new version to all users at once, a small percentage (the "canaries") of traffic is directed to the new version. If the new version performs well, the deployment is gradually increased to the rest of the users. This allows you to detect potential issues before they affect everyone.

2. **Identical Deployment**: 
   The **"identical deployment"** part refers to creating a new Kubernetes deployment that is exactly the same as an existing one but configured to behave like a canary. This usually involves deploying the same application but with slight variations, such as a different replica count or selector to ensure it’s only partially rolled out.

3. **CKAD (Certified Kubernetes Application Developer)**: 
   The **CKAD** exam tests your ability to work with Kubernetes as a developer. In this context, you might be asked to [create an identical deployment canary ckad](https://www.certshero.com/linux-foundation/ckad/practice-test) during the exam to demonstrate your skills in rolling out new features or versions of applications in a controlled, safe way using Kubernetes.

### Example of Creating a Canary Deployment:
Let's say you have an existing deployment and you want to create a canary deployment that mirrors it, but with a smaller number of replicas. You might start with a canary deployment that only receives a small fraction of the traffic to ensure its stability.

Here's an example manifest of how to create an identical **canary deployment**:

#### Existing Deployment (Example):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 5
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app-container
        image: my-app-image:v1
        ports:
        - containerPort: 80
```

#### Canary Deployment:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app-canary
spec:
  replicas: 1  # Fewer replicas for the canary deployment
  selector:
    matchLabels:
      app: my-app
      version: canary
  template:
    metadata:
      labels:
        app: my-app
        version: canary
    spec:
      containers:
      - name: my-app-container
        image: my-app-image:v2  # The new version of the app
        ports:
        - containerPort: 80`
```

### Key Points:
- The **canary deployment** uses the same `app: my-app` label but is differentiated by an additional label (e.g., `version: canary`).
- The **replica count** for the canary deployment is typically set to a small number (e.g., 1 or 2) to limit the exposure of the new version.
- The **image** for the canary deployment could point to a newer version of the application (e.g., `my-app-image:v2`), whereas the original deployment continues to use the stable version (`v1`).
- Once the canary deployment is stable and verified, you can increase its replica count and gradually shift more traffic to it.

### Relevance to CKAD:
As part of the **CKAD exam**, you might be required to demonstrate your knowledge of deployment strategies, including canary deployments. You could be tasked with creating or managing a deployment that mimics another, ensuring smooth updates or rollouts of new versions with minimal risk.

By practicing with tools like **kubectl** and **Helm**, and understanding deployment strategies, you'll be well-prepared for scenarios involving **canary deployments** during the CKAD exam.

### Summary

[Identical deployment canary CKAD](https://www.certshero.com/linux-foundation/ckad) refers to the task of replicating an existing deployment in a Kubernetes cluster but with modifications to create a canary version, which helps in controlling and monitoring the release of new application versions during the exam scenario.

# Practical 5 — Kubernetes: Deploy, Expose and Scale

**Aim:** To deploy, expose and scale an application on a Kubernetes cluster.

**Prerequisite:** A cluster. Pick one option.

---

## Option A — Killercoda (browser only, no installation)

1. Open https://killercoda.com and log in (GitHub login works).
2. **Playgrounds** → **Kubernetes** (1-node) → **Start**.
3. A browser terminal opens with the cluster already running.
4. **Skip** `minikube start` and go to the commands below.

## Option B — Minikube locally

```bash
minikube start --driver=docker
kubectl get nodes
```

If `minikube` is missing, install it from https://minikube.sigs.k8s.io/docs/start/.

## Deploy and verify

```bash
kubectl get nodes
kubectl create deployment nginx --image=nginx
kubectl get deployments
kubectl get pods
```

Wait until the pod shows `Running`.

## Expose the deployment

```bash
kubectl expose deployment nginx --type=NodePort --port=80
kubectl get svc
```

Note the port mapping, e.g. `80:31234`.

- Killercoda: `curl localhost:<NodePort>`
- Minikube: `minikube service nginx` (opens the browser automatically)

You should see **Welcome to nginx!**

## Scale and inspect

```bash
kubectl scale deployment nginx --replicas=3
kubectl get pods
kubectl describe deployment nginx
```

Three pods should be `Running`.

## Clean up

```bash
kubectl delete service nginx
kubectl delete deployment nginx
```

## What to verify / screenshot

- [ ] `kubectl get nodes` → node `Ready`
- [ ] Deployment created and pod `Running`
- [ ] Service with a NodePort
- [ ] `curl` output: `Welcome to nginx!`
- [ ] Three pods `Running` after scaling

## Troubleshooting

| Problem | Fix |
|---|---|
| `kubectl: command not found` | Use Killercoda, or install kubectl + minikube |
| Pod stuck in `ImagePullBackOff` | Check internet/proxy; retry `kubectl describe pod` |
| `curl: connection refused` | Use the exact NodePort from `kubectl get svc` |
| NodePort not reachable on Minikube | `minikube service nginx` instead of curl |
| Pod still `ContainerCreating` | Wait 30–60 seconds, then `kubectl get pods` again |

## Viva

- **Pod vs Deployment?** A pod is the smallest runnable unit; a deployment manages pods, replicas and updates.
- **What is a Service?** A stable network endpoint that exposes pods.
- **What is NodePort?** A service type that opens a port on every node so the app is reachable externally.
- **How do you scale?** `kubectl scale deployment <name> --replicas=N`.
- **What does Kubernetes do?** Orchestrates containers: scheduling, scaling, self-healing and networking.

**Result:** nginx was deployed, exposed with a NodePort service, verified in the
browser/curl, scaled to three replicas and cleaned up.

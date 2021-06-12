Kubernetes is a portable, extensible, open-source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.


The name Kubernetes originates from Greek, meaning helmsman or pilot. Google open-sourced the Kubernetes project in 2014. Kubernetes builds upon a decade and a half of experience that Google has with running production workloads at scale, combined with best-of-breed ideas and practices from the community.

Generating Pod Manifests via CLI
1. Create a Pod from Nginx Image



kubectl run [NAME-OF-POD] --image=[IMAGE=NAME] --restart=Never



kubectl run nginx --image=nginx --restart=Never


2. Create a Pod and Expose a Port
kubectl run nginx --image=nginx --port=80 --restart=Never

3. Output the Manifest File
kubectl run nginx --image=nginx --port=80 --restart=Never --dry-run -o yaml

This will eventually become a blog post on the Eficode blog.

---

# KubeCon Europe 2022: Takeaways and Trends

I had the privilege of attending KubeCon / CloudNativeCon Europe 2022 in Valencia, as well GitOpsCon, one of the co-located events.
In this blog post I will my takeaways from both conventions, as well as point out trends, as I see them, in the Cloud Native community.
These will be presented as topics, and will include any relevant links, as well as references to talks from KubeCon, so you can watch them for yourself.

## Kubernetes is a Generic Cloud Native Control Plane:

Kubernetes is an awesome container orchestrator, but it turns out that the Kubernetes control plane can be used for much more than running containers in clusters!
Kubernetes works on objects using the Kubernetes Resource Model (KRM), this is what enables Kubernetes to continuously reconciliate the desired state the objects (resources) that are desired.

From the Kubernetes [documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/):

> "A Kubernetes object is a "record of intent" -- once you create the object, the Kubernetes system will constantly work to ensure that object exists. By creating an object, you're effectively telling the Kubernetes system what you want your cluster's workload to look like; this is your cluster's desired state."

The KRM is generic, which means that by utilizing Custom Resource Definitions (CRDs) we can actually utilize the Kubernetes control plane to control other things than the standard set of Kubernetes resources (pods, deployments, services, etc.).
This means that we can use the same underlying control plane to control any number of interesting things, using the same reconciliating loop, such as: helm charts, external cloud resources like s3 buckets and databases, and even other Kubernetes clusters!
These resources are then managed by a "control cluster", a Kubernetes cluster with the responsibility of controlling other resources, and not running the actual workloads.

There are a number of new technologies that leverage this idea of Kubernetes as a control plane, but the most exciting of these is [Crossplane](https://crossplane.io/).
Crossplane is a framework for building Cloud Native control planes, without writing custom code.
Crossplane is also a Cloud Native Computing Foundation (CNCF) [incubating project](https://www.cncf.io/projects/crossplane/), developed by [Upbound](https://www.upbound.io/).
Crossplane provides an extensible backend to manage any infrastructure in any environment (as long as it has an API).

Crossplane represents external resources as Kubernetes resources, such that we can represent resources outside of Kubernetes in Kubernetes.
every external resource, for example an AWS s3 bucket or an Azure AKS cluster, is represented by a Kubernetes "kind".
So we can use Crossplane to declare the external resources we need, and use the Crossplane CRDs to utilize the normal Kubernetes control loop to reconcile

<!-- I've been thinking about this without being able to articulate exactly what I was thinking for a while now, but at KubeCon it finally clicked for me: k8s is a control plane, not a container orchestrator! -->
<!-- Or in other words: k8s is great for orchestrating containers, but as k8s has evolved it can help manage so many different kinds of resources today. -->

---

— notes —
Touching on the following topics:
k8s as a generic control-plane
devx / platform engineering / golden paths / paved roads
GitOps
CI/CD Orchestration vs. Choreography
debugging k8s with ephemeral containers
OpenTelemetry
Krew
Talks to watch
Service meshes / linkerd
Chaos testing / engineering
Real traffic testing with pixie/eBPF
eBPF capabilities

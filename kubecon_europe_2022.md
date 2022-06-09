# KubeCon/CloudNativeCon Europe 2022: Takeaways and Trends

I recently had the privilege of attending KubeCon / CloudNativeCon Europe 2022 (from here we'll just call it KubeCon) in Valencia, as well as GitOpsCon, one of the co-located events.

In this blog post I will outline my takeaways and trends that I have seen at the convention, and in the Cloud Native community.
These will be presented as topics, in no particular order, and I will link to relevant talks from KubeCon, so that you can watch them yourself.

## Kubernetes is a (Cloud Native) Control Plane

Kubernetes is an awesome container orchestrator, but it turns out that the Kubernetes control plane can be used for much more than running containers in clusters!
Kubernetes works on objects using the Kubernetes Resource Model (KRM), this is what enables Kubernetes to continuously reconciliate the desired state of the objects (resources) that are desired.

From the [Kubernetes documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/):

> "A Kubernetes object is a "record of intent" -- once you create the object, the Kubernetes system will constantly work to ensure that object exists. By creating an object, you're effectively telling the Kubernetes system what you want your cluster's workload to look like; this is your cluster's desired state."

The KRM is generic, which means that by utilizing Custom Resource Definitions (CRDs) we can actually utilize the Kubernetes control plane to control other things than the standard set of Kubernetes resources (pods, deployments, services, etc.).
This means that we can use the same underlying control plane to control any number of interesting things, using the same reconciliating loop.
This could be managing things running in the cluster, like helm charts, or external cloud resources like S3 buckets or managed databases, even other Kubernetes clusters!
Usually, these resources are then managed by a "control cluster", a Kubernetes cluster with the responsibility of controlling other resources, and not running the actual workloads.

There are a number of new technologies that leverage this idea of Kubernetes as a control plane, but the most exciting of these is [Crossplane](https://crossplane.io/).
Crossplane is a framework for building Cloud Native control planes, without writing custom code.
Crossplane is also a Cloud Native Computing Foundation (CNCF) [incubating project](https://www.cncf.io/projects/crossplane/), developed by [Upbound](https://www.upbound.io/).
Crossplane provides an extensible backend to manage any infrastructure in any environment (as long as it has an API).

Crossplane represents external resources as Kubernetes resources.
Thus Crossplane helps us manage external resources to the cluster, as resources in the cluster.
Each of these external resource, for example an AWS s3 bucket or an Azure AKS cluster, is represented by a Kubernetes "kind".
So we can use Crossplane to declare the external resources we need, and use the Crossplane CRDs to utilize the normal Kubernetes control loop to reconcile the configuration and management of these resources.

A cool usage of Crossplane to control external resources that was showcased at KubeCon, was a [joint presentation](https://kccnceu2022.sched.com/event/ytle/building-digital-twins-for-dfds-with-crossplane-and-kubernetes-tobias-andersen-dfds-matthias-luebken-upbound?iframe=no&w=100%&sidebar=yes&bg=no) from DFDS and Upbound, on how they were representing "Digital Twins" in Kubernetes.
The idea digital twins is to have a digital representation of something physical, essentially a "control plane for the physical world".
In this context, the representations are of shipping logistics and infrastructure: Container Ships, Shipping Terminals, Containers (not software), Trucks, etc.
The "Digital Twin" is thus the aggregated sensor data from these physical things, represented as kinds in Kubernetes.
This leads to some cool interactions like "$ kubectl get ship", to view the coordinated and status of ships in the fleet.

I think we are only starting to see the beginning of what is possible with control planes, and using Kubernetes for others things than orchestrating containers, software or otherwise.

**Talks to watch:**

- Crossplane Intro and Deep Dive: https://www.youtube.com/watch?v=xECc7XlD5kY
- Building Digital Twins for DFDS With Crossplane and Kubernetes: https://www.youtube.com/watch?v=zOWLy-eZQas

## Platform Engineering

Another topic that was talked a lot about at KubeCon is "platform engineering", this was also called: "DevX", "golden paths" and "paved roads", "capability team", we will refer to it as platform engineering (PE).
While there might be slightly different connotations for each of the different names, I think they are all related to the same basic concept.

Essentially the idea of platform engineering is that we want to make it easy for developers to "shift left" in the sense that we make it easy for them to utilize all of the tools and platforms we have available, but without having to be experts of managing the underlying infrastructure.
For example, we want developers to deploy to Kubernetes, but we don't necessarily need all of them to also be experts in Kubernetes administration.
In other words we want to create a good experience for developers or "DevX" (Developer Experience Design).
We do that by treating the platform as the product and the developers as the customers, by making it easy for them to use tools the right way.
We do this by creating friendly interfaces for developers to consume resources, such as cloud databases or Kubernetes deployments.
A friendly interface could be a webportal, where a developer could create an environment, by inputting a few parameters, like the name, resource allocation and how long the environment should exist before being garbage collected.
This is then translated to actual resources by some control plane managed by the Platform Engineering team.

We can think of it as an abstraction similar to how a Kubernetes administrator would create persistent volumes, and then developers would consume those with persistent volume claims.

Thus we get a separation of concerns:

- Operations supplies and manages the foundational infrastructure.
- Platform Engineering Team creates interfaces to make infrastructure easy to consume.
- Developers utilize interfaces created by platform engineering to experiment and create value.

Crossplane is also interesting in the context of platform engineering, as it provides a way of implementing this separation of concerns:
Platform engineering team creates composite resources, and developers consume these by creating claims (instances).

I like this [video](https://www.youtube.com/watch?v=CxJauwazTmY) by Viktor Farcic (Developer Advocate for Upbound), in which he explains control planes and Crossplane, by an example of a Platform Engineering team creating a composite cloud database resource, and developers then consuming it.

**Talks to watch:**

- From Kubernetes to PaaS to … Err, What’s Next? : https://www.youtube.com/watch?v=btUYeOa7JPI
- From Cloud Naive to Cloud Native – Avoiding Mistakes Everyone Does : https://www.youtube.com/watch?v=EhBJkbo0rIE

## GitOps(Con)

GitOps is a dogmatic approach to managing applications and infrastructure, where the desired state is kept in a git repository.
A control plane will then monitor the git repository for changes, and continuously reconcile "the real world" with the desired state.
This brings a number of benefits to managing applications and infrastructure , like a well-known workflow (same as for source code) and an audit trail of changes in the git log.

The main takeaway from GitOpsCon is that GitOps is maturing, both in terms of tooling and practices.
Most teams are still somewhere on the journey towards GitOps, but the teams that adopt GitOps tend to actually make more deployments!

Most notably

## CI/CD Choreography vs Orchestration

## OpenTelemetry

## Chaos Testing / Engineering

## eBPF capabilities

### Real traffic testing with Pixie

## linkerd

## Some new features to check out

### Debugging in Kubernetes with ephemeral containers

### Krew: kubectl extension package manager

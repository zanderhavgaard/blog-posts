**!This blog post is WIP!**

---

# working title: 10 Reasons why not to use Kubernetes!

While we all love Kubernetes and the many awesome things we can achieve with it - it's also important to be critical and continuously evaluate the tools and solutions we use.
The point of this blog post is not to discourage the use Kubernetes, quite the opposite, but to nuance the discussion, and to acknowledge that Kubernetes is actually not the answer to all problems! (No matter how much I want it to be :-) ...)

## k8s is not stable --> it is ever-evolving

## k8s is not great for serving user intefaces --> use CDNs!

## k8s is not great for running databases --> use managed DBS!

## k8s is not great for storing your data --> use storage solutions!

## k8s is not great for event driven architectures --> use FaaS (in k8s: knative)!

## k8s is not always the best place to run workloads ...

## k8s is not great for running your legacy (monolith) --> rearchitect for microservices!

Stateless, high-availablilty, horizontal scaling

"how much of your workload is actually ready for k8s?"

## K8s is hard to maintain --> you should pay someone to do it for you, like a cloud provider!

## k8s is complicated and hard to use (especially if you are a small company / start-up) --> use a simpler container orchestration solution! and you probably don't need all of the features of k8s

Sometimes container orchestration -as-a-service is a better fit

## You need many external tools/plugins: service meshes, storage driver, token handler etc.

---

# So what should I use k8s for???

# k8s is great for orchestrating your ephemeral/stateless containers!

# k8s is a control-plane!

---

Marko's notes:

I guess part of this message is debatable, but it's ok. I hope this helps you (at least you should have 5 more)... :D

- :kubernetes: in not for serving UI's. Many modern microservice app has ui packed as a container to work as a 'frontend' and it's served from :kubernetes: (e.g. routing + simple nginx. I've done that too.). It's cute, but it's wrong. Frontends should be delivered + served from a CDN or similar (e.g. all cloud vendors or cloudflare.com).

- :kubernetes: is not for serving databases. Probably no need to explain that further.

- :kubernetes: is not for storing data. All cloud providers have services for that - and they are easier to use than persistent volume claims (pvc's) etc. There might be a place for that, but more rarely than what they are used.

- Many applications have very slim backends (node, go, rust, plesk, ...) serving as a connection between the UI and the DB. While a nice idea, and easy to ship from a container, I would seriously consider using serverless / FaaS in most cases. Or just services like firebase.

- :kubernetes: is not for serious calculation nor processing. This is a bit of a weak spot for modern cloud still (periodic data processing), and so its handy to solve with a K8s CronJob or a background processing Deployment (such as BullMQ), but I wouldn't use :kubernetes: for that either.
  Good luck with your post
  @Zander Havgaard
  ! :muscle: (edited)

It’s more about the fact that we’re slowly stepping out of the monolith-thinking, and it’s a win for many to be able to squeeze their apps into containers. However that is not always the best option. Thus some of my opinions above are debatable - especially for people who are afraid of cats eating their source code (reference to ’pragmatic programmer’). (edited)

Kalle's notes:

Okay so here are some technical aspects:

- Kubernetes is not stable. What I mean is Kubernetes is ever evolving product, it means it will keep changing and the changes it creates can be big, if your applications part that you deploy to kubernetes should be "we deployed and forgot" this is not what kubernetes was created or is created for. Kubernetes is designed for constant change. You can't use kubernetes as the place that will stay the same, like your VM's

- Kubernetes does not solve the applications HA solution. You need to program your software to do the HA itself (stateless softwares) as kubernetes does not care, and it should not care about how the HA is done, thats your job.

- Plugins. See Jenkins for reference. (How do I do secure networks in kubernetes: install x, How do I do this storage driver: install y, how do i do secure tokens in kubernetes Install z) this is by no means not yet as bad as Jenkins has, but its getting very difficult to stay up-to-date what works and how

- Adding layers: If you are already doing solid deployments and have a constant deployment on-going to cloud kubernetes just adds complexity to your software, as you most likely have IAAC and automated software delivery, if you add kubernetes in additon to cloud network, storage etc. you have same for Kubernetes.

- Kubernetes in EE setting: Kubernetes was not designed for RBAC models, and you can see it (if you really use this let's have a meeting)

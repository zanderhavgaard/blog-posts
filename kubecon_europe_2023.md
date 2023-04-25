# KubeCon 2023 Europe Takeaways and Trends

Security is huge
eBPF is huge
WASM will take over the world (eventually)
cilium is all the buzz

both argocd and flux graduated - gitops commoditized

Everybody adopted platform engineering - now we are all figuring out how to do it - argo and multi-tenancy were huge topics

If you didn't attend KubeCon/CloudNativeCon Europe this year, you've come to the right blog, as I will outline the main trends and takeaways:

- GitOps has been commoditized with the CNCF graduation of the ArgoCD and Flux projects, congrats to them!
- Last year everybody adopted Platform Engineering and now we are trying to figure out how to actually do it.
- Networking is still hard, and tools like Cilium are helping to enable more advanced networking capabilities.
- Observability is getting better and better, especially with eBPF technology enabling kernel-level observability.
- Web Assembly (WASM) is looking be the next big revolution in how we develop and deliver software.
- Security is huge topic, indicating that the CNCF landscape and community is maturing.

## GitOps has been commoditized

I find it very telling that at KubeCon last year, one of the co-located events was GitOpsCon, a hole day dedicated to how to _use_ GitOps.
While KubeCon has always been more of a tooling centered conference, it's fitting that this years iteration as ArgoCON - specifically focusing on ArgoCD and Argo rollouts.
Which implies that we are moving away from figuring out exactly how to use the practice of gitops and towards improving the tooling of gitops.

Both ArgoCD and Flux are now graduated CNCF projects, which means that they have received the CNCF "stamp of approval": they have a large and vibrant community, the technology is mature and all of the components have undergone third-party security audits - in other words they are battle-tested and production ready.

While both ArgoCD and Flux are great tools, the community seems to favor ArgoCD, as it is one of the most popular CNCF projects.

On the devstats Grafana dashboard we can see that ArgoCD is one of the most popular CNCF projects.

https://all.devstats.cncf.io/d/1/activity-repository-groups?orgId=1&var-period=h24&var-repogroups=All&from=now-1y%2Fy&to=now-1y%2Fy

- both argocd and flux graduated projects
- last year we had gitopscon this year we had argocon
- argo as one of the top 10 projects in the cncf
- gitops becoming mature - moving towards "commoditized"
- other argo tools look interesting: rollouts, workflows, events
- many managed argo solutions

## Platform Engineering is hard, especially if you also want a good Developer Experience

Last year at KubeCon there were many talks on Platform Engingeering as an emerging practice.
This year it seems that the buzz has not quieted down and instead been replaced by everyone who adopted platform engineering now figuring out how to do it in practice.
Topics like multi-tenancy, developer portals and internal developer platform, were abundant among the talks.

In terms of multi-tenancy, it was a debated topic whether to isolate tenants in their own clusters, nested vclusters (virtual clusters) or using Kubernetes native namespaces.
This is further complicated by varying needs for security and isolation.

The community seems to have embraced Backstage as the go-to developer portal, with a vibrant community with many users developing plugins.
The biggest reason why many organizations are hesitant to adopt Backstage at the moment is that to realize the full potential, some amount of custom code is required, and therefore I am happy to pass on the update from the Backstage project that they are working hard on making operating Backstage a declarative experience, with no custom code required.

- last year everyone talked about platform engineering, seems that this year everyone is trying to figure out how to do it
- topics such as multi-tenancy were big this year
- devex
- backstage / idp / service catalogs
- idp as SaaS - getport.io
- dev tooling for working with k8s - devspace, okteto, loft etc.
- crossplane was not buzzed so much this year, but seems to have been adopted by the community, though it is still pretty hard to use

## Observability is getting better / eBPF is cool / cilium is all the rage

- enables kernel level functionality, without having to use a new / different kernel
- extend the kernel in a safe and efficient way
- innovative new usecases that were not possible before
- enables networking functionality and observability
- see everything happening in the system
- low level technology
- wide use in the industry, users: android, google, facebook
- even tcpdump uses ebpf with a filter

### Networking is still hard, but the tools are getting better

Operating cloud native workloads requires a lot of networking, and as our cloud native landscape get increasingly complex and sophisticated, so does our networking requirements.
Thankfully there are many tools to help with better networking like

## WASM is the future

- much buzz around WASM
- whole day wasm co-located events
- many talks on the subject
- very exciting new technology
- originally meant to enable non-js code to run in browsers client-side, but now also getting relevant server-side
- my take is that it is not relevant yet, but will be the future, especially once we move beyond k8s

## Security is becoming commoditized / ubiquitous

- most new contributions to cncf community are security related
- many new tools / services
- switch security left / earlier in the dev/delivery process

## other

- tv2 gateway api talk
- choose your own path
- microvms on rpi cluster

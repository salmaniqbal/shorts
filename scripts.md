# Scripts 

This is a collection of scripts that I use to explain Kubernetes concepts in 60 seconds or less. I am focusing on getting the time down to 30-45 seconds. 
The shorts start with a hook and explain the concept in a simple way. I use animations and slides made in figma to explain the concept. I zoom in and out to explain concepts and also use memes to make it more relatable. I also share snippets of yaml to explain the concept. 

## 002 - API

So, the Kubernetes API plays an important role when a request is submitted to the kubernetes cluster. Imagine you have a cluster

And you submit a request to deploy 2 replicas of a pod

This request is received by the API server in the cluster control plane. The API is made up of multiple components 

The first component verifies whether the user has access to the cluster; if not, the request is rejected, otherwise it’s passed to the next stage.

The next step checks whether the user has required permissions to do what they are about to do. Role Based Access Control is used to define whether the user can create a deployment etcetera

Then the mutation admissions controller modifies requests, adds defaults, and applies extra properties defined by policy engines such as Kyverno.

Schema Validation then checks if the request conforms to the defined resource's schema

The validation admission controller checks requests against standard Kubernetes rules and custom policies, rejecting any that don’t comply.

For example you can define a rule that states that only private container images are allowed

And if someone submits a public image, the request will be rejected

After all these and few other checks, the resource handler writes the final object to etcd

this will include the information about the deployment and how many pods are to be created

Then we have a few other components whose job it is to spin up the required pods in the cluster!

Next time you submit a YAML file, remember that it doesn’t just waltz into etcd. It gets interrogated, mutated, validated, and only then, maybe, admitted to the cluster.

## 003 - Operators

Did you know that you can order a pizza using Kubernetes? Let me explain.

When you request a Pod to be created in Kubernetes, the controller manager records it in etcd and ensures that the desired number of Pods are created and scheduled in the cluster. 

Standard objects like Pods, Services StatefulSets are managed by the controller.

What if you want something Kubernetes doesn’t support by default like a Postgres database?

You can install a custom controller, called an Operator 

The Operator watches for a custom resource that says you need a Postgres database  and then automatically deploys and manages it for you


There’s an Operator for almost anything you can think of and yes, you can even build your own.

And then there’s one for pizza! It’s called the Cruster API 🍕.

Apply this YAML file and Kubernetes will actually order a real pizza for you!

So yeah with Kubernetes Operators, you can automate anything, from databases to dinner. 

## 004 - Scheduler

Do you know that Kubernetes plays Tetris with the containers you want to deploy?

When you deploy a Pod in Kubernetes, a component called scheduler scans the nodes and decides which one is the best fit for the pod and places it there.

It filters out the nodes that don’t have enough resources or don’t meet requirements then it scores the remaining ones to find the best match and places the pod there.

You can influence the scheduler, with rules like:
Node selectors to target specific nodes,


Pod affinity to group related workloads,


And taints and tolerations to keep unwanted pods away
And if you want full control, you can even tweak the Scheduler’s settings or build your own!

Imagine that Kubernetes tetris but you get to design the rules 

## 005 - Namespaces

Did you know that Kubernetes namespaces do not provide any security in your cluster?
(Namespaces != Security)

Namespaces are just a logical way to group resources, they are not a security boundary. 

Aaand Kubernetes networking rule #1? Every pod can talk to every other pod… basically a giant group chat nobody asked for. 

You can secure your namespace using Network Policies. These let you control pod-to-pod communication, so only the traffic you explicitly allow is permitted

But security isn’t the only problem with namespaces
They also don’t give you any resource isolation
A pod in one namespace can chew through all the CPU and memory on a node and take everyone else down with it
To fix that, Kubernetes gives us ResourceQuota.
This lets us cap how many pods, how much cpu and memory a namespace can consume
So remember, Namespaces organise, Policies isolate and resource quotas limit


## 006 - Autoscaling 
Title: Kubernetes Autoscaling Explained (HPA, VPA, Cluster Autoscaler)
Description: Learn how Kubernetes scales your pods and cluster automatically using Horizontal Pod Autoscalar, Vertical Pod Autoscalar and the Cluster Autoscale

Did you know Kubernetes can scale your apps, your pods and even your entire cluster… automatically?

When your app gets busy, the Horizontal Pod Autoscaler checks a metric that you define, like CPU or traffic. And if it crosses the threshold, it instantly spins up more replicas, and when the demand drops it scales them back down when demand drops. This is known as Horizontal Pod Autoscaling

When we create a pod, we define how memory and CPU it should consume. This helps Kubernetes to place it on a suitable node and prevent unexpected termination. But workloads change over time. Virtual Pod Autoscalar watches usage over time and automatically updates the resource requests so the pod is not evicted unnecessarily.

And if the cluster runs out of space and pods can’t be scheduled, the Cluster Autoscaler steps in. It adds new nodes when the cluster needs more capacity and removes them when demand drops.

With Vertical Pod Autoscalar, Horizontal Pod Autoscalar and the Cluster Autoscaler working together, Kubernetes makes sure your app always has the right amount of power… without you lifting a finger.


## 007 - PodPriorty
Did you know that you can make Kubernetes scale faster, without changing the autoscalar 

When the cluster is full, new pods sit in Pending state while a node is added which could take a few minutes. 

To reduce this, we can use PriorityClasses. 

PriorityClasses let you rank workloads like high, medium, or low.
Pods then reference one of these classes.
Pods with higher PriorityClass values get preference in scheduling over lower ones
For faster cluster autoscaling we deploy a low priority placeholder pod and when a pod with higher priority arrives the low priority pod is evicted to make space for the new pod
The Cluster Autoscaler then adds a new node for the placeholder pod, effectively scaling the cluster in advance. 
So remember, use PriorityClasses to make sure important workloads always come first.



## 008 - Node Capacity
Did you know that in Kubernetes, pods do not get 100% of the resources available on the node? 
First, we need to reserve some CPU and memory for the operating system so it can run things like system processes, network & disk management  
Next is kubelet reservation.
Kubelet is an agent that runs on every node. It talks to the control plane, manages pods and reports node health. To do this reliably, kubernetes reserves some resources 
Then there is the eviction threshold.
The kubelet watches node resources like memory and disk. If usage crosses a safe limit, it evicts pods early to protect the node from failing, so Kubernetes reserves some resources for that
Only what’s left is available for the pods.
The exact split on resource allocation depends on node size. For example on an AWS m5.large node, there is 8 Gigabytes of memory and 2 virtual CPUs. About 19% is reserved for the OS and Kubelet, about 3% for eviction threshold and the rest is used by the pods.
If you want the exact number for your worknode, you can check out the learnkube instance calculator, link is in the description


## 009 - Promo

 A few weeks ago, I set myself a challenge…
Can I explain Kubernetes concepts in 60 seconds or less?
So I started making YouTube Shorts
Like did you know that or, or, you get the idea
So far I have made 8 shorts and i have said the word kubernetes 26 times plus there are some memes in there too!
I hope you’ll learn something useful from these videos…
But don’t take my word for it 
let’s hear from the experts.
Daniele: A rare sight, Kubernetes concepts explained clearly in under a minute. Remarkable.
Bart: Concise, insightful… rather good, actually.
Lewis: Mad clear explanations, innit bruv. 
Cheers chaps. 
If this sounds useful, head over to youtube.com/soulmaniqbal
Check out the shorts and let me know what you think.”
And if there’s a Kubernetes topic you want covered, drop it in the comments.
The link the channel is also in the comments, like & subscribe, thank you! 



## 010 - I let AI debug my kubernetes cluster

You deploy a website in a kubernetes cluster, you try to access it and it doesn’t work

So you start checking everything 
Is the container healthy?
Are the ports correct?
What about the labels?
And the probes?
Did you hit resource quota?
Is the kubelet down?
Is there enough space?
Does the image even exist?

Or… you could just ask AI
Hey kagent, what’s wrong with my deployment?

There it is, it’s telling us to fix the port mapping!
So, how did it know that?

Kagent is an AI agent that runs inside your Kubernetes cluster
You prompt it using CLI or UI
It gathers real cluster context, sends that to an LLM like ChatGPT
And points you directly to the fix

It’s not only for Kubernetes, it understands the ecosystem around it. Check it out.

Would you trust AI to help run your cluster? let me know in comments




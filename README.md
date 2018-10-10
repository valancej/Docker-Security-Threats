# Docker Security Best Practices

## Introduction

In previous posts we've spent a significant amount of time diving into what Anchore scanning coupled with Anchore policy checks can do to help achieve certain compliance standards and benchmarks. Additionally, we've walked through the different triggers and gates of Anchore polcies that can be configured to look for issues like exposed ports, effective users, and high severity security vulnerabilies (CVEs), to name a few. Along with these policy checks, we've discussed the necessary tooling needed for these scans and policy evaluations to align with a more secure container image build pipeline. All of these best practices are related to Anchore and container image scanning in particular, they do not directly address the other security issues that come with the usage of containers. In this post, I will discuss security of the Docker Host, the Docker Engine, Docker Images, and Runtime Security for Containers. 

## Securing the Host Operating System

Docker security starts at the host layer, and is only as strong as this layer. If attackers are able to compromise the host OS, they could potentially compromise all processes on this OS, including Docker. For the vast majority of Docker users, the host operating systems in a Linux distribution, so best practices for secure OS infrastructure should follow. The host operating system should be kept patched and updated. One example of this is to minimize the attack surface of the host OS. For most secure infrastructure, the base OS should be specifically designed to run Docker only, no other processes that could be compromised. 

## Securing Docker Images

Encorporating the appropriate mechanisms to conduct static analysis on your container images gives insight into any potential vulnerable OS and non-OS packages. As discussed in previous posts, Anchore gives you the ability control whether or not you would like to promote non-compliant images into trusted registries through policy checks within a secure container build pipeline. This step is important because vulnerable images that make their way into production environments pose significant threats to those environments and are also costly. Within these images, focus on the security of the applications that will be running, although other checks are important, your application must be secure as well.

A nice article on the shifting left paradigm: https://www.cloudbees.com/blog/continuous-security-delivering-secure-apps-kubernetes

## Securing Container Runtime

It is important to set up tooling to monitor the containers themselves that are running. If new vulnerabilies get published that are impactful to a particular container, the appropriate alerting mechanisms need to be in place to quickly stop and replace the vulnerable container. Put simply, container infrastructure should be immutable.

The first piece of securing the container runtime is securing the registries where the images reside. For organizations, it is considered best practice to only pull and run images from trusted container registries. As an added layer of security, only trusted and signed images should be promoted into production registies. Vulnerable, non-compliant images should not reside in container registires where images are staged for production deployments. 

The Docker Engine hosts and runs built container images that are pulled from regisitres. Namespaces and Control Groups are two aspects of Docker Engine security that need to be taken into consideration. 

Namespaces provide the first and most straightforward form of isolation: processes running within a container cannot see, and even less affect, processes running in another container, or in the host system.

- Namespaces should always be activated.

Control Groups implement resource accounting and limiting. 

- Resource limits should always be set for containers. This way a single container does not hog all resources and bring down the system. 

Additionally, the Docker daemon itself should only be controlled by trusted users. Currently, root privileges are required to run Docker commands, and caution should be executed when making changes to the Docker group. 

Sysdig Falco is an example of a tool that will continuously monitor and detect anomalous activity in applications and containers: https://github.com/falcosecurity/falco/wiki/About-Falco


## Conclusion

Containerized applications and environments present new security concerns, but fundamentally basic concepts for host and application security can play critical roles is establishing a stronger container security posture. When discussing container adoption, container image scanning, runtime monitoring, and host security are great places to start, however security best practices like scanning application source code for vulnerabilies/coding errors both in open source and propriety, along with adopting a DevSecOps culture both contribute to a more secure container environment. 
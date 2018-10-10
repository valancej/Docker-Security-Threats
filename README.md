# Docker Security Best Practices

## Introduction

In previous posts we've spent a significant amount of time diving into what Anchore scanning coupled with Anchore policy checks can do to help achieve certain compliance standards and benchmarks. Additionally, we've walked through the different triggers and gates of Anchore polcies that can be configured to look for issues like exposed ports, effective users, and high severity security vulnerabilies (CVEs), to name a few. Along with these policy checks, we've discussed the necessary tooling needed for these scans and policy evaluations to align with a more secure container image build pipeline. All of these best practices are related to Anchore and container image scanning in particular, they do not directly address the other security issues that come with the usage of containers. In this post, I will discuss security of the Docker Host, the Docker Engine, Docker Images, and Runtime Security for Containers. 

## Securing the Host Operating System

Docker security starts at the host layer, and is only as strong as this layer. If attackers were able to compromise the host OS, they could potentially compromise all processes on this OS, including Docker. For the vast majority of Docker users, the host operating systems in a Linux distribution, so best practices for secure OS infrastructure should follow. The host operating system should be kept patched and updated. One example of this is to minimize the attack surface of the host OS. For most secure infrastructure, the base OS should be specifically designed to run Docker only, no other processes that could be compromised. 

## Securing Docker Images

Encorporating the appropriate mechanisms to conduct static analysis on your container images gives insight into any potential vulnerable OS and non-OS packages. As discussed in previous posts, Anchore gives you the ability control whether or not you would like to promote non-compliant images into trusted registries through policy checks within a secure container build pipeline. This step is important because vulnerable images that make their way into production environments pose significant threats to those environments and are also costly. A nice article on shifting left: https://www.cloudbees.com/blog/continuous-security-delivering-secure-apps-kubernetes?utm_campaign=General&utm_source=LinkedIn&utm_medium=Organic&utm_term=Continuous%20Security%20blog

## Securing Container Runtime


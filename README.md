# Docker Security Best Practices

## Introduction

In previous posts we've spent a significant amount of time diving into what Anchore scanning coupled with Anchore policy checks can do to help achieve certain compliance standards and benchmarks. Additionally, we've walked through the different triggers and gates of Anchore polcies that can be configured to look for issues like exposed ports, effective users, and high severity security vulnerabilies (CVEs), to name a few. Along with these policy checks, we've discussed the necessary tooling needed for these scans and policy evaluations to align with a more secure container image build pipeline. All of these best practices are related to Anchore and container image scanning in particular, they do not directly address the other security issues that come with the usage of containers. In this post, I will discuss security of the Docker Host, the Docker Engine, Docker Images, and Runtime Security for Containers. 

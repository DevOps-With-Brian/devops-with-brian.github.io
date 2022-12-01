---
title: "New Video Series - Terraform Kubernetes Personal Cluster $40 a month"
date: 2022-11-25
categories:
  - blog
  - devops
  - terraform
  - youtube
  - kubernetes
  - iac
  - Infrastructure As Code
  - Linode
tags:
  - tutorial
  - kubernetes
  - terraform
  - IaC
  
---

We are launching a new video series today that consists of setting up a [Linode](https://www.linode.com/lp/refer/?r=24202434814cd6f94325c26c8a78803a931bed0f) LKE or Kubernetes cluster on a 3 shared node setup with a NGINX ingress using a Linode NodeBalancer for $40 a month.

In this tutorial series you will learn how to use [Terraform](https://www.terraform.io/) to deploy the cluster as well as use [Terraform Cloud](https://app.terraform.io/signup/account) to manage our remote state in Terraform for free.

We also will be setting up a [GitHub Pages](https://pages.github.com/) page using [Minimal Mistakes Starter](https://github.com/mmistakes/mm-github-pages-starter/generate) theme and tying this to our own custom domain.

In the final part of this using our custom domain we will be using cert-manager to setup automated SSL certs for our apps we decide to publish through our ingress, in this example it will be a [Rasa](https://rasa.com/) chatbot example that we already did a video on which can be found below.


{% include video id="kNbFIn-68Z4" provider="youtube" %}


The cookiecutter template used in the video series can be found here, [Cookie Cutter Template](https://github.com/DevOps-With-Brian/cookiecutter-linode-tf-lke).

If you chat with the chat widget on this website you can see a live demo of this running in kubernetes actually.  The bot is basic atm but will be updated shortly.

Part 1 of the video series can be found below:

{% include video id="2cCxEcvPh8c" provider="youtube" %}


Part 2 of the video series can be found below:

{% include video id="5Nst9erhfH8" provider="youtube" %}

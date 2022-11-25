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
  
---

We are launching a new video series today that consists of setting up a [Linode](https://www.linode.com/) LKE or Kubernetes cluster on a 3 shared node setup with a NGINX ingress using a Linode NodeBalancer for $40 a month.

In this tutorial series you will learn how to use [Terraform](https://www.terraform.io/) to deploy the cluster as well as use [Terraform Cloud](https://app.terraform.io/signup/account) to manage our remote state in Terraform for free.

We also will be setting up a [GitHub Pages](https://pages.github.com/) page using [Minimal Mistakes Starter](https://github.com/mmistakes/mm-github-pages-starter/generate) theme and tying this to our own custom domain.

In the final part of this using our custom domain we will be using cert-manager to setup automated SSL certs for our apps we decide to publish through our ingress, in this example it will be a [Rasa](https://rasa.com/) chatbot example that we already did a video on which can be found by clicking on the thumbnail below

[![Rasa Auto Version Chatbot](/assets/images/rasa_chatbot_thumbnail.png)](https://youtu.be/kNbFIn-68Z4)

The cookiecutter template used in the video series can be found here, [Cookie Cutter Template](https://github.com/DevOps-With-Brian/cookiecutter-linode-tf-lke).

If you chat with the chat widget on this website you can see a live demo of this running in kubernetes actually.  The bot is basic atm but will be updated shortly.

Part 1 of the video series can be found by clicking the thumbnail below:

[![How To Build Linode Kubernetes Cluster for $40 A Month With Terraform - Part 1](/assets/images/linode-tf-part-1.png)](https://youtu.be/2cCxEcvPh8c)


Part 2 of the video series can be found by clicking the thumbnail below:

[![How To Build Linode Kubernetes Cluster for $40 A Month With Terraform - Part 2](/assets/images/linode-tf-part-2.png)](https://youtu.be/5Nst9erhfH8)
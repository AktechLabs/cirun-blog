---
layout: post
title: "Fast GitHub Actions runners on your Cloud! 🚀"
---

## GitHub Actions

[GitHub Actions](https://github.com/features/actions) is a powerful and flexible automation
platform provided by GitHub. It allows developers to automate various tasks,
directly within the GitHub repository, such as

- building
- testing
- deployment

By default GitHub Actions runners (the machine where the above-mentioned tasks run) runs on
GitHub's Infrastructure, but you can run it on your infrastructure too.

## Cirun.io

[Cirun.io](https://cirun.io) is a service to run GitHub Actions on your cloud (or on-prem), launched
in **March 2021**:

<div>
<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Introducing <a href="https://t.co/kNS0nBffkN">https://t.co/kNS0nBffkN</a> 🚀 an easy way to create managed self-hosted Github Action runners (for CI/CD) in your cloud. We&#39;re in alpha at the moment, feel free to give it a try: <a href="https://t.co/6zyd4EOx31">https://t.co/6zyd4EOx31</a> <br><br>Open to feedback/suggestions/feature requests. ✨👂 <a href="https://t.co/sBbTUw63WX">pic.twitter.com/sBbTUw63WX</a></p>&mdash; Amit Kumar Jha (@iaktech) <a href="https://twitter.com/iaktech/status/1369984075029749760?ref_src=twsrc%5Etfw">March 11, 2021</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>

## But why?

- Fast and performant runners
- Cost efficient
- Custom Machines
- GPU Runners

## How?

By changing one line in your GitHub Workflow (e.g. `.github/workflows/<workflow-name>.yml`)

```yaml
runs-on: "cirun-aws-t2-large-ubuntu2204"
```

or alternatively, for advance configuration, by creating a `.cirun.yml` file in
the root directory of your repository:

```yaml
# Self-Hosted Github Action Runners on AWS via Cirun.io
# Reference: https://docs.cirun.io/reference/yaml
runners:
  - name: "aws-runner"
    # Cloud Provider: AWS
    cloud: "aws"
    # Instance type on AWS
    instance_type: "t2.medium"
    # Ubuntu-20.4, ami image
    machine_image: "ami-06fd8a495a537da8b"
    preemptible: false
    # Add this label in the "runs-on" param in .github/workflows/<workflow-name>.yml
    # So that this runner is created for running the workflow
    labels:
      - "cirun-aws-runner"
```

The above configuration will create a `t2.medium` EC2 instance on your AWS
with AMI ID mentioned in the `machine_image` key, whenever a GitHub Actions job is created,
which has `runs-on: cirun-aws-runner` .

## Where?

Cirun is supported on **six** cloud providers, YES you read that right, **6**!

- [AWS](https://aws.amazon.com/)
- [GCP](https://cloud.google.com/)
- [Azure](https://azure.microsoft.com/)
- [DigitalOcean](https://digitalocean.com/)
- [OpenStack](https://www.openstack.org/)
- [Oracle](https://www.oracle.com/cloud/)

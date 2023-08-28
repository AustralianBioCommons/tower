---
title: Configure and use compute environments
contributors: [Ziad Al-Bkhetan, Johan Gustafsson, Georgina Samaha]
description: Instructions to add and configure compute envornments for HPCs and commercial cloud services.
toc: true
type: guides
---

## Introduction

Tower supports running pipelines on several compute platforms including commercial cloud such as AWS and Azure, as well as high-performance computer (HPC). A full list of supported platforms is available through [Tower documenation] (https://help.tower.nf/latest/compute-envs/overview/). 

To access these compute infrastructures through Tower, compute environments need to be created and configured on Tower for each compute infrastructure.


## Configuring HPC on Tower

Tower supports adding compute environments for HPCs that utilise [Slurm](https://help.tower.nf/latest/compute-envs/slurm/) and [PBS Pro](https://help.tower.nf/latest/compute-envs/altair-pbs-pro/) workload managers. 

{% include callout.html type="note" content="Compute environments are shared across the users of the same workspace." %}

In order to access compute infrastructure, you need to create access [credentials](https://help.tower.nf/latest/credentials/overview/#introduction). SSH keys or Tower agents can be used to access the HPC. SSH keys are easier to use but some HPC providers are restricted from sharing SSH keys with a third party (e.g. Tower Service). In addition, it can be tricky to use SSH keys if the HPC is in a private network and requires VPN access. 

The following instructions will help you configure compute environments for HPC by using Tower Agent credentials.


### Steps to configure HPC on Tower within organisation workspace


#### Prerequisites for configuration on organisation workspace:

- You have access to an organisation workspace
- The user has an owner or admin role within this workspace.

The following steps need to be completed in order, unless they have been completed earlier and are going to be reused.

1.	[Create Personal Token](create_personal_token)
2.	[Create Tower agent credentials](create_tower_agent_credentials)
3.	[Configure the compute infrastructure](configuring_compute_environment)


### Utilising Compute environment with Tower Agent

There are few points to be considered when using the Tower Agent.

- The users of a workspace will share the same compute environment and credentials.
- Each user needs to create their own personal access token.
- Each user needs to run Tower agent on their account on the HPC.
- Each user needs to pass their personal access token and the shared connection id (of the credential) to their instance of tower agent on the HPC.

To address these points:

1. Create a personal access token or use a pre-created access token as described here (access1).
2. Obtain the connection id for the compote environment from its credential page (conn_id).
3. Run Tower agent using access1 and conn_id, and an independent work directory (any directory you have access to).
4. The compute environment will be available and usable as long as the agent is running.

{% include callout.html type="important" content="Tower agent does not support service accounts on the HPC. In other words, you can not use one agent for multiple users on tower." %}

{% include callout.html type="note" content="The agent should be able to access the internet." %}


## Configuring commercial cloud resources

The easiest way is using AWS Batch and tower forge permissions to allow tower to create the batch environment. In order to do this please follow this [documentation](https://help.tower.nf/latest/compute-envs/aws-batch/).

Other Compute infrastructures such Azure and others: Please visit [Tower documentation](https://help.tower.nf/latest/compute-envs/overview/) for more details.


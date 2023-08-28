---
title: Joining the pilot project
description: Information on how to join the Australian BioCommons Nextflow Tower pilot project.
type: pilot
toc: false
---

## Access and available support

Australian researchers, research groups and organisations can join the Australian BioCommons Nextflow Tower pilot project through the personal or organisation workspace [access model](access-models) that suits their needs.

If your group would like to access and explore the organisation workspace, please express your interest by [contacting us](contact_us). A member of the project team will be in contact to discuss this further. Otherwise, you can access the personal workspace option by logging into the service at this [link](https://tower.services.biocommons.org.au).

Please note that we are unable to directly support personal workspaces at this stage as we have limited capacity during the pilot phase. The available support is summarised below.

**Personal workspace support:**

-   Documentation and [user guide](/tower/user-guide/index) available. 
-   Support for technical issues related to the core functionality of the Australian BioCommons Nextflow Towerservice, such as service availability
-   There is no support available for workspace resources configuration or management issues such as workflows, compute environments, and credentials.

**Organisation workspace support:**

-   Documentation and [user guide](/tower/user-guide/index) available
-   Hands-on support from BioCommons staff to deploy your workspace under the following conditions:
-   Fulfilment of the prerequisite list described below.
-   Agreement to follow a support plan with milstones to achieve.
-   Access to compute infrastructure is available through [Australian BioCommons Leadership Share (ABLeS)](https://australianbiocommons.github.io/ables/) if eligibility criteria are met.

If you meet the prerequisites for an organisation workspace and require help to quickly push your workspace to production mode, [contacting us](contact_us) to discuss this.

If you are unable to meet the prerequisites, you can still access the BioCommons Nextflow Tower service to explore and learn more. However, we encourage you to start working on meeting the prerequisites, as they are essential for effective use of the workspace and to gain the benefits of the support team.

As we are in a pilot project phase, there may be some unplanned interruptions and outages. We will attempt to minimise any disruption during this time.  

## Prerequisite list

1.  **Access to compute infrastructure**\
    At least one compute infrastructure that can be configured on the BioCommons Tower service. There are several platforms that are supported on Tower and you can find them here.

2.  **Nextflow workflows**\
    You should have nextflow workflows implemented and tested on the compute environments from 1. Internally implemented workflows, those re-used from nf-core, or any other resources are ok. We prefer implementation of config profiles that allow docker/singularity executions for portability purposes.

3.  **Testing datasets**\
    For any suggested workflow, there must be testing datasets available during deployment on the BioCommons Tower service. This should include small datasets for quick testing and real datasets for production testing.

4.  **Nextflow expertise**\
    The deployment and configuration of compute environments and workflows should be led and driven by the group or organisation. This requires t dedicated resources with technical expertise in Nextflow, and infrastructure expertise, including HPC and commercial cloud (depending on the exact use case).\
    The dedicated resource with relevant expertise may need to:

    -   Implement changes to the workflow (usually edits to the configuration profiles)
    -   Configure, test and debug the workflows on the infrastructures from prerequisite 1
    -   Understand the available computational resources they access
    -   Have admin access to the compute infrastructure
    -   Manage user access to the organisation workspace.



## Support to access infrastructure 

The Australian BioCommons provide support to access compute infrastructure on NCI Australia and the Pawsey Supercomputing Centre for eligible researchers, research groups and/or organisations through the [Australian BioCommons Leadership Share (ABLeS)](https://australianbiocommons.github.io/ables/).




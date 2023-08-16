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

> Note: compute environments are shared across the users of the same workspace. 

In order to access compute infrastructre, you need to create access [credentials](https://help.tower.nf/latest/credentials/overview/#introduction). SSH keys or Tower agents can be used to access the HPC. SSH keys are easier to use but some HPC providers are restricted from sharing SSH keys with a third party (e.g. Tower Service). In addition, it can be tricky to use SSH keys if the HPC is in a private network and requires VPN access. 

The following instructions is to configure compute invirnment for HPC through Tower agent credentials.


### Steps to configure HPC on Tower within organisation workspace

Prerequisites for configuration on organisation workspace:

1.	You have access to an organisation workspace
2.	The user has an owner or admin role within this workspace.


The following steps need to be completed in order unless they have been completed before and are to be reused.

1.	Create Personal Token
2.	Creating Tower agent credentials
3.	Configuring the compute infrastructure


**Detailed Instructions:**

<div class="accordion" id="accordion-comp-env-all">
    <div class="accordion-item">
        <h2 class="accordion-header" id="heading-access-token" style="margin-top:0rem">
          <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapse-access-token" aria-expanded="false" aria-controls="collapse-access-token">
            Create Personal Token
          </button>
        </h2>
        <div id="collapse-access-token" class="accordion-collapse collapse" aria-labelledby="heading-access-token" data-bs-parent="#accordion-comp-env-all">
          <div class="accordion-body">  
            You don’t need an access token if you intend to create SSH key credentials, but you will need it for the Tower agent credentials. 
            <ul>
            <li>The user can create an access token as <a href="https://help.tower.nf/latest/api/overview/?h=access+token#authentication"> described here </a>.</li>
            <li>Keep it safe, create a new one if you lose it and delete lost tokens</li>
            <li>Use descriptive names.</li>
            <li>Don’t share your token with others.</li>
            <li>After you close the token creation window, you will not be able to view/copy the Token any more, but you can update it or delete it.</li>
            </ul>
            <div class="alert alert-primary" role="alert">
            <h4 class="alert-heading">Note</h4>
            <p>The same personal access token can be used with multiple Tower agents, however, we recommend creating one access token for each credential or at least for each compute infrastructure.</p>
            </div>
          </div>
        </div>
    </div>
    <div class="accordion-item">
        <h2 class="accordion-header" id="heading-tower-agent" style="margin-top:0rem">
          <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapse-tower-agent" aria-expanded="false" aria-controls="collapse-tower-agent">
            Creating Tower agent credentials
          </button>
        </h2>
        <div id="collapse-tower-agent" class="accordion-collapse collapse" aria-labelledby="heading-tower-agent" data-bs-parent="#accordion-comp-env-all">
          <div class="accordion-body">
            <p><a href="https://help.tower.nf/latest/agent/">Tower agent </a> is software that runs on the HPC and communicates with Tower API to perform all tasks needed on the HPC including launching a pipeline and monitoring its execution. For an admin to create a tower agent credential, follow the following steps:</p>
            <ol>
                <li>Navigate to the workspace you want to add credentials to, then click on the <code>Credentials</code> tab.</li>
                <li>Click on the <code>Add Credentials</code> button under <code>Credentials</code> to create a shared <code>Agent connection ID</code> for the tower agent.</li>
                <li>A wizard interface will appear, with some scripts in the <code>Usage</code> box and fields to complete.</li>
                <br/>
                <div style="text-align:center"><img width="50%" src="../assets/doc_img/agent.png"/></div>
                <br/>
                <li>Give your credential a descriptive name, this is working at the infrastructure level so we recommend creating different credentials for different environments.</li>
                <li>Keep <code>Shared agent</code> disabled. check <a href="/user-guide/shared-agent.md">Shared agent section</a> for more details on this.</li>
                <li>Before adding the credential you will need to run the agent on the compute infrastructure. To do this:
                    <ol>
                        <li>Keep the Agent interface open.</li>
                        <li>Log in to infrastructure (the HPC).</li>
                        <li>In theory, you can run the agent from anywhere on the HPC. but you can see best practices for some recommendations.</li>
                        <li>Copy the usage script from the Agent interface to any text editor and edit the Access token to provide your own token created above and provide the path to the work directory for the agent.</li>
                        <li>The work directory for the Agent (provided as a parameter in the command) must exist before running the agent.</li>
                        <li>Run the edited script relevant to your infrastructure (PBS or SLURM) bash.</li>
                        <li>This script will download the Tower Agent script to the current work directory on the HPC and make it executable.</li>
                        <li>Then, it runs the Agent by providing the connection id and access token.</li>
                        <li>You can see the Agent running on the terminal. Keep it running.</li>
                        <li>Back in the Tower interface, click <code>Add</code> to save your credential.</li>
                    </ol>
                </li>
            </ol>
            <p>The steps above will help to create the credentials and understand the Agent&rsquo;s parameters and how it runs. In practice, this can be better optimised by having all scripts and tokens in config files and bash scripts. See best practice recommendations. The procedure is also described in the Tower documentation at <a href="https://help.tower.nf/latest/agent/#quickstart">Quick Start</a>.</p>
            <div class="alert alert-primary" role="alert">
            <h4 class="alert-heading">Note</h4>
            <p>Users of the same workspace share credentials, so there is no need to create a credential per user within a workspace.</p>
            <hr>
            <p>You might need to create multiple credentials for different compute environments. For example, credentials for your institutional HPC and another credential for AWS account or another national HPC.</p>
            </div>
          </div>
        </div>
    </div>
    <div class="accordion-item">
        <h2 class="accordion-header" id="heading-cop-env" style="margin-top:0rem">
          <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#collapse-cop-env" aria-expanded="false" aria-controls="collapse-cop-env">
            Configuring compute environment 
          </button>
        </h2>
        <div id="collapse-cop-env" class="accordion-collapse collapse" aria-labelledby="heading-cop-env" data-bs-parent="#accordion-comp-env-all">
          <div class="accordion-body">
            <ol>
                <li>Navigate back to the launchpad page for the workspace you want to add a compute environment to.</li>
                <li>Select the Compute Environments tab in the top navigation bar </li>
                <li>Select <code>Add Compute Environment</code> button </li>
                <li>Give the environment a name
                    <ul>
                        <li>Make it as descriptive as you like</li>
                        <li>For HPC you may wish to configure different compute environments for different project codes, so you could include this in the environment name to easily identify it. For example, specify the name of the HPC and the relevant project code</li>    
                    </ul>                   
                    <br/>
                    <div style="text-align:center"><img width="50%" src="../assets/doc_img/com-env.png"/></div>
                    <br/>
                </li>
                <li> Select a platform 
                    <ul>
                        <li> This will depend on which infrastructure you are running and what workload managers are available there.</li>
                        <li>Examples: For Setonix- SLURM, for Gadi PBSpro.</li>
                    </ul>
                </li>
                <li>Select workdirectory 
                    <ul>
                        <li>This can remain as $TW_AGENT_WORK or specify your own</li>
                    </ul>
                </li>
                <li>Leave the launch directory field empty.</li>
				<li>Provide the launch and compute queue (as available on the HPC).
                    <ul>
                        <li>We recommend using a queue with long wall time for the launch queue as this is dedicated to the nextflow main process that should run for the whole time of the pipeline execution. </li>
                        <li>Compute queue will be used for the tasks of the pipeline so we recommend using the default queue on the HPC.</li>
                        <li>The compute queue can be reconfigured during the execution through the pipeline configuration options.</li>
                    </ul>
                </li>
                <li>Select staging options. Under Pre-run script:
                    <ul>
                        <li>Here you can provide all commands to be executed on the HPC before launching the pipeline including module loading.</li>
                        <li>Usually you will need to load Nextflow, singularity, conda, awscli .. if any of them will be used.</li>
                    </ul>
                </li>
                <li>Specify advanced options
                    <ul>
                        <li>Under head job submit options add project specific and queue data. This configuration is for the job that runs the main nextflow process.</li>
                        <li>It is recommended to use 2 cpus and 8 GB memory for this job.</li>
                        <li>Apply head job submit options to compute jobs to ensure your account details get passed on </li>
                    </ul>
                </li>
                <li>Click on <code>Add</code> and the compute environment will be created.</li>
            </ol>
		  </div>
		</div>
	</div>
</div>


### Utilising Compute envornment with tower agent

There are few points to be considered when using tower agent

1. The users of a workspace will share the same compute environment and credentials.
2. Each user needs to create their own personal access token.
3. Each user needs to run Tower agent on their account on the HPC.
4. Each user needs to pass their personal access token and the shared connection id (of the credential) to their instance of tower agent on the HPC.

To do that:

1. Create a personal access token or use a pre-created access token as described here (access1).
2. Obtain the connection id for the compote environment from its credential page (conn_id).
3. Run Tower agent using access1 and conn_id, and an independent work directory (any directory you have access to).
4. The compute environment will be available and usable as long as the agent is running.

<div class="alert alert-primary" role="alert">
    <h4 class="alert-heading">Note</h4>
     <p>Tower agent does not support service accounts on the HPC. In other words, you can not use one agent for multiple users on tower.</p>
     <hr>
     <p>The agent should be able to access the internet.</p>
</div>

## Configuring Commerical cloud

The easiest way is using AWS Batch and tower forge permissions to allow tower to create the batch environment. In order to do this please follow this [documentation](https://help.tower.nf/latest/compute-envs/aws-batch/).

Other Compute infrastructures such Azure and others: Please visit [Tower documentation](https://help.tower.nf/latest/compute-envs/overview/) for more details.
 
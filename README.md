## bioinformatics workflow and pipeline framework

--------

### scripts

Scripts, written in Unix shell or other scripting language such as perl or python could be treated as basic form of pipeline framework. In particular, the robustness feature could be brittle and dependencies refer to upstream and downstream of this pipeline need to be solved manually by authors themselves. Also reentrancy, that the framework recovers from last interrupted point, could be  difficult to implement.

For example: [Redundans](https://github.com/lpryszcz/redundans) is a pipeline that assists an assembly of heterozygous/polymorphic genomes. To run this pipeline, your **OS** needs to satisfy the prerequisites and  by typing the command in terminal the pipeline begins to run until it generates the output or is interrupted by exception.

Recently, as docker container technology becomes more and more popular, so lots of these pipelines could be packaged into images in order to avoid additional installment.  

### make

Make utility is successfully used to manage file transformations common to scientific computing pipelines. It introduces the concept of 'implicit wild card rules', which searches file and dependencies based on file suffixes. However, make itself is not defined for scientific pipelines, as a result, it has several limitations,  such as no built-in support for distributed computing, lacking of powerful data structures as well as impossible sophisticated logic implementation, making it impractical for modern bioinformatics analysis.

------

### [Arvados](https://arvados.org/)

[github](https://github.com/curoverse/arvados)

It enables you to quickly begin using cloud computing resources in your data science work and allows you to track your methods and datasets, share them and re-run analysis.

* Syntax: Explicit
* Paradigm: Configuration
* Interaction: CLI
* Distributed Computing Support: Yes, [Curoverse](https://cloud.curoverse.com/) [document](http://doc.arvados.org/user/tutorials/tutorial-workflow-workbench.html) 
* Extensive: [SDK](http://doc.arvados.org/sdk/index.html)
* Language: Python, Go, Ruby
* License: AGPL-3.0 Apache-2.0 CC-BY-SA-3.0 [github](https://github.com/curoverse/arvados/blob/master/COPYING)
* Pros: CWL and YAML are supported, runtime environment is packaged into docker image
* Cons: Compute nodes must have Docker installed to run containers. So root is required.

------

### [Taverna](https://taverna.incubator.apache.org/) 

[apache git](http://git.apache.org/)

Taverna Workbench is a redesign of the Taverna Workbench 1.7.x series from the ground up. In addition to the improvements to the engine, Taverna Workbench provides more support for workflow design with a graphical workflow editor for direct manipulation of the workflow diagram, context-specific views over Web services and other resources, and standard editing facilities such as copy/paste and undo/redo.

* Syntax: Explicit
* Paradigm: Configuration
* Interaction: CLI [Apache Taverna Command-line Tool](https://taverna.incubator.apache.org/download/commandline) & workbench  [Taverna Workbench](https://taverna.incubator.apache.org/download/workbench) 
* Distributed Computing Support:  Yes, [Service Sets](https://taverna.incubator.apache.org/documentation/service-sets/) [(WSDL based)](https://taverna.incubator.apache.org/documentation/web-service-developers/) 
* Extensive: [SDK](https://taverna.incubator.apache.org/javadoc/)
* Language: Java
* License: Apache License 2.0
* Pros: [Data viewer](https://taverna.incubator.apache.org/documentation/dataviewer-tool/) for viewing result.  [Provenance Management](https://taverna.incubator.apache.org/documentation/provenance/) , which could capture the provenance of workflow definations, workflow runs and data. Capturing everything generated during the runtime.  [Taverna Player](https://taverna.incubator.apache.org/documentation/taverna-player/) is web-based interface for executing existing workflows with new data. Taverna Server is used as the back end processing server.  [Taverna Language](https://taverna.incubator.apache.org/documentation/scufl2/) is  a Java API that gives programmatic access to inspecting, modifying and converting [SCUFL2](https://taverna.incubator.apache.org/documentation/scufl2/) workflow definitions and [Research Object Bundles](https://w3id.org/bundle).
* Cons: It seems that only several service sets are available and it is difficult to create your own service based on current documents. Additional language learning for pipe development.

------

### [Galaxy](https://galaxyproject.org/) 

[github](https://github.com/galaxyproject/galaxy)

Galaxy is an open, web-based platform for accessible, reproducible, and transparent computational biomedical research.

1. Accessible: Users without programming experience can easily specify parameters and run tools and workflows.
2. Reproducible: Galaxy captures information so that any user can repeat and understand a complete computational analysis.
3. Transparent: Users share and publish analyses via the web and create Pages, interactive, web-based documents that describe a complete analysis.

* Syntax: Explicit

* Paradigm: Configuration

* Interaction: workbench

* Distributed Computing Support: Yes, [CloudMan](https://galaxyproject.org/cloudman/) 

* Extensive: [API](https://galaxyproject.org/develop/api/)

* Language: Python

* License: Academic Free License version 3.0

* Pros: Integrated graphics interface and visualization tools, easy drag. There are several programing language bindings for galaxy api. [document](https://galaxyproject.org/develop/api/#programming-language-bindings)  includes Java, Php, Python, Javascript, CLI

* Cons: By default, one could deploy galaxy on AWS, Jetstream cloud and etc. Following [document](https://galaxyproject.org/cloudman/building/) to create private cloud, one needs to build galaxyIndicesFS, install dependencies and start relative services, which may need some time and root privileges.  

  ------

### [Agave](http://developer.agaveapi.co/)

  [github](https://github.com/agaveapi)

  The Agave Platform is an open source, science-as-a-service API platform for powering your digital lab. Agave allows you to bring together your public, private, and shared high performancecomputing (HPC), high throughput computing (HTC), Cloud, and Big Data resources under a single, web-friendly REST API.

  1. Run code

  2. Manage data

  3. Collaborate meaningfully

  4. Integrate anywhere

     ​

  - Syntax: Explicit

  - Paradigm: Configuration

  - Interaction: [CLI](http://developer.agaveapi.co/?plaintext#jupyter-hub) and [Agave ToGo](http://togo.agaveapi.co/)

  - Distributed Computing Support: Yes, [Execution Sys Config](http://developer.agaveapi.co/?plaintext#execution-systems) 

    - HPC, Condor -> batch scheduler
    - CLI -> processes

  - Extensive: [Web API](http://developer.agaveapi.co/?plaintext#web-api)

  - Language: Php, Java

  - License: Unkown

  - Pros: JSON file is used to configure everything. Core service is deployed and distributed by docker images.[github](https://github.com/agaveapi/core-services) . It has a file service to manage the data storage, and the system itself will transfer data and ensure it completes. It has a angular-js based web administration console. 

  - Cons: It implements basic functions of workflow system but doesn't have reproducible feature. Data will be transfered among nodes and may be improper for huge data. Docker is used and root privileges may be required.

    ------

### [Snakemake](https://bitbucket.org/snakemake/snakemake)

The Snakemake workflow management system is a tool to create reproducible and scalable data analyses. Workflows are described via a human readable, Python based language. They can be seamlessly scaled to server, cluster, grid and cloud  environments, without the need to modify the workflow definition. Finally, Snakemake workflows can entail a description of required software, which will be automatically deployed to any execution environment.

  - Syntax: Implicit

  - Paradigm: Configuration

  - Interaction: [CLI](https://snakemake.readthedocs.io/en/latest/executable.html#useful-command-line-arguments) 

  - Distributed Computing Support: Yes, Kubernetes, Singularity, Docker

  - Extensive: [API](https://snakemake.readthedocs.io/en/latest/api_reference/snakemake.html) 

  - Language: Python

  - License:  MIT License

  - Pros: Packages are managed by conda. Google cloud engine is supported and cluster execution is easily integrated. DAG is introduced to visualize workflow. Configuration is based on YAML or JSON. Sustainable and reproducible archiving. Scheduling algorithm provides general support for distributed computing.

  - Cons: Extended Backus-Naur form ([EBNF](https://snakemake.readthedocs.io/en/latest/snakefiles/writing_snakefiles.html)) is needed to learn to write pipelines. No other languages are supported. No community of sharing pipelines written and ran on snakemake.  Cloud file or storage management?

    ------

### [Bpipe](http://docs.bpipe.org/)

[github](https://github.com/ssadedin/bpipe/)

1. Simple definition of tasks to run - Bpipe runs shell commands almost as-is - no programming required.

2. Transactional management of tasks - commands that fail get outputs cleaned up, log files saved and the pipeline cleanly aborted.  No out of control jobs going crazy.

3. Automatic Connection of Pipeline Stages -  Bpipe manages the file names for input and output of each stage in a systematic way so that you don't need to think about it.  Removing or adding new stages "just works" and never breaks the flow of data.

4. Easy Restarting of Jobs - when a job fails cleanly restart from the point of failure.

5. Easy Parallelism - Bpipe makes it simple to split jobs into many pieces and run them all in parallel whether on a cluster or locally on your own machine

6. Audit Trail - Bpipe keeps a journal of exactly which commands executed and what their inputs and outputs were.

7. Integration with Cluster Resource Managers - if you use Torque PBS, Oracle Grid Engine or Platform LSF then Bpipe will make your life easier by allowing pure Bpipe scripts to run on your cluster virtually unchanged from how you run them locally.

8. Notifications by Email or Instant Message - Bpipe can send you alerts to tell you when your pipeline finishes or even as each stage completes.

   ​

   * Syntax: Explicit

   - Paradigm: Class

   - Interaction: [CLI](http://docs.bpipe.org/Commands/Commands/) 

   - Distributed Computing Support:  Partially?  Based on the [document](http://docs.bpipe.org/Guides/ParallelTasks/), it seems that the parallel tasks are executed in small-scale. 

   - Extensive: NA

   - Language: Groovy

   - License:  BSD 3-clause "New" or "Revised" License

   - Pros: Tiny, low-level and efficient. No needs to learn any other languages while it supports executing several embedded languages. Auditing every commands pipelines executed and recovering from interruption and error. Pipelines are written through combination of inner commands.

   - Cons: Compared to other workflows, it doesn't provide any gui interactions, visualization of workflows or results, sharable feature and container based dispatch feature. Also the small-scale parallel tasks are not fully distributed ones? 

     ------

### [Ruffus](http://www.ruffus.org.uk/installation.html)
[github](https://github.com/bunbun/ruffus)

The ruffus module has the following design goals:

1. Simplicity. Can be picked up in 10 minutes
2. Elegance
3. Light weight
4. Unintrusive
5. Flexible/Powerful

Automatic support for

1. Managing dependencies
2. Parallel jobs
3. Re-starting from arbitrary points, especially after errors
4. Display of the pipeline as a flowchart
5. Reporting

- Syntax: Explicit


- Paradigm: Class
- Interaction: [CLI](http://www.ruffus.org.uk/tutorials/new_tutorial/manual_contents.html)
- Distributed Computing Support:  Yes, It uses python multiprocessing to run each job in a separate process. From version 2.4 onwards, it includes Open Grid Forum API specification.
- Extensive: NA
- Language: Python
- License:  MIT License
- Pros: Lightweight, elegance and distributed computing supporting. Easy for the guys familiar with python development.
- Cons: No visualization of result or workflows. Requiring python development knowledge. Pip and easy_installl dependencies. [Official Todo](http://www.ruffus.org.uk/todo.html)

------

### [Nextflow](https://www.nextflow.io/)

[github](https://github.com/nextflow-io/nextflow)

Nextflow framework is based on the *dataflow* programming model, which greatly simplifies writing parallel and distributed pipelines without adding unnecessary complexity and letting you concentrate on the flow of data, i.e. the functional logic of the application/algorithm. Nextflow script is defined by composing  many different processes. Each process can be written in any scripting language that can be executed by the Linux platform (BASH, Perl, Ruby, Python, etc), to which is added the ability to coordinate and synchronize the processes execution by simply specifying their inputs and outputs.

Feature:

1. Fast prototyping, Nextflow allows you to write a computational pipeline by making it simpler to put together many different tasks.
2. Reproducibility, docker and singularity supported.
3. Portable, it provides abstraction layers between pipeline's logic and the execution layer.
4. Unified parallelism, it is based on dataflow programing model simplifying writing complex pipelines.
5. Continuous checkpoints, all the intermediate results are tracked.
6. Stream oriented, it extends the Unix pipes model with a fluent DSL.

- Syntax: Implicit


- Paradigm: Class

- Interaction: CLI

- Distributed Computing Support:  Yes, it provides out of box support for SGE, LSF, SLURM, PBS and HTCondor batch schedulers and for kubernetes and AWS 

- Extensive: NA

- Language: Groovy

- License:  GNU GPLv3 License

- Pros: Powerful, it includes lots of features such as cluster support, execution report, resources and task report, pipelines sharing and container technology support. Groovy based language development for pipelines, quite easy to write and read. [CWL support](https://github.com/nextflow-io/cwl2nxf). Multiple scripts running on unix platform supports including python, ruby, bash and etc. 

- Cons: No rootless container support, many dependencies including apache ignite and jdk.

  ------

### [BioQueue](https://github.com/liyao001/BioQueue)

BioQueue is a lightweight and easy-to-use queue system to accelerate the proceeding of bioinformatic workflows. Based on machine learning methods, BioQueue can maximize the efficiency, and at the same time, it also reduces the possibility of errors caused by unsupervised concurrency (like memory overflow). BioQueue can both run on POSIX 
compatible systems (Linux, Solaris, OS X, etc.) and Windows.

- Syntax: Implicit


- Paradigm: Class
- Interaction: CLI and GUI(Web-based)
- Distributed Computing Support:  Yes, [document](http://bioqueue.readthedocs.io/en/latest/cluster.html#how-to-use-bioqueue-on-clusters)
- Extensive: API
- Language: Python
- License:  Apache License 2.0
- Pros: Machine learning method is introduced to estimate the resource usage(CPU,memory and disk) needed by each step. It possesses a shell command-like syntax instead of implementing a new script language. Reading and writing to sqlite rather than disk files.
- Cons: Lack of some features such as pipelines sharing and container technology. Also the performance and accuracy of  resource usage estimation is not tested.


------

### [Cluster Flow](http://clusterflow.io/)

[github](https://github.com/ewels/clusterflow)

Cluster Flow is designed to be quick and easy to install, with flexible configuration and simple customization.

1. Simple. Installation walkthroughs and a large module toolset mean you get up and running quickly.
2. Powerful. Comes packaged with support for 24 different bioinformatics tools (RNA, ChIP, Bisulfite and more).
3. Flexibile. Pipelines are fast to assemble, making it trivial to change on the fly.
4. Traceable. Commands, software versions, everything is logged for reproducability.

- Syntax: Implicit


- Paradigm: Class

- Interaction: CLI

- Distributed Computing Support:  Yes, It supports the sun GRidEngine, LSF and SLURM job managers.

- Extensive: NA

- Language: Perl

- License:  GNU General Public License v3.0

- Pros: Simple, it is a complex perl script requiring basic core perl packages, which makes it runnable on most machines. 

- Cons: Currently, it supports a list of [tools](https://github.com/ewels/clusterflow) . For cluster, one needs to configure it manually such as resource estimation and environment configuration. 

  -------

### [Toil](http://toil.ucsc-cgl.org/)
[github](https://github.com/BD2KGenomics/toil)

A scalable, efficient, cross-platform pipeline management system written entirely in Python and designed around the principles of functional programming.

1. Pythonic. Easily mastered, the Python user API for defining and running workflows is built on one core class. Also, everything is open source under the Apache License.
2. Robust. Toil workflows support arbitrary worker and leader failure, with strong check-pointing that always allows resumption.
3. Efficient. Caching, fine grained, per task, resource requirement specifications, and support for the AWS spot market mean workflows can be executed with little waste.
4. Built for the cloud. Develop and test on your laptop, then deploy on Microsoft Azure, Amazon Web Services (including the spot market), Google Compute Engine, OpenStack, or on an individual machine.
5. Strongly scalable. Build a workflow on your laptop, then scale to the cloud and run it concurrently on hundreds of nodes and thousands of cores with ease. We've tested it with [32,000 preemptable cores](http://biorxiv.org/content/early/2016/07/07/062497) so far, but Toil can handle more.
6. Service integration. Toil plays nice with databases and services, such as Apache Spark. Service clusters can be created quickly and easily integrated with a Toil workflow, with precisely defined start and end times that fits with the flow of other jobs in the workflow.

- Syntax: Implicit


- Paradigm: Class

- Interaction: CLI

- Distributed Computing Support:  Yes, it supports AWS, Azure, Openstack, GCE and HPC.

- Extensive: [API](http://toil.readthedocs.io/en/latest/developingWorkflows/toilAPI.html)

- Language: Python

- License:  Apache License, Version 2.0

- Pros: Full features support, including reproducibility, cloud and container technology support. CWL is supported. 

- Cons:  No multiple languages supported. No visualization of workflows or report. Pythonic development requires package dependencies management and pip or easy_install tools dependencies.

  --------

### [Bcbio](https://bcbio-nextgen.readthedocs.io/en/latest/)
[github](https://github.com/chapmanb/bcbio-nextgen)

Validated, scalable, community developed variant calling, RNA-seq and small RNA analysis. You write a high level configuration file specifying your inputs and analysis parameters. This input drives a parallel run that handles distributed execution, idempotent processing restarts and safe transactional steps. bcbio provides a shared community resource that handles the data processing component of sequencing analysis, providing researchers with more time to focus on the downstream biology.

1. Community developed: We welcome contributors with the goal of overcoming the biological, algorithmic and computational challenges that face individual developers working on complex pipelines in quickly changing research areas. See our [users page](https://bcbio-nextgen.readthedocs.org/en/latest/contents/introduction.html#users) for examples of bcbio-nextgen deployments, and the [developer documentation](https://bcbio-nextgen.readthedocs.org/en/latest/contents/code.html) for tips on contributing.

2. Installation: [A single installer script](https://bcbio-nextgen.readthedocs.org/en/latest/contents/installation.html#automated) prepares all third party software, data libraries and system configuration files.

3. [Automated validation](http://bcb.io/2014/05/12/wgs-trio-variant-evaluation/): Compare variant calls against common reference materials or sample specific SNP arrays to ensure call correctness.Incorporation of multiple approaches for alignment, preparation and variant calling enable unbiased comparisons of algorithms.

4. Distributed: Focus on [parallel analysis and scaling](http://bcb.io/2013/05/22/scaling-variant-detection-pipelines-for-whole-genome-sequencing-analysis/) to handle large population studies and whole genome analysis. Runs on single multi-core computers, in compute clusters using [IPython parallel](http://ipython.org/ipython-doc/dev/index.html),or on the Amazon cloud. See the [parallel documentation](https://bcbio-nextgen.readthedocs.org/en/latest/contents/parallel.html) for full details.

5. Multiple analysis algorithms: bcbio-nextgen provides configurable[variant calling, RNA-seq and small RNA pipelines](https://bcbio-nextgen.readthedocs.org/en/latest/contents/pipelines.html).

   - Syntax: Implicit


   - Paradigm: Class
   - Interaction: CLI
   - Distributed Computing Support:  Yes, it supports AWS, Azure, Openstack, GCE and HPC.
   - Extensive: [API](http://toil.readthedocs.io/en/latest/developingWorkflows/toilAPI.html)
   - Language: Python
   - License:  Apache License, Version 2.0
   - Pros: Full features support, including reproducibility, cloud and container technology support. CWL is supported. 
   - Cons:  No multiple languages supported. No visualization of workflows or report. Pythonic development requires package dependencies management and pip or easy_install tools dependencies.
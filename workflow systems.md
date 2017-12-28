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

   - Syntax: Explicit
   - Paradigm: Class
   - Interaction: [CLI](http://docs.bpipe.org/Commands/Commands/) 
   - Distributed Computing Support:  Partially? 
   - Extensive: [API](https://snakemake.readthedocs.io/en/latest/api_reference/snakemake.html) 
   - Language: Python
   - License:  MIT License
   - Pros: Packages are managed by conda. Google cloud engine is supported and cluster execution is easily integrated. DAG is introduced to visualize workflow. Configuration is based on YAML or JSON. Sustainable and reproducible archiving. Scheduling algorithm provides general support for distributed computing.
   - Cons: Extended Backus-Naur form ([EBNF](https://snakemake.readthedocs.io/en/latest/snakefiles/writing_snakefiles.html)) is needed to learn to write pipelines. No other languages are supported. No community of sharing pipelines written and ran on snakemake.  Cloud file or storage management?
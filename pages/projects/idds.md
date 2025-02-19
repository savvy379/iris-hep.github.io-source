---
permalink: /projects/idds.html
layout: project
title: Intelligent Data Delivery Service
shortname: idds
pagetype: project
image: logos/idds.png
blurb: Delivering Data.  Better.
maturity: Deployed
maturity-note:
focus-area: doma
team:
 - bbockelm
 - wguan
 - Tadashi Maeno
 - Rui Zhang
 - Tuan Minh Pham
---

The intelligent Data Delivery Service (iDDS) is a general service to orchestrate the workload management system and data management system with generalized workflows, and to transform and deliver needed data to consumers, in order to improve the workflow between the workload management system and the data management system.

The IDDS work is an ongoing joint project within IRIS-HEP and US ATLAS in the DOMA and
Analysis Systems area, as well as within the HEP Software Foundation
event delivery group.

## R&D Significance and Impact
* *Data Carousel for LHC:* iDDS enables fine-grained prompt processing to efficiently use disk storage. It's already in production for more than 2 years.
* iDDS hyperparameter optimization service is used for the new ML (GAN) based component in production fast simulation (AtlFast3), FastCaloGAN. (effective HPC/GPU utilization, distributed resource utilization for ML)
* iDDS DAG based workflow management in production for Rubin Observatory, joint with PanDA to manage the dependencies of different jobs.
* Ongoing R&D - a growing number of analysis use cases that are demanding in their complexity and resource needs: active learning, toy MC generation, integrated REANA workflows.

## Benefits
* Experiment-agnostic which is already employed by LHC ATLAS and Vera Rubin Observatory, exploring for new directions such as the sPHENIX experiment.
* Fine-grained data carousel workflow addressing the HL-LHC storage challenge to reduce storage usage.
* Scable Machine Learning service to efficiently distribute ML hyperparameter optimization tasks and so on to distributed HPC/GPU resources.
* Complex dynamic workflow management, such as DAG (Directed Acyclic Graphs), Loop workflow, Template workflow and Condition workflow, to automate complex production and analysis workflows. It has been used in different experiments, such as ATLAS Hyper ParameterOptimization, ATLAS Active Learning, ATLAS REANA production+analysis integration workflow, Rubin data processing and near-term sPHENIX processing.
* Operating on grid, commercial clouds, HPCs and etc.
* Futuer development: fine-grained data transformation and delivery for remote analysis.

## Use Cases

 * *[ATLAS Data Carousel](https://aipanda181.cern.ch/monitor/)*:
    If HL-LHC is going to process exabytes of data, it needs data access systems
that can deliver.  The iDDS attempts to make the workflow system more aware of
the data workflows and get data processed more effectively. The ATLAS "data carousel"
 is the initial use case for iDDS. It orchestrates the processing of data as soon as
 it comes out of archival systems instead of waiting for entire datasets to be staged.  This minimizes
the use of disk buffers -- especially relevant for HL-LHC as the size of the
disk buffer shrinks compared to the total dataset volumes.

   iDDS performs the fine grained choreography between the processing workflow and dataflow management, initiating processing and deletion quickly at the file level when the data is staged from the tape, rather than when the entire datasets reach the disk as in the pre-iDDS system.
   ATLAS has been expanding the number of workflows using data carousel, now extending to most production workflows. The iDDS minimizes the delay between data being staged and being processing, reducing the data pinning time so that it can be deleted as soon as possible if required, so that it reduces the storage usage.

   Over the two years that the iDDS-enabled data carousel has been in production. Several hundreds of PB data has been processed.
   (The monitor snapshot below only shows data from July 2021. The data before it is already archived.)
   ![iDDS ATLAS Data Carousel](/assets/images/idds_atlas_data_carousel.jpg){:style="display:block; margin-left: auto; margin-right: auto; width: 75%"}


 * *Hyper Parameter Optimization (HPO)*:
   HPO is a scable machine learning service to efficiently distribute ML tasks to distributed HPC/GPU resources. It is an interest to both HL-LHC Computing R&D and ML-based analysis for the potential to use large scale computing resources, such as HPCs and distributed GPUs, to reduce latencies within the development and refinement of ML applications by order of magnitude.

   iDDS HPO, integrated with PanDA workload management system, has provides a fully-automated platform for ML hyper parameter optimization, and also similar tasks, on top of geographically distributed GPU resources on the grid, HPC, and clouds.

   The PanDA/iDDS based ML service is the basis for optimizing the first ML application to reach production in the ATLAS fast simulation; the new AtlFast3 simulation that began production in 2021 incorporates FastCaloGAN, which uses PanDA/iDDS to accelerate its optimization of 300 neural networks requiring 100 GPU-days for a single pass.

   Recently a new use case of the MC toy based confidence limits estimation, has adapted to use the iDDS HPO framework to manage its toy generation workflow with multiple steps.

   Future development: apply Jupyter and container to simplify the user interface and the ML environment management.

 * *[DAG based workflow management](https://aipanda017.cern.ch/monitor/dashboard.html)*:
   To meet the requirements of the Rubin Observatory's workflows which are defined as DAGs.
   The iDDS internally implements a high-level workflow engine, specifying a set of
   interdependent jobs as described by DAG. iDDS, interacting
   with software such as PanDA, drives workload scheduling and implements
   management of job chains for multi-step processing with thousands of jobs
   per step.

   The iDDS DAG is motivated by Rubin. It enabled the smooth integration of PanDA into Rubin's
   workflow and middleware, which together with successful PanDA scaling tests was instrumental
   in Rubin's adoption of PanDA and iDDS in August 2021.

   ![iDDS ATLAS DOMA Rubin](/assets/images/idds_doma_rubin.jpg){:style="display:block; margin-left: auto; margin-right: auto; width: 75%"}

   The DAG support then catalyzed a rapid proliferation of implemented complex workflows
   of interests to the ATLAS HL-LHC computing R&D and analysis communities. To enhance the
   workflow management, iDDS has implemented complex, dynamic workflow management such as
   Loop workflow, Template workflow and Condition workflow, to meet the requirements of
   some applications such as ATLAS Active Learning. The iDDS workflow management has been used
   to support a still growing succession of complex workflow management applications, such as
   ATLAS MC toy based confience limits, ATLAS REANA production and analysis integration, and sPHINX workflow management.

 * *Monte Carlo Toy Based Confidence Limits with iDDS*: An efficient Monte Carlo
   Toy generation process requires multiple steps of grid scans, where current steps
   depends on the previous steps. The HPO framework is employed to provide a
   fully-automated platform for Toy generations.

   The test workflow has passed successfully. Working on documenting and client integration.
   Will advertise it to users soon.

 * *REANA/PanDA/iDDS integration for Active Learning*: Active Learning is one of the ideas
   that require complex logics between tasks in an analysis workflow. Here we employ iDDS
   for workflow managements, PanDA for task management and REANA (Reusable Analyses) for
   analysis tasks executions.

   The demo workflow has passed the tests successfully. Working to adapt real analysis
   workflows.

 * *sPHENIX workflow management*: The sPHENIX is also starting to test to use iDDS/PanDA for
   its workflow management.

## Architecture: [reference vCHEP2021](https://arxiv.org/pdf/2103.00523.pdf)
![iDDS Architecture](/assets/images/idds_architecture.png){:style="display:block; margin-left: auto; margin-right: auto; width: 50%"}

## Reference
 * *[Home page](https://iddsserver.cern.ch/website/)*
 * *[Code at github](https://github.com/HSF/iDDS)*
 * *[Documents at readthedocs](https://idds.readthedocs.io)*
 * *[ATLAS instance monitor](https://aipanda181.cern.ch/monitor/)*, *[ATLAS request monitor](https://bigpanda.cern.ch/idds)*
 * *[DOMA instance monitor](https://aipanda017.cern.ch/monitor/dashboard.html)*, *[DOMA request monitor](https://panda-doma.cern.ch/idds/)*, *[DOMA workflow monitor](https://panda-doma.cern.ch/idds/wfprogress/)*

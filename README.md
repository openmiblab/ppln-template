# Template repository for miblab pipelines

## Repository naming convention

Naming convention: miblab pipelines always have a repository name that starts with *ppln-*. After this can be just one string (lowercase) for simple standalone pipelines, such as *ppln-template*. 

For pipelines that are part of a project you would list the project name, followed by a dash and the pipeline name, like *ppln-project_name-pipeline_name*. 

Note parts of the name are separated by underscores rather than dashes.

## Header files

At the top level you will find some essential files that each pipeline needs to have:

- .zenodo.json: header information used when releasing to Zenodo.
- env.yml: conda environment listing all required packages
- LICENSE: always Apache 2.0
- pyproject.toml: header file that allows the pipeline to be installed 
  from source.
- README.md: some explanation for pipeline users.

## The src folder

The subfolder **src** is required, and contains the pipeline source code. 

It needs to have a subfolder with the full name of the pipeline. If the repository is of the form *ppln-template* this would be *template*. If the repository is of the form *ppln-project_name-pipeline_name* this would be *project_name_pipeline_name*. Note dashes are replaced by underscores here.

At the top level, **src/pipeline_name** has the top level scripts for the individual stages, always named as "stage_xx_name.py", and the complete pipeline named ppln.py. Please refer to the templates for the typical structure of stages and pipelines.

If functions are shared between stages, they need to be stored in separate modules in **src/pipeline_name/utils**, and imported. 

At some point you may find that certain utilities need to be shared between  pipelines. In that case they need to be moved into stand-alone packages, that can eventually mature into a new python package. 

## The hpc folder

This is only required for pipelines that are intended to run on the HPC, and contain the SLURM scripts to run the stages (stg.sh) or pipeline (ppln.sh), and archive the results (arxv.sh). Archiving can also be done in the same script as illustrated in stg.sh. 

Note the SLURM scripts are templates and details about path information etc will need to be updated for the pipeline.


## Installation

To run the pipeline, first install the conda environment. Navigate to the top folder **ppln-template** and go:

```bash
conda env create -n template -f env.yml
```

This will create an environment named *template* with the packages specified in the file *env.yml*.

Then activate it:

```bash
conda activate template
```

## Running individual stages

To run an individual stage, first change the path to the **BUILD** folder of the scripts **stage_1_hello_world.py** and **stage_2_hello_world_back.py**.

Then you can run:

```bash
python "src/template/stage_1_hello_world.py"
```

and:


```bash
python "src/template/stage_2_hello_world_back.py"
```





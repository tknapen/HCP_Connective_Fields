# HCP_Connective_Fields

Repo containing code to reproduce figures for the article on retinotopic connectivity [published in PNAS](http://bit.ly/retino_DMN_hippo). 

## Repo being populated

**This repository is being populated by cleaned code from a separate private repository. I apologize for any delay in updating this repository; I'm on paternaty leave right now. **

## Install required packages

The analyses in this repository were run inside a conda environment that can be created as follows; 

```conda create -c intel -n cf_hcp python=3.6 intelpython3_core==2019.5 jupyterlab matplotlib seaborn statsmodels pandas scikit-learn scikit-image cython
conda activate cf_hcp
conda install -c conda-forge nibabel nilearn cifti bottleneck tqdm nistats pingouin
```

It also depends on some non-conda software from other developers: [neuropythy](https://github.com/noahbenson/neuropythy) and [pycortex](https://github.com/gallantlab/pycortex), as well as our own prf-fitting package, [prfpy](https://github.com/VU-Cog-Sci/prfpy).

To install, the following assumes these packages are cloned to the `~/projects/` directory. 

```
cd ~/projects/neuropythy
python setup.py develop

cd ~/projects/prfpy
python setup.py develop

cd ~/projects/pycortex
python setup.py develop

```

## Analysis outline

The custom software that is run to produce the figures in the article is structured as a python package, called `cfhcpy`. This package can be installed from this repository using `python setup.py develop`. The notebooks in the [notebooks](notebooks) folder then run specific parts of the analysis. 

The parameters for the analyses are codified in the [config.yml](config.yml) file in a format that allows annotated versioning of these analysis parameters. That is, in many cases, to change analyses it should suffice to change the settings in the `yaml` file without changing the underlying code. For instance, to set up your own version of the analysis, add a system to this `yaml` file in the *systems* section. Code, where reasonable, is documented in the `numpy` docstring format. 

This `yaml` file is read in by the main analysis class, `AnalysisBase` in [cfhcpy/base.py](cfhcpy/base.py), which can then be used to run per-subject analyses. For group analysis, a similar `GroupAnalysis` class exists in [cfhcpy/group.py](cfhcpy/group.py).


## Cluster 

The fitting of the CF models happens on a SLURM cluster, to which the data are `rsync`ed. To submit jobs and run fitting outside of notebooks, adapt and use the `scripts/submit.py` and `scripts/run.py` scripts.
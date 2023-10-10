# Usage

Here are example notebooks for membrane analyses, and the environments needed.

To start with, please make sure you have a package manager using one of:

* [conda / Anaconda](https://conda.io/projects/conda/en/latest/user-guide/install/index.html) **not recommended due to speed**
* [mamba](https://mamba.readthedocs.io/en/latest/mamba-installation.html#mamba-install)
* [micromamba](https://mamba.readthedocs.io/en/latest/micromamba-installation.html)

Of these, mamba may be the easiest to use. Personally I'm trying out micromamba right now. Whichever one you use, please swap out the `micromamba` in my command below for `conda` or `mamba` as required.


## Installation option 1: create conda environments with installed packages (simple)

*Use this option if you don't expect to edit the lipyds code.*

To run the `membrane_only.ipynb` notebook, please create an environment with **Lipyds software package** by building from the `lipyds-env.yaml` file. This downloads all released software packages, as well as the tagged `v0.0.1-alpha` (guaranteed not to change) version of lipyds.

```bash
micromamba env create -f lipyds-env.yaml
micromamba activate lipyds-env
```

I also like to create a Jupyter kernel to make clear which environment I'm running in:

```bash
python -m ipykernel install --user --name lipyds-env --display-name "Python (lipyds-env)"
```

Then to open the Jupyter notebook and run:

```bash
jupyter notebook membrane_only.ipynb
```

The process is analogous for the other environment, which has an older version of MDAnalysis:

(This is the `slc6-transporters` branch of my fork of MDAnalysis, which I will make best efforts not to change for reproducibility).

```bash
micromamba env create -f old-mdanalysis-env.yaml
micromamba activate old-mda-env
python -m ipykernel install --user --name old-mda-env --display-name "Python (old-mda-env)"
jupyter notebook membrane_and_protein.ipynb
```

## Installation option 2: create conda environments with editable packages (more work)

*Use this option if you do expect to edit the lipyds code and want changes to show up in your environment*.

To do this, use the `*-dev.yaml` versions of each environment.

### Lipyds

Firstly, install dependencies:

```bash
micromamba env create -f lipyds-dev.yaml
micromamba activate lipyds-dev
```

Then clone `lipyds`:

```bash
git clone https://github.com/lilyminium/lipyds.git
```

Install lipyds as an "editable" installation.

```bash
cd lipyds
pip install -e .
```

Now, if you make changes to lipyds code and restart the kernel in your Jupyter notebook with the `lipyds-dev` environment, changes will propagate.

### Old MDAnalysis

Firstly, install dependencies:

```bash
micromamba env create -f old-mdanalysis-dev.yaml
micromamba activate old-mdanalysis-dev
```

Then clone **my fork** of `mdanalysis`:

```bash
git clone https://github.com/lilyminium/mdanalysis.git
```

**Change the branch to the old slc6-transporters branch**:

```bash
cd mdanalysis
git checkout slc6-transporters
```

And install as editable:

```
pip install -e .
```

(**Note** -- all changes will propagate in your Python environment, so if you change branch in this directory, the MDAnalysis available to Jupyter will differ as well!)


## Other tools

Here are other tools I recommend looking at or using:

- [fatslim](https://fatslim.github.io/)
- [lipyphilic](https://lipyphilic.readthedocs.io/en/latest/reference/analyses.html)
- [membrane-curvature](https://membrane-curvature.readthedocs.io/en/latest/index.html)

## Feedback

If you have feedback either on these instructions or on Lipyds, please feel welcome to raise an issue! Tell me what is wrong, what you expected, or what you would like to see either on this issue tracker or the [Lipyds](https://github.com/lilyminium/lipyds/issues?q=is%3Aissue+is%3Aopen+sort%3Aupdated-desc) one. If you have questions, the issue tracker is also a good place for those too, or contact me via email.

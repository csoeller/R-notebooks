# R installation with Jupyter Notebooks

Below I go through the steps I used (on a mac) to install R notebook infrstructure using the jupyter notebook approach.

Once you worked through the steps below you should be able to make new R notebooks from the Jupyter `New Notebook` menu which should allow you to select R, i.e. to open a new R notebook.

## Creating the environment and basic conda installs

```
conda create -n r-stats
conda activate r-stats

conda install -c conda-forge r-recommended
conda install -c conda-forge r-ggplot2
```

## Install some packages using R

Below we install a few extra packages that are mainly useful for plotting which initially is our main motivation in using R. Rather than using `conda` which I found hit-and-miss in working properly for some of the packages, this uses R's builtin `install.packages` command. Below I use the way to this from the (mac) command line, but one can also do this from an R command line directly (e.g. in an RStudio session) and then type at the R command line `install.packages("xxxx")` where `xxxx` is a placeholder for the actual package name, see examples bow.

### [Optional] Startup setting to avoid having to choose repo location each time

As explained in [this post](https://stackoverflow.com/questions/11488174/how-to-select-a-cran-mirror-in-r), it can be useful to set the default repo to autoselect from a close mirror. Otherwise, I always had to manually select a local Swiss mirror from a long list, before the command would execute. I added the following code to `$HOME/.Rprofile`:

```R
## Default repo
local({r <- getOption("repos")
       r["CRAN"] <- "https://cloud.r-project.org" 
       options(repos=r)
})
```

### Packages for quasirandom point plotting

```
R -e 'install.packages("beeswarm")'
R -e 'install.packages("ggbeeswarm")'
```

### Packages for plotting several panels

Note that `gridExtra` is probably superfluous when using `patchwork`. In tests to date just using `patchwork` seemed enough. 

```
R -e 'install.packages("gridExtra")'
R -e 'install.packages("patchwork")'
```

### Package for reading excel data

```
R -e 'install.packages("readxl")'
```



## Conda install of jupyter support and register R kernel

For this last part we are switching back to using `conda`. It seems pretty hassle-free and has always worked when I tried it.

```
conda activate r-stats # activate r-stats env if not already done
conda install -c conda-forge jupyter
conda install -c conda-forge r-irkernel
R -e 'IRkernel::installspec()'
```

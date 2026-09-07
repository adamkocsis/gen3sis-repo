# Repo concent for gen3sis

Sorry - I cannot create a new repo in the org :D Built at <https://adamkocsis.github.io/gen3sis-repo>

This can be an easy v1 of the repo. 
- Publish data on Zenodo, make *gen3sis* organization, collect links.
- Put links in a csv file, make the available on the website.
- Collect links also in the chronosphere, make them accessible R
- Example codes are also provided on the site.

The v2 version can be a full-stack web app instead of the static jekyll site, providing
an API and more advanced searching capabailities. The rest of the pipeline remains the same.


Chronosphere integration:

``` r
# Trial script for accessing gen3sis simulation input through the chronosphere.


# install.packages("chronosphere")
# devtools::install_github("gen3sis2/gen3sis2_R-package@main")
# devtools::install_github("gen3sis2/spac3tools_R-package@decompress-fix")

library(chronosphere) # install from CRAN
library(gen3sis2) # current main 
library(spac3tools) # from current decompress-fix branch!

################################################################################
# IN TEMPORARY DIRECTORY, use datadir to change download dir.
################################################################################

# get a config - on ZENODO SANDBOX
configObject <- chronosphere::fetch(src="gen3sis", ser="hagen2024macro-config_M0")

# FYI: The instruction to cite the chronosphere is scheduled for deletion. Now I find it cheesy,
# I had no time to write an actual paper, and the important thing is that people cite
# the original source of the data.
# In the next version I will ask to put in the acknowledgements instead,
# and rather start counting publications that use it.

# get space, returns a path- on ZENODO SANDBOX
spacePath <- chronosphere::fetch(src="gen3sis", ser="hagen2024macro-space")

## The returned obj. would optimally be of a wrapper class, which includes the path
## to the space ($space) and a path to the resistance matrices in a subdirectory
## ($resistance, if there is any). If this is not there ($resistance is NA), that
## indicates that the line below needs to run. 

# decompress the space
spac3tools::decompress_space(dir_input=spacePath, dir_output=spacePath)

## # ideally this would be:
## spacePathWithResistance <- spac3tools::decompress_space(spacePath)
## # which you would then use as input in the code below to start the simulation.
## # This would be a single space-resistance combination, so 
## spacePathWithResistancesList <- spac3tools::decompress_space(spacePath,
## 		cost_function_index=<vector>)
## # returns a list, you could get spacePathWithResistancesList[[1]], as a specific
## # simulation input.

# run the simulation
sim2 <- gen3sis2::run_simulation(config = configObject,
    space = file.path(spacePath, "decompressed"),
	output_directory = tempdir(), call_observer = 1)
```

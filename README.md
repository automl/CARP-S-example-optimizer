# CARP-S-example-optimizer

This is an example of an optimizer adhering to the [carps](https://github.com/automl/CARP-S) interface
and how this optimizer can be run in carps just via the commandline.
The optimizer here is random search (which is just copy-pasted from carps).

## Installation
```bash
# Create conda env
conda create -n carpsopt python=3.12 -c conda-forge

# Activate env
conda activate carpsopt

# Clone repo
git clone git@github.com:automl/CARP-S-example-optimizer.git
cd CARP-S-example-optimizer

# Install 
pip install -e .
```

## Running a benchmark from carps
The command for running the optimizer on a benchmark, e.g., a BBOB function from carps looks as follows:
```bash
# we need to install the BBOB benchmark requirements
pip install ioh==0.3.14
python -m carps.run 'hydra.searchpath=[pkg://carp_s_example_optimizer/configs]' +myoptimizer/randomsearch=config +problem/BBOB=cfg_2_12_2_1 seed=1
```
The breakdown of the command:
- `'hydra.searchpath=[pkg://carp_s_example_optimizer/configs]'`: Let hydra know where to find the configs of the optimizer package. For this, `carp_s_example_optimizer` needs to be installed. It is in general: pkg://PACKAGE_NAME/PATH_INSIDE_PACKAGE_TO_CONFIGS_FOLDER .
- `+myoptimizer/randomsearch=config`: select an optimizer from your package. Follows the config folder structure in `carp_s_example_optimizer`. Maybe make sure that config folder names don't overlap with carps.
- `+problem/BBOB=cfg_2_12_2_1`: Select a problem. Follows the config folder structure in `carps`. Beware, for other benchmarks you need to install dependencies (check the [repo](https://github.com/automl/CARP-S)).
- `seed=1`: Set the seed to 1. 🙂

Of course, you can also specify the run dir etc.
For more hydra overrides and parallelization, check their [docs/tutorials](https://hydra.cc/docs/advanced/override_grammar/basic/).
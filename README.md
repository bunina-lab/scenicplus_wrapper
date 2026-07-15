# grn-core-wrapper

A minimal Snakemake pipeline with the 6 GRN-core rules from scenicplus (`tf_to_gene`, `region_to_gene`, `eGRN_direct`, `eGRN_extended`, `AUCell_direct`, `AUCell_extended`). It runs against frozen fixture inputs in `data/fixtures/` so the pipeline can be verified deterministically without network access or upstream preprocessing steps.

## Install

```bash
# Create and activate the conda environment
conda env create -f environment/environment.yml
conda activate scenicplus

# Install Python dependencies
python -m pip install --upgrade pip
python -m pip install -r environment/requirements.txt

# pybedtools must be installed separately
python -m pip install "setuptools<70"
python -m pip install --no-build-isolation "pybedtools==0.9.1"

# scenicplus is not on PyPI — install the pinned commit
python -m pip install --no-deps \
  "git+https://github.com/aertslab/scenicplus.git@840dab85de3044846234c157e327b6ea0290abfb"
```

## Run

```bash
snakemake \
  --snakefile workflow/Snakefile \
  --configfile config/config.yaml \
  --directory results \
  --cores 2

python tests/compare_to_control.py
```

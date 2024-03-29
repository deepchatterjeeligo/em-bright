# Changelog

## [1.1.7] - Unreleased

- No changes yet

## [1.1.6] - 2023-08-29

- Documentation updated to include ROC plots from MDC paper.
- Cover the case of `mass2` > `mass1` in `source_classification`.

## [1.1.5] - 2023-08-04

- Split `source_classification_pe` into `source_classification_pe_from_table` and
  `source_classification_pe_from_samples`.
- Use isinstance() instead of type() for flake8

## [1.1.4.post2] - 2023-06-16

- Pin download links that were missed in v1.1.4.

## [1.1.4] - 2023-06-14

- Fix bug where R_ns was using incorrect units (km instead of m) in the case of EOS marginalization.
  This corrects the NSBH HasRemnant prediction using PE posterior with EOS marginalization.
- Improve the performance of `source_classification_pe`

## [1.1.3] - 2023-05-24

- Fetch `spin1z` and `spin2z` keys first from bilby posterior samples files in
  `source_classification_pe`.

## [1.1.2] - 2023-04-14

- Pin scikit-learn to 1.2.1 due to sklearn's model persistence.
- Drop python3.8 support. Add python3.11 testing.
- Make data directory a subpackage, and set package data related variables there.
  This only downloads package data when importing the `ligo.em_bright.data` subpackage.
  (see https://git.ligo.org/emfollow/gwcelery/-/merge_requests/1148)

## [1.1.1] - 2023-02-23

- Bump sklearn to v1.2.1. Retrain classifer

## [1.1.0] - 2023-01-11

- update dependencies due to pipelines failing: astropy, h5py, pandas (commit message mentions scipy, but 
  that is not affected)

## [1.1.0.dev1] - 2022-12-12

- add HasMassGap: `em_bright.source_classification` returns HasNS, HasRemnant, HasMassGap
- modify `dag_writer` to add mass_gap training workflow, add classifiers
- add HasMassGap unittests

## [1.0.5] - 2022-12-10

- Fix typo in redshift function
- Update to sklearn v1.1.3
- add an EoS marginalization option to `source_classification_pe`. EoS
  posterior draws are from Legred et al. (https://zenodo.org/record/6502467#.Y1xFdHbMI2z).
  See https://git.ligo.org/emfollow/em-properties/em-bright/-/merge_requests/39

## [1.0.4] - 2022-10-19

- Update `source_classification_pe` to be compatible with bilby online
  PE format. Deprecate previous LALInference format. This fixes
  KeyError seen in emfollow/gwcelery#475.
- Use ThreadPoolExecutor to download data files in parallel.

## [1.0.3] - 2022-09-07

- Restrict scikit-learn to v1.1.1 due to model persistance 
- Update links to classifiers because project is moved

## [1.0.2] - 2022-07-09

- Add python 3.10 testing
- Bump sklearn version to 1.1. Retrain classifiers.
- Add `request_disk` to the condor submit file. Using 1GB as a start.
- Restrict astropy >= 5.1.

## [1.0.1] - 2022-03-15

- Fix failing test v1.0.0.

## [1.0.0] - 2022-03-15

- Add EoS marginalization to HasNS and HasRemnant. After this, the
  package data will contain classifiers trained on several different
  NS equations of state from literature. The HasNS and HasRemnant score
  will be computed from each, and re-weighted based on the bayes factor
  calculation done by Ghosh et. al. in https://doi.org/10.1103/PhysRevD.104.083003.

- Drop python 3.7 support since IGWN environments no longer support it.

## [0.1.6] - 2022-02-18

- Make htcondor a dev dependency.

## [0.1.5] - 2022-01-18

- implement fetching and caching package data using `astropy.data.utils`.

## [0.1.4] - 2022-01-13

- Update dependencies meeting SCCB requirements.

## [0.1.3] - 2022-01-07

- Re-implement dag writer using htcondor python bindings.
- Remove unnecessary configuration variables from conf.ini.
- Don't package the classifiers; they will be downloaded if not present.
- Add injected redshift to the categorization output.
- Remove pin for astropy.

## [0.1.2] - 2021-10-27

- Handle hdf5 files using context manager.
- Minor bug fixes in handling arrays in `computeDiskMass` code.

## [0.1.1] - 2021-10-06

- Make `source_classification_pe` work for both aligned and precessing cases
- Relax h5py>=2.10.0
- Fix documentation

## [0.1.0] - 2021-09-18

- Port over em-bright functionaility from p-astro SHA 0b9c8247
- Switch to poetry for dependency management and packaging
- Demote data directory from a package stage; use pathlib
- Trim DAG writing script to only em-bright training components
- Remove scikit-learn pin; use latest release
- Retrain and replace classifiers using scikit-learn==0.24.2

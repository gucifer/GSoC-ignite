# GSoC-ignite
This Repository contains the work done during Google Summer of Code 2021 for the Metric Enhancement Project in Pytorch-Ignite.

The Repository is divided into three folders, namely, metrics, examples and tests.

The metric folder contain the distributed implementation and documentation of three metrics, Frechet Inception Distance, Inception Score and mean Average Precision.
- FID PR (merged) - https://github.com/pytorch/ignite/pull/2049/files
- IS PR (merged) - https://github.com/pytorch/ignite/pull/2053/files
- Further work on FID and IS (merged) - https://github.com/pytorch/ignite/pull/2061/files , https://github.com/pytorch/ignite/pull/2094/files
- PPL - a pull request for the PPL has not been made since it is a case specific metric and does not have a more generalized implementation. An example and blog post showing implementation of the same in ignite can be found in the Examples listed below.
- mAP PR (Open) - https://github.com/pytorch/ignite/pull/2130

The tests folder contain the tests written for the above three metrics to test there functionality and compatibility with ignite.

The examples folder contain the Google Colab Notebook examples written for the above three metrics using pytorch-ignite.
- FID/IS Example (Completed) - https://colab.research.google.com/drive/1bMmIbS13y3UCpkl0BwaNiQISXGV5pbxL?usp=sharing
- PPL Example (In progress) (It has been left incomplete as mAP is a higher priority and needs to be done first.) - https://colab.research.google.com/drive/1uqGmxMiEO7iDorrsZd7ccQfwMoGsqmoZ?usp=sharing
- mAP Example (In progress) - https://colab.research.google.com/drive/1SdcNZ57OWPuo_XhNsipIMgFu9o5P51ga?usp=sharing

Note: Further work is being done on PPL Example, mAP PR and mAP Example. This work will be done in the same PR/ Notebook shared here.
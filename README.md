# qceims

Basic wrapper scripts to run QCEIMS in Metacentrum/CERIT-SC

1. copy qceims.in.init to qceims.in in your working dir (with your coord file)
1. run qceims for the initial MD run; set OMP_NUM_THREADS to reasonably low value (4 for small molecules, maybe 8-12 will help for bigger ones)
2. replace qceims.in qceims.in.prod
3. run qceims again to prepare TMPQCEIMS/
4. transfer TMPQCEIMS to Metacentrum storage if not already there
5. run q-batch to submit the jobs
6. run q-result periodically to check progress
7. once you feel happy (enough jobs finished successfully), the results are gathered in TMPQCEIMS/qceims.res

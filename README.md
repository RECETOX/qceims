# qceims

Basic wrapper scripts to run QCEIMS in Metacentrum/CERIT-SC

1. copy qceims.in.init to qceims.in in your working dir (with your coord file)
1. run qceims for the initial MD run; set OMP_NUM_THREADS to reasonably low value (4 for small molecules, maybe 8-12 will help for bigger ones)
2. replace qceims.in qceims.in.prod
3. run qceims again to prepare TMPQCEIMS/
4. transfer TMPQCEIMS to Metacentrum storage if not already there
5. add Orca to path (module add orca-4.2.1), and run qceims in e.g. TMPQCEIMS/TMP.1; kill it (^C) after few seconds and inspect job.last; it may complain about insufficient memory, which makes orca run extremely inefficient:
<pre>
     Warning (ORCA_SCF): Not enough memory available!
     Memory available for SCF calculation:        12288 MB
                    Memory needed (estimated)           :        12307 MB
</pre>
6. add something like 20% to the estimation
7. run "q-batch -m MEMORY_IN_GB" (substituting the required memory size) to submit the jobs
8. run q-result periodically to check progress
9. once you feel happy (enough jobs finished successfully), the results are gathered in TMPQCEIMS/qceims.res

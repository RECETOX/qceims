# qcxms

Basic wrapper scripts to run QCXMS in Metacentrum/CERIT-SC

1. copy `qcxms.in.init` to `qcxms.in` in your working dir (with your coord file)
1. run `qcxms` for the initial MD run; set `OMP_NUM_THREADS` to reasonably low value (4 for small molecules, maybe 8-12 will help for bigger ones)
2. replace `qcxms.in` in your working directory with `qcxms.in.prod`
3. run `qcxms` again to prepare `TMPQCXMS/`
4. transfer `TMPQCXMS` to Metacentrum storage if not already there
5. add Orca 5 to path (`module add orca/orca-5.0.2-intel-19.0.4-byylubw` in Metacentrum), and run qcxms in e.g. `TMPQCXMS/TMP.1`; kill it (^C) after few seconds and inspect `job.last`; it may complain about insufficient memory, which makes orca run extremely inefficient:
<pre>
     Warning (ORCA_SCF): Not enough memory available!
     Memory available for SCF calculation:        12288 MB
                    Memory needed (estimated)           :        12307 MB
</pre>
6. add something like 20% to the estimation
7. run `q-batch -m MEMORY_IN_GB` (substituting the required memory size) to submit the jobs
8. run `q-result` periodically to check progress
9. once you feel happy (enough jobs finished successfully), the results are gathered in `TMPQCXMS/qcxms.res`

The `q-batch` script contains a defaults section:
<pre>
echo QCEIMS=${QCEIMS:=/storage/brno3-cerit/home/ljocha/work/QCxMS-5.1.3}
echo HOURS=${HOURS:=24}
echo SCRATCH_SIZE=${SCRATCH_SIZE:=20gb}
</pre>
Should any of these settings be adjusted, just set the environment variables before running it,
they will be favoured.

QCxMS static binary was downloaded from the [current release](https://github.com/qcxms/QCxMS/releases/latest).

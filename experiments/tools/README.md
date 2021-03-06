# Configuration Options

- `satune.jar` created using Ecilpse IDE with the "Export>Java>Runnable JAR File" menu option which include all the dependencies in the jar.

```shell
(base) ugurko@redacted tools % java -jar satune.jar -h
usage: java -jar satune.jar [options]
    --anneal-neighbor-strat <arg>   The neighbor generation startegy for
                                    simulated annealing: base, greedy,
                                    conservative (default:base)
 -h,--help                          Display usage info.
    --improve                       Run the improvement experiment
    --ml-model <arg>                regression or classification
    --pca                           perform principal component analysis
    --search <arg>                  the search algorithm to use:
                                    anneal,astar,tabu,genetic (default:
                                    anneal)
    --seed <arg>                    numeric value to be used as the seed
                                    of random number generator.
    --threshold <arg>               The threshold value for the
                                    incorrectness score. Should be in the
                                    range of [0,1] for classification, and
                                    in the range aof min and max numeric
                                    values used for regression mapping.
    --tool <arg>                    the subject tool:
                                    cbmc,symbiotic,jayhorn,jbmc
```

Should be run from this directory. Following commands would repeat the SATune executions in the paper with the random seed 1234:
```shell
java -jar satune.jar --tool jarhorn --threshold 1.0 --seed 1234 --search anneal --ml-model classification
java -jar satune.jar --tool jbmc --threshold 1.0 --seed 1234 --search anneal --ml-model classification
java -jar satune.jar --tool cbmc --threshold 1.0 --seed 1234 --search anneal --ml-model classification
java -jar satune.jar --tool symbiotic --threshold 1.0 --seed 1234 --search anneal --ml-model classification
```

Note that, `--threshold 1.0` and `--ml-model classification` parameters are not discussed in the paper (and they have no effect in the algorithm).

## Subject Verification Tools

All verification tools can be downloaded from: https://sv-comp.sosy-lab.org/2019/systems.php

Each subdirectory contain tool specific artifacts:
 - tool/data contains Arff files used in training
 - tool/results contains the ground-truth data pre-arff
 - Config-space-Xopts.txt the configuration space
 - Configs-Xopts-t3-CA-actual.txt sample configurations
  - Configs-Xopts-t3-CA.txt the tiny version of the sample configurations. For artifacts evaluation, the scripts/tools will be using these versions for quicker executions.
 - `run_exp.py` runs the the ground-truth generation dataset.
 - `run_defconfig.py` runs the tools for each benchmark in our sample set using the default configuration in Config-default.txt

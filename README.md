# Hypergraph Partitioning for VLSI: Benchmarks, Code and Leaderboard

Hypergraph Partitioning Leaderboard: Leaderboard of minimum hyperedge cut values for different testcases with multiple imbalance factors.

SpecPart: A Supervised Spectral Framework for Hypergraph Partitioning Solution Improvement

*******************************************************************************************

## Description ##

This repository supports "Data, Benchmarking and Roadmapping" goals for the balanced hypergraph min-cut partitioning problem, which is central to chip design and the divide-and-conquer paradigm. The repository is a one-stop shop" that serves the following purposes.

1. We provide the [ISPD98 benchmarks](https://dl.acm.org/doi/10.1145/274535.274546) (with unit vertex weights and actual vertex weights) and [Titan23 benchmarks](https://www.eecg.utoronto.ca/~kmurray/titan.html) in [hMETIS](http://glaros.dtc.umn.edu/gkhome/metis/hmetis/overview) format. To understand this format please refer to the [hMETIS manual](http://glaros.dtc.umn.edu/gkhome/metis/hmetis/download). 
2. We provde open source code for the Julia implementation of a recent hypergraph partitioning code, [SpecPart](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/SpecPart/SpecPart_final_submission.pdf). We also provide the implementation of CMG (Combinatorial Multigrid) preconditioner with this package. 
3. We provide the best known partitioning solutions for the ISPD98 benchmarks (both with unit vertex weights and actual vertex weights) and the Titan Benchmarks. 
4. We provide a "Golden Evaluator" which processes a partition file to report the cutsize and the block balances. 
5. We provide a leaderboard of minimum hyperedge cutsize values found on the ISPD98 benchmarks and the Titan23 benchmarks. We encourage fellow researchers to update the leaderboard if better solutions are found. 

We hope to see pull requests with new solutions and optimization codes, and will continue to update the repository and leaderboard as we this happens.

## Table of Contents ##

1. [Current file/directory tree](#current-file-directory-tree-and-description) and description
2. (SpecPart-specific) installation and run [instructions](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/tree/main/SpecPart)
3. [Leaderboard](#leaderboards-of-minimum-hyperedge-cut-values) of minimum hyperedge cutsize values
4. [Authors](#authors)

*******************************************************************************************
## Current File/Directory Tree and Description ##

    .
    |── Leaderboard
    |   └── ISPD98_Leaderboard                # Leaderboard of minimum hyperedge cut values for ISPD98 benchmarks (unit vertex weights and actual vertex weights)
    |   └── Titan23_Leaderboard               # Leaderboard of minimum hyperedge cut values for Titan23 benchmarks
    |
    ├── SpecPart                              # SpecPart Implementation
    │   ├── SpectralCommunityDetection
    │   │   ├── cmg                           # Combinatorial Multigrid Implementation
    |
    ├── benchmark                             # hypergraph files for each benchmark
    │   ├── ISPD_benchmark                    # ISPD98 VLSI Circuit Benchmark Suite with unit vertex weights
    │   ├── ISPD_weight_benchmark             # ISPD98 VLSI Circuit Benchmark Suite with actual vertex weights
    │   └── Titan23_benchmark                 # Titan23 Benchmark Suite
    │   
    ├── golden_evaluator                      # script for evaluating partitioning solutions
    │ 
    ├── solutions                             # solutions for all the benchmarks with different imbalance factors
    │   ├── ISPD_benchmark_solutions          # solutions on ISPD98 testcases with unit vertex weights
    │   |   ├── hMetis                        # solutions using hMETIS
    │   |   |   ├── UBfactor_2                # solutions with imbalance factor 2
    │   |   |   └── UBfactor_10               # solutions with imbalance factor 10
    │   |   |   
    │   |   ├── KaHyPar                       # solutions with KaHyPar
    │   |   |   ├── UBfactor_2                # solutions with imbalance factor 2
    │   |   |   └── UBfactor_10               # solutions with imbalance factor 10
    │   |   |   
    |   |   └── SpecPart                      # solutions with SpecPart
    │   |       ├── hMetis_SpecPart           # SpecPart with initial solution generated from hMETIS
    |   │       |   ├── UBfactor_2            # solutions with imbalance factor 2
    │   |       |   └── UBfactor_10           # solutions with imbalance factor 10
    │   |       |
    │   |       └── KaHyPar_SpecPart          # SpecPart with initial solution generated from KaHyPar
    |   │           ├── UBfactor_2            # solutions with imbalance factor 2
    │   |           └── UBfactor_10           # solutions with imbalance factor 10
    │   |       
    │   ├── ISPD_weight_benchmark_solutions   # solutions on ISPD98 testcases with actual vertex weights
    │   |   ├── hMetis                        # solutions with hMETIS
    │   |   |   ├── UBfactor_2                # solutions with imbalance factor 2
    │   |   |   └── UBfactor_10               # solutions with imbalance factor 10
    │   |   |   
    │   |   ├── KaHyPar                       # solutions with KaHyPar
    │   |   |   ├── UBfactor_2                # solutions with imbalance factor 2
    │   |   |   └── UBfactor_10               # solutions with imbalance factor 10
    │   |   |   
    │   |   └── SpecPart                      # solutions with SpecPart
    │   |       ├── hMetis_SpecPart           # SpecPart with initial solution generated from hMETIS
    |   │       |   ├── UBfactor_2            # solutions with imbalance factor 2
    │   |       |   └── UBfactor_10           # solutions with imbalance factor 10
    │   |       |   
    │   |       └── KaHyPar_SpecPart          # SpecPart with initial solution generated from KaHyPar
    |   │           ├── UBfactor_2            # solutions with imbalance factor 2
    │   |           └── UBfactor_10           # solutions with imbalance factor 10
    │   |       
    └── └── Titan23_benchmark_solutions       # solutions on Titan23 testcases
            ├── hMetis                        # solutions with hMETIS
            |   ├── UBfactor_2                # solutions with imbalance factor 2
            |   └── UBfactor_20               # solutions with imbalance factor 20
            |   
            ├── hMetis_Autotune               # solutions with Autotuned hMETIS
            |   └── UBfactor_10               # solutions with imbalance factor 10
            |   
            ├── hMetis_Autotune_SpecPart      # SpecPart with initial solution generated from Autotuned hMETIS   
            |   └── UBfactor_10               # solutions with imbalance factor 10
            |   
            └── hMetis_SpecPart               # SpecPart with initial solution generated from hMETIS   
                ├── UBfactor_2                # solutions with imbalance factor 2
                └── UBfactor_20               # solutions with imbalance factor 20
    
*******************************************************************************************
  
## Installation and Run Instructions ## 

Open Julia REPL and do the following: 
``` 
include("SpectralRefinement.jl")
using Main.SpecPart
SpecPart.SpectralRefinement(hg = "Hypergraph file", pfile = "Partition file", Nparts = "Number of partitions", cycles = ζ, hyperedges_threshold = γ, ub = ε, nev = m, refine_iters = β, best_solns = δ)

ζ is the number of graph cycles (we recommend ζ=2)
γ is the threshold number of hyperedges to run ILP (we recommend γ=600)
ε is the imbalance factor (ε=1-49)
m is the number of eigenvectors (we recommend m=2)
β is the number of SpecPart iterations (we recommend β=2)
δ is the number of solutions picked from candidate solutions for overlay based clustering (we recommend δ=5)

```

Please note that current version of SpecPart supports bipartitions only. We will publish future versions of the code to tackle k-way partitions. A user guide is available [here](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/tree/main/SpecPart/README.md). 

*******************************************************************************************

## Leaderboards of minimum hyperedge cut values ##

Current Leaderboard of minimum hyperedge cut values on [ISPD98 testcases](https://dl.acm.org/doi/10.1145/274535.274546) with unit vertex weights and actual vertex weights, with different imbalance factors (ε):  

|   Testcase   | Statistics |              |    Cutsize    |              |              |               |
|:------------:|:----------:|:------------:|:-------------:|:------------:|:------------:|:-------------:|
|              | # Vertices | # Hyperedges | ε  = 1 | ε = 2 | ε = 5 | ε = 10 |
|     IBM01    |    12752   |     14111    |      203      |      [200](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm01.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      180     |      [166](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm01.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
| IBM01_wt |    12752   |     14111    |      216      |      [215](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm01.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      215     |      [215](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm01.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
|     IBM02    |    19601   |     19584    |      341      |      [307](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm03.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      262     |      [262](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm02.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
| IBM02_wt |    19601   |     19584    |      266      |      [266](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm04.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      260     |      [207](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm02.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
|     IBM03    |    23136   |     27401    |      954      |      [951](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm04.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      950     |      [950](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm03.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
| IBM03_wt |    23136   |     27401    |      775      |      [691](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm03.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      680     |      [580](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm03.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
|     IBM04    |    27507   |     31970    |      580      |      [573](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm04.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      514     |      [388](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm04.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
| IBM04_wt |    27507   |     31970    |      496      |      [475](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm04.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      438     |      [393](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm04.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
|     IBM05    |    29347   |     28446    |      1719     |     [1706](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm05.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1697     |      [1645](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm05.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
| IBM05_wt |    29347   |     28446    |      1724     |     [1722](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm05.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1693     |      [1647](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm05.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
|     IBM06    |    32498   |     34826    |      976      |      [962](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm06.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      871     |      [728](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm06.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
| IBM06_wt |    32498   |     34826    |      483      |      [442](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm06.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      363     |      [297](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm06.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
|     IBM07    |    45926   |     48117    |      910      |      [878](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm07.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      818     |      [764](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm07.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
| IBM07_wt |    45926   |     48117    |      737      |      [736](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm07.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      717     |      [636](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm07.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
|     IBM08    |    51309   |     50513    |      1140     |     [1140](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm08.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1140     |      [1120](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm08.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
| IBM08_wt |    51309   |     50513    |      1170     |     [1168](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm08.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1120     |      [972](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm08.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
|     IBM09    |    53395   |     60902    |      625      |      [620](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm09.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      620     |      [519](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm09.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
| IBM09_wt |    53395   |     60902    |      519      |      [519](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm09.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      519     |      [522](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm09.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
|     IBM10    |    69429   |     75196    |      1285     |     [1253](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm10.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1244     |      [1244](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm10.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
| IBM10_wt |    69429   |     75196    |      1030     |      [947](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm10.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      732     |      [413](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm10.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
|     IBM11    |    70558   |     81454    |      1065     |     [1051](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm11.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      951     |      [763](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm11.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
| IBM11_wt |    70558   |     81454    |      767      |      [766](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm11.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      687     |      [656](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm11.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
|     IBM12    |    71076   |     77240    |      1934     |     [1919](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm12.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1871     |      [1841](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm12.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
| IBM12_wt |    71076   |     77240    |      1976     |     [1973](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm12.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1976     |      [1855](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm12.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
|     IBM13    |    84199   |     99666    |      837      |      [831](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm13.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      831     |      [655](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm13.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
| IBM13_wt |    84199   |     99666    |      892      |      [846](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm13.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      846     |      [793](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm13.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)      |
|     IBM14    |   147605   |    152772    |      1842     |     [1842](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm14.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1794     |      [1509](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm14.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
| IBM14_wt |   147605   |    152772    |      1740     |     [1674](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm14.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1501     |      [1282](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm14.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
|     IBM15    |   161570   |    186608    |      2743     |     [2730](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm15.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     2530     |      [2135](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm15.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
| IBM15_wt |   161570   |    186608    |      2014     |     [1913](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm15.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1771     |      [1444](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm15.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
|     IBM16    |   183484   |    190048    |      1975     |     [1827](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm16.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1695     |      [1619](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm16.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
| IBM16_wt |   183484   |    190048    |      1656     |     [1634](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm16.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1634     |      [1634](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm16.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
|     IBM17    |   185495   |    189581    |      2314     |     [2270](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm17.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     2186     |      [1989](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm17.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
| IBM17_wt |   185495   |    189581    |      2302     |     [2289](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm17.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     2187     |      [2018](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm17.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
|     IBM18    |   210613   |    201920    |      1521     |     [1521](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm18.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1521     |      [1520](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm18.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |
| IBM18_wt |   210613   |    201920    |      1641     |     [1588](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_2/ibm18.weight.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1520     |      [1520](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/ISPD_weight_benchmark_solutions/hMetis_SpecPart/UBfactor_10/ibm18.weight.hgr.k.2.UBfactor.10.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |

*******************************************************************************************

Current Leaderboard of minimum hyperedge cut values on [Titan23 testcases](https://www.eecg.utoronto.ca/~kmurray/titan.html) with different imbalance factors (ε): 

|               | Statistics |             |    Cutsize   |              |              |               |               |
|---------------|:----------:|:-----------:|:------------:|:------------:|:------------:|:-------------:|:-------------:|
|    Testcase   |  #Vertices | #Hyperedges | ε = 1 | ε = 2 | ε = 5 | ε = 10 | ε = 20 |
|  sparcT1_core |    91976   |    92827    |     1088     |     [1012](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/sparcT1_core.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1001     |      1090     |      903      |
|     neuron    |    92290   |    125305   |      239     |      [239](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/neuron.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      239     |      239      |      206      |
|  stereovision |    94050   |    127085   |      186     |      [180](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/stereo_vision.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      180     |       91      |       91      |
|     des90     |   111221   |    139557   |      416     |      [372](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis/UBfactor_2/des90.hgr.k.2.UBfactor.2.seed.0)     |      393     |      393      |      358      |
|  SLAM_spheric |   113115   |    142408   |     1061     |     [1061](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/SLAM_spheric.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1061     |      1061     |      1061     |
|  cholesky_mc  |   113250   |    144948   |      343     |      [285](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/cholesky_mc.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      281     |      281      |      285      |
|  segmentation |   138295   |    179051   |      165     |      [126](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/segmentation.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      107     |      85      |       78      |
|  bitonic_mesh |   192064   |    235328   |      588     |      [587](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/bitonic_mesh.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      581     |      543      |      483      |
|      dart     |   202354   |    223301   |      807     |      [807](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/dart.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      807     |      719      |      540      |
|     openCV    |   217453   |    284108   |      566     |      [510](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/openCV.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      506     |      506      |      506      |
|    stap_qrd   |   240240   |    290123   |      398     |      [398](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/stap_qrd.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      380     |      296      |      295      |
|     minres    |   261359   |    320540   |      241     |      [215](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/minres.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      215     |      199      |      189      |
| cholesky_bdti |   266422   |    342688   |     1213     |     [1156](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/cholesky_bdti.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1156     |      1156     |      947      |
|    denoise    |   275638   |    356848   |      457     |      [416](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/denoise.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      416     |      416      |      224      |
|  sparcT2_core |   300109   |    302663   |     1227     |     [1227](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/sparcT2_core.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1227     |      1227     |      1227     |
|   gsm_switch  |   493260   |    507821   |     1836     |     [1827](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/gsm_switch.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1615     |      1460     |      1407     |
|    mes_noc    |   547544   |    577664   |      703     |      [634](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/mes_noc.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      634     |      634      |      617      |
|     LU230     |   574372   |    669477   |     3362     |     [3273](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/LU230.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     3339     |      3262     |      2677     |
|   LU_Network  |   635456   |    726999   |      646     |      [525](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/LU_Network.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      524     |      524      |      524      |
| sparcT1_chip2 |   820886   |    821274   |     1037     |      [899](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/sparcT1_chip2.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      899     |      815      |      783      |
|    directrf   |   931275   |   1374742   |      673     |      [574](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/directrf.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |      574     |      378      |      295      |
| bitcoin_miner |   1089284  |   1448151   |     1512     |     [1297](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/solutions/Titan23_benchmark_solutions/hMetis_SpecPart/UBfactor_2/bitcoin_miner.hgr.k.2.UBfactor.2.eig_vecs.2.num_cycles.2.h_threshold.300.solver_iters.80.spec_iters.2.best_solns.5.seed.0)     |     1232     |      1232     |      1225     |

*******************************************************************************************

## Authors ##
Ismail Bustany, Andrew Kahng, Yiannis Koutis, Bodhisatta Pramanik, Zhiang Wang


## References ##
To reference SpecPart, please cite:

I. Bustany, A. B. Kahng, Y. Koutis, B. Pramanik and Z. Wang, "SpecPart: A Supervised Spectral Framework for Hypergraph Partitioning Solution Improvement", ([pdf](https://github.com/TILOS-AI-Institute/HypergraphPartitioning/blob/main/SpecPart/SpecPart_final_submission.pdf)),
*Proc. ACM/IEEE International Conference on Computer-Aided Design*, 2022, to appear.

## Acknowledgments ##
This work was partially supported by NSF CCF-2112665, CCF-2039863, CCF-1813374, DARPA HR0011-18-0-2-0032

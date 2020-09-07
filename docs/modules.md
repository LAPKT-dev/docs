# Modules and Planners

## Planners


Planners by default use the FD parser. A version of each planner exist
using FF parser instead. 3 planners where submitted to Satisficing and
Agile track in IPC 2014.

They support action costs and Conditional Effects. See
[Documentation\#Parsers\_Supported](Documentation#Parsers_Supported "wikilink")
to know how to tell the parser to ignore or account for action costs.

### FF


FF planner as described in JAIR 2001. Goal agenda is not computed by
default.

-   FF-parser

<!-- -->

    planners/ff-ffparser

    Command: ./ff --domain <domain_file> --problem <problem_file> --output <plan_output> 

    Options::
      --help                Show help message
      --domain arg          Input PDDL domain description
      --problem arg         Input PDDL problem description
      --output arg          Output file for plan

### BFS\_f


Greedy Best First Search Planner that uses f(n) = novelty(n), breaking
ties with lm\_count(n) and h\_rel\_plan(n). described in [Lipovetzky et
al. at ECAI 2012](http://ebooks.iospress.nl/Download/Pdf/7029)

-   FD-parser

<!-- -->

    planners/bfs_f

    Command: 
    ./bfs.py <domain_file> <problem_file> <plan_output> 

    Ignores costs:
    ./bfs_f_unit_cost.py  <domain_file> <problem_file> <plan_output> 

    Options specified inside the script

-   FF-parser

<!-- -->

    planners/bfs_f-ffparser

    Command: ./bfs_f --domain <domain_file> --problem <problem_file> --output <plan_output> 

    Options::
      --help                          Show help message
      --domain arg                    Input PDDL domain description
      --problem arg                   Input PDDL problem description
      --bound arg (=2)                Max width w for novelty (default 2)
      --output arg                    Output file for plan
      --one-ha-per-fluent arg (=0)    Extract only one helpful action per fluent
      --use-original-ff-heur arg (=0) Use original FF heuristic computed by layers

#### Anytime BFS\_f

Runs First SIW, then BFS\_f with the bound found by SIW, and finally an
anytime version using RWA\* described in [IPC 2014
Booklet](http://people.eng.unimelb.edu.au/nlipovetzky/papers/ipc8_siw_bfs_probe.pdf)

-   FD-parser

<!-- -->

    planners/at_bfs_f

    Command: 
    ./at_bfs.py <domain_file> <problem_file> <plan_output> 

    ./at_bfs_f-2-no-bfs_f.py <domain_file> <problem_file> <plan_output> 

    ./at_bfs_f-2-no-siw.py <domain_file> <problem_file> <plan_output> 

    ./at_bfs_f-no-siw-no-bfs_f.py <domain_file> <problem_file> <plan_output> 

    Options specified inside the script

-   FF-parser

<!-- -->

    planners/at_bfs_f-ffparser

    Command: ./at_bfs_f --domain <domain_file> --problem <problem_file> --output <plan_output> 

    Options::
      --help                       Show help message
      --domain arg                 Input PDDL domain description
      --problem arg                Input PDDL problem description
      --iw-bound arg (=2)          Max width w for SIW (default 2)
      --max-novelty arg (=2)       Max width w for novelty heuristic in BFS(f) 
                                   (default 2)
      --output arg                 Output file for plan
      --one-ha-per-fluent arg (=0) Extract only one helpful action per fluent
      --disable-siw arg (=0)       Disable SIW stage
      --disable-bfs-f arg (=0)     Disable BFS(f) stage

### Blind & Width-Based Search Planners


#### IW

Iterative Width is a blind search planner that exploits the low width of
classical benchmark when goals are atomic. For conjuctive goals look at
SIW, SIW+ or DFS+ described in [Lipovetzky et al. at ECAI
2012](http://ebooks.iospress.nl/Download/Pdf/7029)

-   FD-parser

<!-- -->

    planners/iw

    Command: 
    ./iw.py <domain_file> <problem_file> <plan_output> 

    Options specified inside the script

-   FF-parser

<!-- -->

    planners/iw-ffparser

    Command: ./iw --domain <domain_file> --problem <problem_file> --output <plan_output> 

    Options::
      --help                Show help message
      --domain arg          Input PDDL domain description
      --problem arg         Input PDDL problem description
      --bound arg (=1)      Max width w for IW(w)
      --atomic arg (=1)     Runs IW(w) over each atomic goal of the problem (bool)
      --output arg          Output plan file

#### IW Plus

IW+ relaxes IW novelty pruning. described in [Lipovetzky et al. at ECAI
2014](http://people.eng.unimelb.edu.au/nlipovetzky/papers/width_ecai14.pdf)

-   FD-parser

<!-- -->

    planners/iw

    Command: 
    ./rp_iw.py <domain_file> <problem_file> <plan_output> 

    Options specified inside the script

-   FF-parser

<!-- -->

    planners/iw-ffparser

    Command: ./rp_iw --domain <domain_file> --problem <problem_file> --output <plan_output> 

    Options::
      --help                Show help message
      --domain arg          Input PDDL domain description
      --problem arg         Input PDDL problem description
      --bound arg (=2)      Max width w for IW(w)
      --output arg          Output plan file

#### SIW

Serialized Iterative Width is a blind search planner competitive that
exploits the low width of classical benchmark through IW and simple goal
serialization described in [Lipovetzky et al. at ECAI
2012](http://ebooks.iospress.nl/Download/Pdf/7029)

-   FD-parser

<!-- -->

    planners/siw

    Command: 
    ./siw.py <domain_file> <problem_file> <plan_output> 

    Ignores costs:
    ./siw_unit_cost.py  <domain_file> <problem_file> <plan_output> 

    Options specified inside the script

-   FF-parser

<!-- -->

    planners/siw-ffparser

    Command: ./siw --domain <domain_file> --problem <problem_file> --output <plan_output> 

    Options::
      --help                Show help message
      --domain arg          Input PDDL domain description
      --problem arg         Input PDDL problem description
      --bound arg (=1)      Max width w for IW(w)
      --output arg          Output plan file

#### SIW Plus

SIW+ relaxes IW novelty pruning. Blind Search Planner with high
performance, closer to FF over IPC\'11 benchmark described in
[Lipovetzky et al. at ECAI
2014](http://people.eng.unimelb.edu.au/nlipovetzky/papers/width_ecai14.pdf)

-   FD-parser

<!-- -->

    planners/siw_plus

    Command: 
    ./siw_plus.py <domain_file> <problem_file> <plan_output> 

    Ignores costs:
    ./siw_plus_unit_cost.py  <domain_file> <problem_file> <plan_output> 

    Options specified inside the script

-   FF-parser

<!-- -->

    planners/siw_plus-ffparser

    Command: ./siw_plus --domain <domain_file> --problem <problem_file> --output <plan_output> 

    Options::
      --help                Show help message
      --domain arg          Input PDDL domain description
      --problem arg         Input PDDL problem description
      --bound arg (=1)      Max width w for IW(w)
      --output arg          Output plan file

#### DFS Plus

DFS+ Extends SIW+ Goal serialization. Blind Search planner with high
performance, closer to LAMA\'11 and BFS\_f over IPC\'11 benchmark
described in [Lipovetzky et al. at ECAI
2014](http://people.eng.unimelb.edu.au/nlipovetzky/papers/width_ecai14.pdf)

-   FD-parser

<!-- -->

    planners/dfs_plus

    Command: 
    ./dfs_plus.py <domain_file> <problem_file> <plan_output> 

    Ignores costs:
    ./dfs_plus_unit_cost.py  <domain_file> <problem_file> <plan_output> 

    Options specified inside the script

-   FF-parser

<!-- -->

    planners/dfs_plus-ffparser

    Command: ./dfs_plus --domain <domain_file> --problem <problem_file> --output <plan_output> 

    Options::
      --help                Show help message
      --domain arg          Input PDDL domain description
      --problem arg         Input PDDL problem description
      --bound arg (=2)      Max width w for IW(w)
      --output arg          Output plan file

### Generic BFS with Optional Heuristics


By default BFS is set to GBFS

-   FF-parser

<!-- -->

    planners/generic-best_first-ffparser

    Command: ./bfs --domain <domain_file> --problem <problem_file> --output <plan_output> 

    Options::
      --help                Show help message
      --domain arg          Input PDDL domain description
      --problem arg         Input PDDL problem description
      --heuristic arg (=1)  1: H_add (default 1)
                            2: H_add_Rp
                            3: H_max_Rp
                            4: H_add_FF_Rp
                            5: H_max_FF_Rp
                            6: H_layered_FF_Rp ( FF_*, as in Journal Paper)
      --anytime arg (=0)    Anytime (default False)
      --output arg          Output file for plan

## Search Algorithms Implemented


All Search Algorithms implement Forward Search by accessing

     interfaces/agnostic/fwd_search_prob.hxx 

decoupling the search algrotihm from successor generation, applicability
function, etc. Intended to easily run this algorithms on backward
search.

### Blind Search


No use of heuristics.

#### Breadth-First search

     include/aptk/brfs.hxx 

### Width-Based Search


described in [Lipovetzky et al. at ECAI
2012](http://ebooks.iospress.nl/Download/Pdf/7029), and [Lipovetzky et
al. at ECAI
2014](http://people.eng.unimelb.edu.au/nlipovetzky/papers/width_ecai14.pdf)

#### Iterated Width

Breadth-First search with novelty pruning.

     include/aptk/iw.hxx 

#### Iterated Width Plus

Breadth-First search with a relaxed novelty pruning.

     include/aptk/rp_iw.hxx 

#### Serialized Iterated Width

Uses iterated width to both solve and serialize the goals. The
serialization is a form of Hill-Climbing over the set of goals

     include/aptk/siw.hxx 

#### Serialized Iterated Width Plus

Uses iterated width plus to both solve and serialize the goals. The
serialization is a form of Hill-Climbing over the set of goals

     include/aptk/siw_plus.hxx 

#### Depth-first Search Width

Uses iterated width to both solve and serialize the goals. DFS in the
space of serialization induced by bounded Iterative Width.

     include/aptk/dfs_plus.hxx 

### Heuristic Search


#### Best-First search

##### Greedy Best First Search

     include/aptk/at_gbfs.hxx 

##### Any-time Best First Search

     include/aptk/at_bfs.hxx 

##### Any-time Best First Search with two open lists

     include/aptk/at_bfs_dq.hxx 

The PREFERRED list, for nodes generated by preferred operators, and the
OPEN list, for the rest.

##### Best First Search with three open lists and two heuristic estimators

    include/aptk/at_bfs_dq_mh.hxx 

The search frontier is split into three lists:

-   BOTH: holds nodes generated by actions deemed as \'preferred\' by
    both heuristic

estimators

-   PREFERRED: holds nodes generated by actions deemed as \'preferred\'
    by the

primary heuristic estimator

-   OPEN: holds nodes generated by actions not deemed as \'preferred\'
    by the primary

heuristic estimator

##### Any-time Weighted A\*

Weight W decaying according to fixed decay parameter. Variants include
single queue and multiple queue (either with one or two heuristic
estimators).

     
    include/aptk/at_wbfs.hxx
    include/aptk/at_wbfs_dq.hxx
    include/aptk/at_wbfs_dq_mh.hxx

##### Any-time Restarting Weighted A\*

described in [Ricther et al. at ICAPS
2010](http://www.aaai.org/ocs/index.php/ICAPS/ICAPS10/paper/download/1437/1541)
with weight W decaying according to fixed decay parameter. Variants
include single queue and multiple queue (either with one or two
heuristic estimators).

     
    include/aptk/at_rwbfs.hxx
    include/aptk/at_rwbfs_dq.hxx
    include/aptk/at_rwbfs_dq_mh.hxx
     

#### Contract Search

##### The Deadline Aware Search algorithm

described in [Dionne et al. at SOCS
2011](http://www.aaai.org/ocs/index.php/SOCS/SOCS11/paper/viewFile/4030/4356)

    include/aptk/das.hxx

#### EHC

Enforced Hill Climbing as in JAIR 2001.

    include/aptk/ff_ehc.hxx

## Heuristics Implemented


### Critical Paths


#### h\^1

    interfaces/agnostic/h_1.hxx

#### h\^2

    interfaces/agnostic/h_2.hxx

### Delete Relaxations
------------------

#### h\_max / h\_add

Same implementation as h\^1. h\_add and h\_max differ only through the
evaluation function, which can be specified. Dijskstra Based
implementation

    interfaces/agnostic/h_1.hxx

Relaxed Planning Graph implementation

    interfaces/agnostic/layered_h_max.hxx

#### h\^ff

Original FF heuristic computation from JAIR 2001 paper

    interfaces/agnostic/ff_rp_heuristic.hxx

#### Relaxed Planning Graph Heuristics

Computes relaxed plan heuristics backwards from the goal based on
best\_supporters function. [Keyder et al. ECAI
2008](http://ebooks.iospress.nl/Download/Pdf/4439) h\_1 and h\_add
natively define best supporters, although other heuristics could be used
too.

    interfaces/agnostic/rp_heuristic.hxx

#### h\^C

Semi Relaxed Heuristic by introducing special fluents that explicitly
represent conjunctions of fluents [Keyder et al. ICAPS
2012](http://www.aaai.org/ocs/index.php/ICAPS/ICAPS12/paper/viewFile/4568%26lt%3B/4722)

    interfaces/agnostic/h_C.hxx

### Counting heuristic


#### Unachieved Goals

Counts the number of unachieved goals

    interfaces/agnostic/h_unsat.hxx

#### Unachieved Landmarks

Counts the number of unachieved landmarks. Landmark graph is built from
And/Or Graphs [Keyder et al. ECAI
2010](http://ebooks.iospress.nl/Download/Pdf/5793)

    interfaces/agnostic/landmark_count.hxx

#### Novelty

Counts the size of the smallest tuple made true by a given state for the
first time in the search [Lipovetzky et al. at ECAI
2012](http://ebooks.iospress.nl/Download/Pdf/7029)

    interfaces/agnostic/novelty.hxx

#### Novelty Plus

Relaxed versioin of Novelty [Lipovetzky et al. at ECAI
2014](http://people.eng.unimelb.edu.au/nlipovetzky/papers/width_ecai14.pdf)

    interfaces/agnostic/novelty.hxx

### Reachability


Naive implementation for testing reachability

    interfaces/agnostic/reachability.hxx

Watchlist-based implementation for testing reachability:

    interfaces/agnostic/watch_list_succ_gen.hxx

(see the \"is\_reachable(const State&)\" method)

## Parsers Supported


We currently ported FF-Parser and FD-Parser

### FF Parser


FF-Parser is based on bison and flex. It\'s compiled as an independent
library in

    external/libff

and connected to the toolkit in

    interfaces/ff-wrapped/ff_to_aptk.hxx
    interfaces/ff-wrapped/ff_to_aptk.hxx

creating a STRIPS Problem instance.

**Action costs** can be ignored by setting the ignore\_action\_costs =
true

    void get_problem_description(  std::string pddl_domain_path,
                        std::string pddl_problem_path,
                        STRIPS_Problem& strips_problem,
                        bool ignore_action_costs = false,
                        bool get_detailed_fluent_names = false );

    aptk::FF_Parser::get_problem_description(...,true) 

### FD-parser


FD-Parser is written in python. It\'s located in

    external/fd

and connected to the toolkit in

    planners/python/agnostic/py_strips_prob.hxx
    planners/python/agnostic/py_strips_prob.cxx

creating a STRIPS Problem instance.

**Action costs** can be ignored by setting in your python script

    task.ignore_action_costs = True 

as it\'s done for example in

    /planners/bfs_f/bfs_f_unit_cost.py

## Problem Representation (STRIPS Model)


### STRIPS Problem and useful information like mutexes (if computed)

    interfaces/agnostic/strips_prob.cxx  
    interfaces/agnostic/strips_prob.hxx 

### STRIPS States

    interfaces/agnostic/strips_state.cxx    
    interfaces/agnostic/strips_state.hxx

### Actions and Fluents

    interfaces/agnostic/fluent.cxx  
    interfaces/agnostic/fluent.hxx

    interfaces/agnostic/action.cxx  
    interfaces/agnostic/action.hxx

    interfaces/agnostic/cond_eff.cxx    
    interfaces/agnostic/cond_eff.hxx

### Successor Generator

    interfaces/agnostic/succ_gen.cxx
    interfaces/agnostic/succ_gen.hxx

## Running Experiments


Scripts for running experiments, profiling, benchmarking and creating
tables with Coverage, IPC Time and Quality Score are available

    benchmarks/run.py

    # Dependencies/Prerequisites:
    #   - valgrind
    #   - timeout
    #   - dot (graphviz)
    #   - krtoolkit

     Usage:
        python run.py profile <executable> <ipc directory> [<domain pddl> <problem pddl>]
        python run.py benchmark <executable> <ipc directory> <results directory> [<domain>]
        python run.py compare <directories with , separated> <ipc directory>
        python run.py clean

Some Benchmark domains can be found at

    benchmarks/ipc-2006/
    benchmarks/ipc-2011/
    benchmarks/ipc-2014/

To use run.py script over new sets of benchmarks instead of specific
domains, edit

    benchmarks/domains.py

## Examples


### FF-Interface Example


The example for the 'ff parser' interface can be found on

    * examples/ff-interface

### FD-Interface Example


The example for the 'fD parser' interface can be found on

    * examples/fd-interface

This is a very simple example that shows the basics for interfacing
lwaptk with Fast Downward parser. In order to build the example issue
the command:

    $ ./build.py

and to run the example:

    $ ./parser.py <path to pddl domain file> <path to pddl problem file>

if everything is working as it should, you should see FD parsing output
on the standard output, as well as a dump of the grounded actions.

Note that this will copy the folder externals/fd to the local directory,
so DO NOT add it to the repository. If you need to do customize Fast
Downward parsing scripts, just edit build.py to avoid it clobbering your
local copy.

### Agnostic Interface Examples


The examples for the 'planner agnostic' interface can be found on

examples/agnostic-examples

and cover the following topics:

#### Assembling STRIPS problem programatically

Shows how to define a STRIPS planning problem programatically.

    * agnostic-examples/assembling_strips_problems

#### Successor Generators

Discusses and compares different ways of generating successors during
search.

    * agnostic-examples/successor_generation

#### Open Lists

Discusses and compares different ways of creating open lists for your
search algortithm.

    * agnostic-examples/fibonacci_open

#### BFS engine variations

Shows how can one assemble available components to deliver a planner
built around a BFS search engine, with multiple queues and secondary
heuristics, on a parametrized planning task.

    * agnostic-examples/bfs
    * agnostic-examples/bfs-double-queue 
    * agnostic-examples/bfs-double-queue-secondary-heuristic

#### BFS + h\_max (greedy\|delayed\|anytime) + FF-parser

Shows how to assemble a classic planner: best-first search using h\_max
with multiple modes: greedy/delayed/anytime, over a task specified in
PDDL and parsed by FF-parser

    * agnostic-examples/bfs-hmax

#### WA\* variations + landmarks

Shows how can one assemble available components to deliver a planner
built around a WA\* search engine, with multiple queues and secondary
heuristics, on a parametrized planning task. Illustrates as well how to
use landmark count heurstic.

    * agnostic-examples/wa-planner
    * agnostic-examples/rwa-planner

#### Deadline Aware Search engine

Shows how can one assemble available components to deliver a planner
built around Deadline Aware Search.

    * agnostic-examples/das

#### Breadth-First search + FF-parser

Shows how can one assemble available components to deliver a blind
search planner.

    * agnostic-examples/brfs

#### h\_C compilations + FF-parser

Shows how can one use the \\Pi\_C compilation to compute the h\_C
heuristic. [Keyder et al. ICAPS
2012](http://www.aaai.org/ocs/index.php/ICAPS/ICAPS12/paper/viewFile/4568%26lt%3B/4722)

    * agnostic-examples/h_C_heuristics

#### Replanner (changing init and goal situation on the fly)

Shows how to create a replanner. It illustrates how to change the
initial and goal states without having to parse the problem again,
solving it with bfs+h\_max. In the example we change the initial and
goal situations by applying the first action of the current plan to
progress the initial state, and last action of the plan to regress the
goal.

    * agnostic-examples/replanner

#### Width-Based algorithm + FD parser

Shows how SIW is implemented, using novelty function and FD parser

    * planners/siw

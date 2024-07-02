# About 

The algorithm employs a zero branch-length statistical test to evaluate the
necessity of edges within network triangles. Utilizing the TN93 substitution
matrix and Felsenstein's maximum likelihood approach, it assesses whether the
nodes in a triangle are conditionally independent. Edges failing the test are
marked for removal unless they serve as 'bridges' in the network, ensuring no
clusters are broken. The method iterates until no further edges can be removed
and is extendable to cycles of arbitrary length.

## Example Usage

## How to Perform Edge Filtering with HIV-TRACE

Edge filtering is crucial in analyzing HIV transmission networks by removing
spurious transitive connections that might misrepresent the true structure of
the network. Here's how you can apply edge filtering using the `hivtrace` tool
and the `hivnetworkcsv` command.

### Requirements

- [HIV-TRACE](https://github.com/veg/hivtrace) installed and configured on your system.
- A FASTA file with your sequence data.

### Using `hivtrace` for Edge Filtering

The `hivtrace` command allows you to run the entire HIV-TRACE pipeline. To apply edge filtering, use the `-f` or `--filter` option with either `remove` or `report` arguments:

- `remove`: Reports spurious transitive connections.
- `report`: Removes spurious transitive connections.

**Example Command:**

```sh
hivtrace --do-not-store-intermediate -i PATH_TO_FASTA -a resolve -f remove -r REFERENCE_SEQUENCE -t TRANSMISSION_THRESHOLD -m MINIMUM_CLUSTER_SIZE -g GENETIC_DISTANCE_THRESHOLD -o OUTPUT_JSON --log OUTPUT_LOG
```

Replace PATH_TO_FASTA, REFERENCE_SEQUENCE, TRANSMISSION_THRESHOLD, MINIMUM_CLUSTER_SIZE, GENETIC_DISTANCE_THRESHOLD, OUTPUT_JSON, and OUTPUT_LOG with your specific parameters.

### Using hivnetworkcsv for Edge Filtering
If you already have pairwise distances, use the hivnetworkcsv command with the --edge-filtering option:

#### Syntax:
```
hivnetworkcsv -i INPUT_CSV -t TRANSMISSION_THRESHOLD -f FORMAT -j -o -n {remove,report} -s SEQUENCE_FILE
```

* `INPUT_CSV`: Your input CSV file with pairwise distances.
* `TRANSMISSION_THRESHOLD`, `FORMAT`, `SEQUENCE_FILE`: Replace with your specific parameters.
* `--edge-filtering {remove,report}`: Choose remove to report spurious connections, report to view flagged edges as dashed lines in the visualization.

After performing edge filtering and generating the results JSON file using `hivtrace` or `hivnetworkcsv`, you can visualize the resulting network by visiting [hivtrace.datamonkey.org](http://hivtrace.datamonkey.org). To upload and view your results, follow these steps:

1. Navigate to [hivtrace.datamonkey.org](http://hivtrace.datamonkey.org).
2. Click on **Select File**.
3. Choose **Upload File** and select the results JSON file you generated.

This web-based tool provides a convenient way to visually analyze the HIV transmission network based on your data.


## Method

### Zero branch-length statistical test for edge removal

In each network triangle, a zero branch-length statistical test is
executed to assess the conditional independence of nodes. The test's
foundational premise posits that if a node's branch length exceeds zero
within a putative transmission chain, the remaining nodes in the
triangle are not conditionally independent. The test employs the TN93
substitution matrix in conjunction with Felsenstein's maximum likelihood
method for parameter optimization. We adopt a null hypothesis stating a
branch length of zero and an alternative hypothesis of a non-zero branch
length. The TN93 model was chosen for its balance of computational
efficiency and robust results, compared to more complex alternatives
like GTR.

The steps to perform the zero-length branch test is as follows.

1.  Create a 3-taxon unrooted phylogenetic tree for a given triangle.

2.  Calculate the maximum likelihood of the tree under the full TN93
    model of evolution.

3.  Iterate through each of the three sequences and calculate the
    maximum likelihood with the respective index branch length
    constrained to zero.

4.  Return the hypothesis test's P-value results for each of the three
    sequences, using a one sided likelihood ratio test (50:50 mixture of
    $\chi^2_1$ and $\chi^2_0$). Note that in cases when more than one
    edge could be removed, and the degree of edge support is the same,
    **none** of the edges are removed in order to avoid creating
    spurious directionality due to tie-breaking. In the extreme case, a
    triangle of three identical sequences cannot be simplified to a
    chain simply because there is no information to do so.

### Procedure for Edge Pruning in Triangles

1.  Compute the network and list all existing triangles. Given that the
    total number of triangles scales as $N^3$, where $N$ represents the
    node count in a cluster, a preset limit (e.g., $2^{18}$) is
    established to restrict the number of triangles examined.

2.  For every triangle, identify which chains are statistically
    unsupportable. Edges corresponding to any non-rejectable chain are
    flagged for potential removal.

3.  Arrange flagged edges in ascending order based on p-value support
    (ranging from 0.5 to a smaller decimal).

4.  Eliminate the greatest possible number of statistically
    unsupportable edges, ensuring that no 'bridge' edges are removed,
    thereby maintaining the existing cluster configuration.

5.  Repeat the above steps iteratively until no additional edges qualify
    for removal.

### Extension to Cycles of Arbitrary Length $N$

1.  Derive the network and catalog all cycles of length $N$.

2.  For every identified cycle, generate $(2N-5)!!$ feasible unrooted
    trees.

3.  Administer the zero branch-length test on each constructed tree to
    ascertain which edge, if any, qualifies for removal from the cycle.

4.  Loop back to the first step and reiterate the process until no
    further edges are removable.

The zero branch-length test for edge removal in cycles of arbitrary
length $N$ is implemented in the `CycleSupport.bf` file within the
`hivclustering` Python package.


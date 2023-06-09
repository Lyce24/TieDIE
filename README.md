## Modified TieDIE Algorithm

This repository contains a modified version of the TieDIE Algorithm, originally designed by Evan Paull and others. The purpose of this modification is to address a bug related to the failure of running the `pagerank` method in the original implementation. Additionally, this repository includes a `requirements.txt` file and an `environment.yml` file to facilitate the setup of a virtual environment for running the algorithm.

## Bug Fix

In the original implementation of the TieDIE Algorithm, there was a bug that caused the `pagerank` method to fail. This bug prevented the proper execution of the method, leading to unexpected results and potential errors in downstream processes. The bug was specifically related to the lack of indentation in lines 319-323 of the `/bin/tiedie` file.

## Modification Details

To fix the bug in the TieDIE Algorithm, the following changes were made:

1. Open the `/bin/tiedie` file in a text editor.
2. Navigate to lines 319-323.
3. Add proper indentation to these lines.

The modified lines (line 305 -323 of the `/bin/tiedie` file) should look as follows:

```python (bin)
if opts.pagerank:
	# use PageRank to diffuse heats: create a diffuser object to perform this step
	diffuser = PPrDiffuser(network)
else:
	if opts.kernel is not None:
		sys.stderr.write("Loading Heat Diffusion Kernel..\n")
		# load a heat diffusion kernel to perform diffusion
		diffuser = Kernel(opts.kernel)
	else:
		sys.stderr.write("Using SCIPY to compute the matrix exponential, t=0.1...\n")
		# No kernel supplied: use SCIPY to generate a kernel on the fly, and then use it
		# for subsequent diffusion operations
		diffuser = SciPYKernel(opts.network)

	# Check to make sure the node universe matches the
	k_labels = diffuser.getLabels()
	if len(network_nodes) != len(k_labels) or len(network_nodes.intersection(k_labels)) != len(k_labels):
		sys.stderr.write("Error: the universe of gene/node labels in the network file doesn't match the supplied kernel file!\n")
		sys.exit(1)

```

These changes ensure the correct execution of the `pagerank` method and resolve the issue that caused it to fail in the original implementation.

## Acknowledgments

The original [TieDIE Algorithm](https://github.com/epaull/TieDIE) was designed by Evan Paull and others. We acknowledge their contributions and appreciate their work.

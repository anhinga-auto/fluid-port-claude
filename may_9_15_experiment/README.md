This is a dataflow program written in Processing 2.2.1 with `may_9_15_experiment.pde` being the main program.

The current configuration is controlled by the dataflow graph described in `may_8_graph.pde`
that currently uses `Before elections 015.JPG` image as the static input stream.

The dataflow graph described in `may_8_graph.pde` is an acyclic graph, with the original static stream being first
processed by a warp (`CustomWaveTransform`), then by color negation (`NegationTransform`), and then by another warp (`CustomWaveTransform`).

Results of those two warps are displayed in the rectangles on the left, `layer_1_1` and `layer_3_1`.

Those rectangles are equipped with `CustomClickControl` mouse controls, which restart the wave
when left-clicked or dragged. Otherwise, the wave is gradually relaxing with time.

Linear combinations of the original image and `layer_3_1`, and of `layer_1_1` and `layer_3_1` are
computed by `SumOf2Transform` transformations and are displayed in the rectangles on the right, `layer_4_1` and `layer_4_2`.

Those rectangles are equipped with `NumericControl` mouse controls, which control
coefficients in those linear combinations.

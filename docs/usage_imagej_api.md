# ImageJ API Usage

Note that most of the code examples here use PyImageJ and scyjava.

## `ij.plugin.filter.ParticleAnalyzer`

This section covers the `ParticleAnalyzer` which is triggred by the "Analyze Particles..." command.

### Save results to ResultsTable (headless)

Save results from the particle analyzer to a `ResultsTable` headlessly by and obtaining an empty results table object from `ij.ResultsTable.getResultsTable()` and setting the particle analyzer results table to the empty one.

```python
# get the particle analyzer
pa = scyjava.jimport('ij.plugin.filter.ParticleAnalyzer')()

# get a results table form ImageJ
rt = ij.ResultsTable.getResultsTable()

# set results table for particle analyzer
pa.setResultsTable(rt)
```

After running the "Analyze Particles..." command will store results in the `rt` object. For example:

```python
ij.py.run_plugin(plugin="Analyze Particles...", args"clear overlay", imp=imp)
```
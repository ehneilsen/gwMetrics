# gwMetrics

Strategy Studies for Gravitational Wave Cosmology

## Motivation

Mergers of compact binary systems have great potential to be used as standard sirens for cosmology. 
This study aims at developing a strategy to realize this potential and establish a new powerful cosmological probe.

## People
```
Marcelle Soares-Santos
Antonella Palmese
Tina Peters
Alex Malz
James Annis
Eric Neilsen
Hiranya Peiris
Rahul Biswas
```
## How-to Run a Simple Test

```
import matplotlib
matplotlib.use("Agg")
import matplotlib.pyplot as plt

import unittest

import lsst.sims.maf
import lsst.sims.maf.db as db
import lsst.sims.maf.metrics as metrics
import lsst.sims.maf.slicers as slicers
import lsst.sims.maf.stackers as stackers
import lsst.sims.maf.plots as plots
import lsst.sims.maf.metricBundles as metricBundles
import lsst.sims.maf.utils as utils

import numpy as np
import healpy as hp
import astrometry_defs as astr
import astrometryMAF_metrics
dirdb = '/data/des40.a/data/marcelle/lsst-gw/OperationsSimulatorBenchmarkSurveys/'
file = 'kraken_1042_sqlite.db'
opsdb = db.OpsimDatabase(dirdb+file)
outdir = '/data/des40.a/data/palmese/lsst-gw/'
resultsDb = db.ResultsDb(outDir=outdir)
metric = astrometryMAF_metrics.AstrometryMetric()
slicer = slicers.HealpixSlicer(nside=32)
sql0 = 'filter = "u" and night < 100'
cmap = plt.get_cmap('winter')
plotDict0={'title': 'u-band. error: 0.020, z: 2.1. 1 year. opsim: kraken_1042.',  'logScale': True, 'xlabel': 'Bayes Factor','cmap': cmap,'percentileClip': None, 'colorMin':1.0, 'colorMax':100.0, 'cbarFormat':'%.1g','cbar_edge': True, 'nTicks': 10, 'aspect': 'auto','xextent': None, 'origin': None}
HealpixSkyMap = plots.HealpixSkyMap()
HealpixHistogram = plots.HealpixHistogram()
mb0 = metricBundles.MetricBundle(metric, slicer, sql0,  plotDict=plotDict0, plotFuncs=[HealpixSkyMap, HealpixHistogram])
mbD = {0:mb0}
bgroup = metricBundles.MetricBundleGroup(mbD, opsdb, outDir=outdir, resultsDb=resultsDb)
bgroup.runAll()
```




## License, Contributing

The code in this repo is available for re-use under the MIT license. If you are interested in this project, please contact us by writing an [issue](https://github.com/soares-santos/gwMetrics/issues/new). To get started contributing to the project, just fork the repo - pull requests are always welcome!

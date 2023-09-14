
# Summary
Sandbox of software tools for parsing engine log files generated by a [Great Lakes EIS-4000 Engine Information System (EIS)](https://grtavionics.com/product/eis-4000/).

Jupyter notebook is convenient for graphing data locally. 

log_processor.py batch-processes text logs from ./new_logs/ into CSVs in ./processed_logs/, automatically uploading them to [Savvy Analysis](https://apps.savvyaviation.com/)

## Tried So Far
* Use protobufs to parse raw logs (see log format in "Model 4000:600 Serial Data List") - this turned out to be pretty awkward and python can easily handle the task in one line with struct. The format argument to struct is a bit of a hard-coded magic number, so maybe there's room to improve this.
* Parse logs and post to InfluxDB, to allow review with Grafana - got it working, but abandoned it. InfluxDB is really not suitable for this task for several reasons:
** 5MB/5min limits on free plan mean I can't upload a full log files at will, much less a group of them. Log files may be tens of MB each, and are packed as densely as possible as binary logs; the size of the parsed data structure I'm attempting to post is likely more than 10x the size of the packed log file.
** Logs are not timestamped on engine information system, nor on the Openlog that records the datastream from the EIS. Therefore, points get grouped by processing time. This doesn't really break anything but makes the X-axis rather clumsy and misleading. A plain sequence number might be better. 


# Note
* Working on a laptop where I have to tolerate a dev environment I didn't build, and jupyter installed from pip won't load a kernel, so I've had to install anaconda to get jupyter working. 

# Next Steps


# Related
* [Great Lakes Engine Information System](https://grtavionics.com/product/eis-4000/) to [Openlog](https://www.sparkfun.com/products/13712) [Inverting Adapter](https://github.com/ersatzavian/EIS_Inverting_Adapter)

NETCDF exercise
###################

In this folder there are the results of the netcdf exercise. The first data used to do the exercise were taken from

.. code::
   
    http://test.opendap.org/opendap/data/nc/coads_climatology.nc

while the largest file used was taken from

.. code::
   
   http://thredds.daac.ornl.gov/thredds/dodsC/ornldaac/551/climate_1901_1998_PRE.nc4.html

The *script.sh* file shows the way in which are obtained the data for the plots. We compress the downloaded data with a growing compression factor (-d num flag) and then store the size of the compressed file in a correspondent file. The compression is also done with the shuffling of variables (-s flag) that tipically allow a better compression of the file.

We are interested in the size of the compressed files and in the time needed to decompress each file. It is trivial obtain the size of the compressed files. It can be obtained with the execution of the following command:

.. code::
   
   du -b name_file

which return the real size of the file in bytes (like in the output of ls -l). Instead, the measure of the time needed to decompress a file is a bit more complicate. In particular, for each file we measure for 10 times the time needed to perform the following command:

.. code::
   
   ncdump namefile > /dev/null

The redirection of the output to /dev/null allows to measure only the time to decompress the file without taking into account of the time needed to write the output into another file. The measures are done for both the shuffled and non-shuffled files.

RESULTS
========

The first obtained results are the ones referring to a file with initial size of 3 MB. The following plot shows the size of the compressed files as a function of the compression factor:

.. image:: size_comparison.png
   :height: 60px
   :width: 60px
   :scale:  50%
   :alt: Size comparison for compressed files
   :align: center
	   
As expected, the size of the shuffled files is less then the other. The following plot shows the time needed to decompress the file as a function of the compression factor:

.. image:: time_comparison.png
   :height: 60px
   :width: 60px
   :scale:  50%
   :alt: Time needed to decompress the file
   :align: center

This behavior is not what we are expected: we expect a time increases with the compression factor. This behavior can be explained with the small dimension of the file.

Indeed, the usage of the file found at the second link, produces the following plots.

.. image:: long_size_comparison.png
   :height: 60px
   :width: 60px
   :scale:  50%
   :alt: Size comparison for compressed files
   :align: center

This is for the comparison of the size. The following, instead, is for the time needed to decompress the files:

.. image:: long_time_comparison.png
   :height: 60px
   :width: 60px
   :scale:  50%
   :alt: Time needed to decompress the file
   :align: center

This is the expected behavior.

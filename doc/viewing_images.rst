.. _viewing_images:

Viewing Images
==============

.. rubric:: How to use other packages with pydicom to view DICOM images

Introduction
------------

pydicom is mainly concerned with getting at the DICOM data elements in files,
but it is often desirable to view pixel data as an image.
There are several options:

  * Use any of the many `DICOM viewer
    <http://www.dclunie.com/medical-image-faq/html/part8.html#DICOMFileConvertorsAndViewers>`_
    programs available
  * use pydicom with `matplotlib <https://matplotlib.org/>`_
  * use pydicom with python's stdlib `Tkinter <https://docs.python.org/3.4/library/tkinter.html>`_ module.
  * use pydicom with the `Python Imaging Library (PIL)
    <http://www.pythonware.com/products/pil/>`_
  * use pydicom with `wxPython <http://www.wxpython.org/>`_

Using pydicom with matplotlib
-----------------------------

matplotlib is available at https://matplotlib.org/. It
can take 2-d image information from ``Dataset.pixel_array`` and display it.
Here is an example::

  >>> import matplotlib.pyplot as plt
  >>> import pydicom
  >>> from pydicom.data import get_testdata_files
  >>> filename = get_testdata_files("CT_small.dcm")[0]
  >>> ds = pydicom.read_file(filename)
  >>> plt.imshow(ds.pixel_array, cmap=plt.cm.bone) # doctest: +ELLIPSIS
  <matplotlib.image.AxesImage object at ...>

.. image:: ./auto_examples/input_output/images/sphx_glr_plot_read_dicom_001.png
   :target: ./auto_examples/input_output/plot_printing_dataset.html
   :scale: 60
   :align: center

Thanks to Roy Keyes for pointing out how to do this.

Using pydicom with Tkinter
--------------------------

The program `pydicom_Tkinter.py
<https://github.com/pydicom/contrib-pydicom/blob/master/viewers/pydicom_Tkinter.py>`_
in the ``contrib-pydicom`` repository demonstrates how to show an image using the
Tkinter graphics system, which comes standard with most python installs.
It creates a Tkinter PhotoImage in a Label widget or a user-supplied widget.

Using pydicom with Python Imaging Library (PIL)
-----------------------------------------------

The module `pydicom_PIL.py
<https://github.com/pydicom/contrib-pydicom/blob/master/viewers/pydicom_PIL.py>`_
in the ``contrib-pydicom`` repository
uses PIL's ``Image.show()`` method after creating an Image instance
from the pixel data and some basic information about it (bit depth, LUTs, etc)

Using pydicom with wxPython
---------------------------

The module `imViewer-Simple.py
<https://github.com/pydicom/contrib-pydicom/blob/master/viewers/imViewer_Simple.py>`
in the ``contrib-pydicom`` repository uses wxPython (also PIL, but it notes that it
may not be strictly necessary) to display an image from a pydicom dataset.
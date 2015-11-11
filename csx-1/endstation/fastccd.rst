Fast CCD Detector
=================

Specifications
--------------

*   Pixel Size: 30 |micron| x 30 |micron|
*   Active Area: 960 pixels x 960 pixels
*   The center, black stripe is artificial (over scan function)
*   192 independent outputs (480 rows x 10 columns)
*   10 columns = super-column
*   Frame Store Mode
*   Pixel readout time: 500 us
*   Digitization time: 2 us at 120 Hz
*   100 Hz maximum data collection

.. |micron| unicode:: 0x00B5
    :rtrim:

.. figure:: fcric.png
   :alt: LBNL FCRIC Circuit

.. table:: Data Format

    +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+
    | 15| 14| 13| 12| 11| 10| 09| 08| 07| 06| 05| 04| 03| 02| 01| 00| 
    +===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+===+
    | G1| G0|ERR|D12|D11|D10|D09|D08|D07|D06|D05|D04|D03|D02|D01|D00|
    +---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+---+

.. table:: Gain Setting

    == == ==== ==========
    G1 G0 Gain Pre-factor
    == == ==== ==========
    0  0  x8   x1
    1  0  x2   x4
    1  1  x1   x8
    == == ==== ==========

.. math::
    I_{corr} = (I{meas} * G) - BG

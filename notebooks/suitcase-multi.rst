
iPython Notebook To Export CSX Data as a suitcase
=================================================

.. code:: python

    from dataportal import DataBroker as db
    import os
    import sys
    from suitcase import export
    from time import sleep
    from __future__ import print_function

.. code:: python

    FILENAME = 'scan-'  # no file extension; we take care of that below
    SCAN_ID = 52326
    START =  SCAN_ID
    STOP = 52329
    OVERWRITE = True  # If true, I will delete the file FILENAME if it exists.

.. code:: python

    # sanity check that we can see the GPFS. If this fails, give up and email Rob Petkus. There is no hope.
    !ls '/GPFS/'


.. parsed-literal::

    xf23id


.. code:: python

    h = db[SCAN_ID]
    h





.. raw:: html

    
    <table>
    
      <tr>
        <th> descriptors </th>
        <td>
          
              
                [{'uid': 'affcd928-f16d-4d1a-b91b-36d9a5229d76', '_name': 'EventDescriptor', 'time': 1444989136.6295948, 'run_start': '8c293b62-b015-42a9-bcf5-77daeadc205f', 'data_keys': {'npty': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif:Lens-Ax:TopY}Mtr.RBV'}, 'fccd_image_lightfield': {'shape': [100, 960, 960], 'dtype': 'array', 'external': 'FILESTORE:', 'source': 'PV:XF:23ID1-ES{FCCD}'}, 'fccd_stats_total3': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{FCCD}Stats3:Total_RBV'}, 'theta': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif-Ax:Th}Mtr.RBV'}, 'sclr_chan4': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Sclr:1}.S4'}, 'sclr_chan1': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Sclr:1}.S1'}, 'temp_b': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{TCtrl:1-Chan:B}T-I'}, 'sclr_chan3': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Sclr:1}.S3'}, 'npbz': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif:Lens-Ax:BtmZ}Mtr.RBV'}, 'pgm_energy': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-OP{Mono}Enrgy-I'}, 'sy': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif-Ax:SY}Pos-RB'}, 'fccd_acquire_time': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{FCCD}cam1:AcquireTime_RBV'}, 'npby': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif:Lens-Ax:BtmY}Mtr.RBV'}, 'sclr_chan7': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Sclr:1}.S7'}, 'delta': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif-Ax:Del}Mtr.RBV'}, 'sz': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif-Ax:SZ}Pos-RB'}, 'fccd_acquire_period': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{FCCD}cam1:AcquirePeriod_RBV'}, 'say': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif-Ax:Y}Mtr.RBV'}, 'epu2_phase': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID-ID{EPU:2-Ax:Phase}Pos-I'}, 'nptx': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif:Lens-Ax:TopX}Mtr.RBV'}, 'sclr_chan6': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Sclr:1}.S6'}, 'eta': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Diag:1-Ax:Eta}Mtr.RBV'}, 'nptz': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif:Lens-Ax:TopZ}Mtr.RBV'}, 'sclr_chan5': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Sclr:1}.S5'}, 'sclr_time': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Sclr:1}.T'}, 'gamma': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif-Ax:Gam}Mtr.RBV'}, 'sclr_chan2': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Sclr:1}.S2'}, 'fccd_stats_total4': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{FCCD}Stats4:Total_RBV'}, 'temp_a': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{TCtrl:1-Chan:A}T-I'}, 'epu2_gap': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID-ID{EPU:2-Ax:Gap}Pos-I'}, 'fccd_stats_total5': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{FCCD}Stats5:Total_RBV'}, 'ring_curr': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID-SR{}I-I'}, 'sclr_chan8': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Sclr:1}.S8'}, 'fccd_stats_total2': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{FCCD}Stats2:Total_RBV'}, 'fccd_stats_total1': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{FCCD}Stats1:Total_RBV'}, 'sx': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif-Ax:X}Mtr.RBV'}, 'saz': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif-Ax:Z}Mtr.RBV'}, 'npbx': {'shape': [], 'dtype': 'number', 'source': 'PV:XF:23ID1-ES{Dif:Lens-Ax:BtmX}Mtr.RBV'}}}]
              
            
        </td>
      </tr>
    
      <tr>
        <th> start </th>
        <td>
          
            <table>
              
      <tr>
        <th> beamline_id </th>
        <td>
          
              
                CSX
              
            
        </td>
      </tr>
    
      <tr>
        <th> config </th>
        <td>
          
            <table>
              
            </table>
            
        </td>
      </tr>
    
      <tr>
        <th> group </th>
        <td>
          
              
                
              
            
        </td>
      </tr>
    
      <tr>
        <th> owner </th>
        <td>
          
              
                xf23id1
              
            
        </td>
      </tr>
    
      <tr>
        <th> project </th>
        <td>
          
              
                
              
            
        </td>
      </tr>
    
      <tr>
        <th> sample </th>
        <td>
          
            <table>
              
            </table>
            
        </td>
      </tr>
    
      <tr>
        <th> scan_args </th>
        <td>
          
            <table>
              
      <tr>
        <th> delay </th>
        <td>
          
              
                0
              
            
        </td>
      </tr>
    
      <tr>
        <th> detectors </th>
        <td>
          
              
                [EpicsMotor(name='theta', record='XF:23ID1-ES{Dif-Ax:Th}Mtr'), EpicsMotor(name='delta', record='XF:23ID1-ES{Dif-Ax:Del}Mtr'), EpicsMotor(name='gamma', record='XF:23ID1-ES{Dif-Ax:Gam}Mtr'), EpicsMotor(name='sx', record='XF:23ID1-ES{Dif-Ax:X}Mtr'), PVPositioner(name='sy', setpoint='XF:23ID1-ES{Dif-Ax:SY}Pos-SP', readback='XF:23ID1-ES{Dif-Ax:SY}Pos-RB', stop='XF:23ID1-ES{Dif-Cryo}Cmd:Stop-Cmd', stop_val=1, put_complete=True, settle_time=0.05, limits=(0, 0)), PVPositioner(name='sz', setpoint='XF:23ID1-ES{Dif-Ax:SZ}Pos-SP', readback='XF:23ID1-ES{Dif-Ax:SZ}Pos-RB', stop='XF:23ID1-ES{Dif-Cryo}Cmd:Stop-Cmd', stop_val=1, put_complete=True, settle_time=0.05, limits=(0, 0)), EpicsMotor(name='say', record='XF:23ID1-ES{Dif-Ax:Y}Mtr'), EpicsMotor(name='saz', record='XF:23ID1-ES{Dif-Ax:Z}Mtr'), EpicsSignal(name='temp_a', read_pv='XF:23ID1-ES{TCtrl:1-Chan:A}T-I', rw=False, string=False, limits=False, put_complete=False, pv_kw={}, auto_monitor=None), EpicsSignal(name='temp_b', read_pv='XF:23ID1-ES{TCtrl:1-Chan:B}T-I', rw=False, string=False, limits=False, put_complete=False, pv_kw={}, auto_monitor=None), PVPositioner(name='pgm_energy', setpoint='XF:23ID1-OP{Mono}Enrgy-SP', readback='XF:23ID1-OP{Mono}Enrgy-I', stop='XF:23ID1-OP{Mono}Cmd:Stop-Cmd', stop_val=1, put_complete=True, settle_time=0.05, limits=(200, 2200)), PVPositioner(name='epu2_gap', setpoint='XF:23ID-ID{EPU:2-Ax:Gap}Pos-SP', readback='XF:23ID-ID{EPU:2-Ax:Gap}Pos-I', stop='SR:C23-ID:G1A{EPU:2-Ax:Gap}-Mtr.STOP', stop_val=1, put_complete=True, settle_time=0.05, limits=(0, 0)), EpicsSignal(name='ring_curr', read_pv='XF:23ID-SR{}I-I', rw=False, string=False, limits=False, put_complete=False, pv_kw={}, auto_monitor=None), EpicsMotor(name='npbx', record='XF:23ID1-ES{Dif:Lens-Ax:BtmX}Mtr'), EpicsMotor(name='npby', record='XF:23ID1-ES{Dif:Lens-Ax:BtmY}Mtr'), EpicsMotor(name='npbz', record='XF:23ID1-ES{Dif:Lens-Ax:BtmZ}Mtr'), EpicsMotor(name='nptx', record='XF:23ID1-ES{Dif:Lens-Ax:TopX}Mtr'), EpicsMotor(name='npty', record='XF:23ID1-ES{Dif:Lens-Ax:TopY}Mtr'), EpicsMotor(name='nptz', record='XF:23ID1-ES{Dif:Lens-Ax:TopZ}Mtr'), EpicsScaler(name='sclr', record='XF:23ID1-ES{Sclr:1}', numchan=8), PVPositioner(name='epu2_phase', setpoint='XF:23ID-ID{EPU:2-Ax:Phase}Pos-SP', readback='XF:23ID-ID{EPU:2-Ax:Phase}Pos-I', stop='SR:C23-ID:G1A{EPU:2-Ax:Phase}-Mtr.STOP', stop_val=1, put_complete=True, settle_time=0.05, limits=(0, 0)), EpicsMotor(name='eta', record='XF:23ID1-ES{Diag:1-Ax:Eta}Mtr'), AreaDetectorFileStoreHDF5(name='fccd', basename='XF:23ID1-ES{FCCD}', stats=[1, 2, 3, 4, 5], shutter=None, shutter_rb=None, shutter_val=None, file_path='/GPFS/xf23id/xf23id1/fccd_data/', ioc_file_path=None)]
              
            
        </td>
      </tr>
    
      <tr>
        <th> num </th>
        <td>
          
              
                1
              
            
        </td>
      </tr>
    
            </table>
            
        </td>
      </tr>
    
      <tr>
        <th> scan_id </th>
        <td>
          
              
                52326
              
            
        </td>
      </tr>
    
      <tr>
        <th> scan_type </th>
        <td>
          
              
                Count
              
            
        </td>
      </tr>
    
      <tr>
        <th> time </th>
        <td>
          
              
                a month ago (2015-10-16T05:48:38.831460)
              
            
        </td>
      </tr>
    
      <tr>
        <th> uid </th>
        <td>
          
              
                8c293b62-b015-42a9-bcf5-77daeadc205f
              
            
        </td>
      </tr>
    
            </table>
            
        </td>
      </tr>
    
      <tr>
        <th> stop </th>
        <td>
          
            <table>
              
      <tr>
        <th> exit_status </th>
        <td>
          
              
                success
              
            
        </td>
      </tr>
    
      <tr>
        <th> reason </th>
        <td>
          
              
                
              
            
        </td>
      </tr>
    
      <tr>
        <th> run_start </th>
        <td>
          
              
                8c293b62-b015-42a9-bcf5-77daeadc205f
              
            
        </td>
      </tr>
    
      <tr>
        <th> time </th>
        <td>
          
              
                a month ago (2015-10-16T05:52:17.810649)
              
            
        </td>
      </tr>
    
      <tr>
        <th> uid </th>
        <td>
          
              
                b531b74e-4895-4e6c-8eed-a67b8c6bd67c
              
            
        </td>
      </tr>
    
            </table>
            
        </td>
      </tr>
    
    </table>




.. code:: python

    for SCAN_ID in range(START,STOP+1):
        h = db[SCAN_ID]
        SCANNUMBER=str(SCAN_ID)
        fn = '{filename}.h5'.format(filename=FILENAME+SCANNUMBER)
        if os.path.isfile(fn):
            if OVERWRITE:
                os.remove(fn)
            else:
                raise Exception("That file already exists. Set OVERWRITE = True if you want to overwrite.")
        export([h], fn)



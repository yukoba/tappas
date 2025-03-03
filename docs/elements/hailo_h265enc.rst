Hailo H265 Encoder
==================

Overview
--------

| HailoH265Enc is an element which enables the user to encode a video in h265 coding format, using the **Hailo-15 encoding hardware accelerator**.
| **Currently only NV12 pipelines are supported by HailoH265Enc.**


Parameters
^^^^^^^^^^

| The hailoh265enc element provides a veriaty of properties that control the encoding performance and quality.
| Among those properties are the encoding profile, bitrate, encoding level, etc...
| When a property has the "changeable in NULL, READY, PAUSED or PLAYING state" flag, it means that it can be changed during the pipeline.

.. image:: ../resources/dynamic_param.png

| Changes to such properties during the pipeline will be updated at the end of the group of images (GOP).
| A change in bitrate during the pipeline will be applied at the end of the GOP, for instance.
| It is important to note that forcing a keyframe will reset the GOP and the new property will take effect at the end of the next GOP.

Hierarchy
---------

.. code-block::

  GObject
  +----GInitiallyUnowned
        +----GstObject
              +----GstElement
                    +----GstVideoEncoder
                          +----GstHailoH265Enc

  Implemented Interfaces:
    GstPreset

  Pad Templates:
    SINK template: 'sink'
      Availability: Always
      Capabilities:
        video/x-raw
                format: NV12
                width: [ 16, 2147483647 ]
                height: [ 16, 2147483647 ]
                framerate: [ 0/1, 2147483647/1 ]
    
    SRC template: 'src'
      Availability: Always
      Capabilities:
        video/x-h265
                stream-format: byte-stream
                alignment: au
                profile: { (string)main, (string)main-still-picture, (string)main-intra, (string)main-10, (string)main-10-intra }

  Element has no clocking capabilities.
  Element has no URI handling capabilities.

  Pads:
    SINK: 'sink'
      Pad Template: 'sink'
    SRC: 'src'
      Pad Template: 'src'

  Element Properties:
    bframe-qp-delta     : QP difference between BFrame QP and target QP, -1 = Disabled
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Integer. Range: -1 - 51 Default: 0 
    bitrate             : Target bitrate for rate control in bits/second
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 10000 - 40000000 Default: 40000000 
    bitvar-range-b      : Percent variations over average bits per frame for B frame
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 0 - 2000 Default: 2000 
    bitvar-range-i      : Percent variations over average bits per frame for I frame
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 0 - 2000 Default: 2000 
    bitvar-range-p      : Percent variations over average bits per frame for P frame
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 0 - 2000 Default: 2000 
    block-rc-size       : Size of block rate control
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Enum "GstHailoH265EncBlockRcSize" Default: 0, "64x64"
                            (0): 64x64            - 64X64
                            (1): 32x32            - 32X32
                            (2): 16x16            - 16X16
    compressor          : Enable/Disable Embedded Compression
                          flags: readable, writable
                          Enum "GstHailoH265EncCompressor" Default: 3, "enable-both"
                            (0): disable          - Disable Compression
                            (1): enable-luma      - Only Enable Luma Compression
                            (2): enable-chroma    - Only Enable Chroma Compression
                            (3): enable-both      - Enable Both Luma and Chroma Compression
    ctb-rc              : Adaptive adjustment of QP inside frame
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Boolean. Default: false
    fixed-intra-qp      : Use fixed QP value for every intra frame in stream, 0 = disabled
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 0 - 51 Default: 0 
    gop-length          : GOP Length
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 1 - 300 Default: 30 
    gop-size            : GOP Size (1 - No B Frames)
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 1 - 8 Default: 1 
    hrd                 : Restricts the instantaneous bitrate and total bit amount of every coded picture.
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Boolean. Default: false
    hrd-cpb-size        : Buffer size used by the HRD model in bits
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 10000 - 40000000 Default: 10000000 
    intra-pic-rate      : I frames interval (0 - Dynamic IDR Interval)
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 0 - 300 Default: 30 
    intra-qp-delta      : QP difference between target QP and intra frame QP
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Integer. Range: -51 - 51 Default: -5 
    level               : level to encoder
                          flags: readable, writable
                          Enum "GstHailoH265EncLevel" Default: 153, "level-5-1"
                            (30): level-1          - Level 1
                            (60): level-2          - Level 2
                            (63): level-2-1        - Level 2.1
                            (90): level-3          - Level 3
                            (93): level-3-1        - Level 3.1
                            (120): level-4          - Level 4
                            (123): level-4-1        - Level 4.1
                            (150): level-5          - Level 5
                            (153): level-5-1        - Level 5.1
    min-force-key-unit-interval: Minimum interval between force-keyunit requests in nanoseconds
                          flags: readable, writable
                          Unsigned Integer64. Range: 0 - 18446744073709551615 Default: 0 
    monitor-frames      : How many frames will be monitored for moving bit rate. Default is using framerate
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 10 - 120 Default: 0 
    name                : The name of the object
                          flags: readable, writable, 0x2000
                          String. Default: "hailoh265enc0"
    parent              : The parent of the object
                          flags: readable, writable, 0x2000
                          Object of type "GstObject"
    picture-rc          : Adjust QP between pictures
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Boolean. Default: true
    picture-skip        : Allow rate control to skip pictures
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Boolean. Default: false
    profile             : profile to encoder
                          flags: readable, writable
                          Enum "GstHailoH265EncProfile" Default: 0, "main"
                            (0): main             - Main Profile
                            (1): main-still-picture - Main Still Picture Profile
                            (2): main-10          - Main 10 Profile
    qos                 : Handle Quality-of-Service events from downstream
                          flags: readable, writable
                          Boolean. Default: false
    qp-hdr              : Initial target QP, -1 = Encoder calculates initial QP
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Integer. Range: -1 - 51 Default: 26 
    qp-max              : Maximum frame header QP
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 0 - 51 Default: 51 
    qp-min              : Minimum frame header QP
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 0 - 51 Default: 0 
    roi-area1           : Specifying rectangular area of CTBs as Region Of Interest with lower QP, left:top:right:bottom:delta_qp format 
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          String. Default: null
    roi-area2           : Specifying rectangular area of CTBs as Region Of Interest with lower QP, left:top:right:bottom:delta_qp format 
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          String. Default: null
    tol-moving-bitrate  : Percent tolerance over target bitrate of moving bit rate
                          flags: readable, writable, changeable in NULL, READY, PAUSED or PLAYING state
                          Unsigned Integer. Range: 0 - 2000 Default: 2000 

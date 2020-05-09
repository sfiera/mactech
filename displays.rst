Mac Tech: Displays
==================

.. contents::

Summary
-------

Pinout
~~~~~~

.. table::
   :widths: auto

   ================== ===== =====
   Description        DA-15 VGA
   ================== ===== =====
   Red signal         2     1
   Red ground         1     6
   Green signal       5     2
   Green ground       6     7
   Blue signal        9     3
   Blue ground        13    8
   HSync signal       15    13
   HSync ground       14    5
   VSync signal       12    14
   CSync signal       3     NC
   VSync/CSync ground 11    10
   Sense pin          4     NC
   Sense pin          7     NC
   Sense pin          10    NC
   Unused             8     NC
   Chassis ground     Shell Shell
   ================== ===== =====

I’ve seen schematics with the RGB grounds (pins 1, 6, and 13) wired to
the shell, and observed this in an adapter in practice.

Sense pins
~~~~~~~~~~

.. table::
   :widths: auto

   ====  ==============  ===============  ================  ==============================
   Gen.  Mode            Resolution       Connections       Example
   ====  ==============  ===============  ================  ==============================
   1     8”              512×342          N/A               Macintosh 128k internal
   2     12”             512×384          G↔︎4↔︎10            Macintosh 12″ RGB Display
   2     NTSC [#ntsc]_   512×384          G↔︎4↔︎7             North American TV
   2     13”             640×480          G↔︎4               AppleColor High-Resolution RGB Monitor
   2     Apple Portrait  640×870          G↔︎7↔︎10            Macintosh Portrait Display
   2     Color Portrait  640×870          G↔︎7               Radius Full Page Display
   2     21” Mono        1152×870         G↔︎10
   2     21” Color       1152×870         G↔︎4↔︎7↔︎10
   3     VGA [#vga]_     800×600          7↔︎10              Non-Apple monitor
   3     16”             832×624          4↔︎10
   3     19”             1024×768         4↔︎7
   3     PAL [#pal]_     512×384          4↔︎7↔︎10           European TV
   4     Up to 13”       Up to 640×480    G↔︎4              (same as 12” above)
   4     Up to 14”       Up to 800×600    G↔︎4, 7→10, 10→7  Apple Multiple Scan 14 Display
   4     Up to 17”       Up to 1024×768   G↔︎4, 7→10        Apple Multiple Scan 15 Display
   4     Up to 21”       Up to 1152×870?  G↔︎4, 10→7        Apple Multiple Scan 20 Display
   ====  ==============  ===============  ================  ==============================

.. [#ntsc] Overscan 640×480; underscan 512×384.
.. [#vga] Defaults to 640×480; change to 800×600 and restart.
.. [#pal] Overscan 640×480; underscan 512×384. saragossa.net Also lists
   a second PAL option, connecting 4↔︎7, 7→10, but does not say what the
   difference from the mode listed above is.

Details
-------

Generation 1: Compact Mac
~~~~~~~~~~~~~~~~~~~~~~~~~

The original Macintosh had a single resolution: 512×342.

.. list-table::
   :widths: auto
   :header-rows: 1
   :stub-columns: 1

   * * Size
     * 8”
   * * Visible area
     * 512×342
   * * Total area
     * 704×370
   * * Scan rate
     * 60.15 Hz
   * * Line rate
     * 22.25 kHz
   * * Dot clock
     * 15.6672 MHz [#15.6672]_
   * * Width
     * 512px
   * * Total width
     * 704px
   * * HBlank
     * 192px
   * * Front porch
     * 14px
   * * HSync
     * 288px
   * * Back porch
     * -110px [#neg-porch]_
   * * Height
     * 342px
   * * Total height
     * 370px
   * * VBlank
     * 28px
   * * Front porch
     * 0px
   * * VSync
     * 4px
   * * Back porch
     * 24px

.. [#15.6672] 15.6672 MHz is twice the clock rate of the original
   Macintosh, or 68 * 32 * 7200 Hz.
.. [#neg-porch] The HSync pulse is longer than the the HBlank interval,
   so it overlaps the visible part of the scan line, and there is no
   back porch.

Generation 2: External Displays
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Macintosh II required an external monitor, and connected to it
through a DA-15 video port [#iigs]_. Aside from the signal and ground
pins, three `sense pins`_ were used so that the computer would know what
kind of monitor was connected. Any or all of them could be grounded,
yielding 8 (2³) possible combinations:

1. 13” (640×480)
2. Color Portrait (640×870)
3. NTSC (512×384)
4. 21” Mono (1152×870)
5. 12” (512×384)
6. Apple Portrait (640×870)
7. 21” Color (1152×870)
8. No monitor connected

.. list-table::
   :widths: auto
   :header-rows: 1
   :stub-columns: 1

   * * Size
     * 12”
     * 13” 16-bit [#16bit]_
     * 13”
     * Portrait [#portrait]_
     * 21” [#21]_
   * * Visible area
     * 512×384
     * 640×400
     * 640×480
     * 640×870
     * 1152×870
   * * Total area
     * 704×370
     * 864×525
     * 864×525
     * 832×918
     * 1456×915
   * * Scan rate
     * 60.15 Hz
     * 66.67 Hz
     * 66.67 Hz
     * 75 Hz
     * 75 Hz
   * * Line rate
     * 24.48 kHz [#24.48]_
     * 35.0 kHz
     * 35.00 kHz
     * 68.9 kHz
     * 68.68 kHz
   * * Dot clock
     * 15.6672 MHz
     * 30.24 MHz
     * 30.24 MHz
     * 57.2832 MHz
     * 100 MHz
   * * Width
     * 512px
     * 640px
     * 640px
     * 640px
     * 1152px
   * * Total width
     * 640px
     * 864px
     * 864px
     * 832px
     * 1456
   * * HBlank
     * 128px
     * 224px
     * 224px
     * 192px
     * 304px
   * * Front porch
     * 16px
     * 64px
     * 64px
     * 32px
     * 32px
   * * HSync
     * 32px
     * 64px
     * 64px
     * 80px
     * 128px
   * * Back porch
     * 80px
     * 96px
     * 96px
     * 80px
     * 144px
   * * Height
     * 384px
     * 400px
     * 480px
     * 870px
     * 870px
   * * Total height
     * 407px
     * 525px
     * 525px
     * 918px
     * 915px
   * * VBlank
     * 32px
     * 125px
     * 45px
     * 48px
     * 45px
   * * Front porch
     * 1px
     * 43px
     * 3px
     * 3px
     * 3px
   * * VSync
     * 3px
     * 3px
     * 3px
     * 3px
     * 3px
   * * Back porch
     * 19px
     * 79px
     * 39px
     * 42px
     * 39px

.. [#iigs] Was the IIgs the first to use DA-15, though?
.. [#16bit] This is an alternate version of 640×480 available on some
   machines with low amounts of VRAM, allowing 16-bit color at the cost
   of screen space. The parameters are the same as 640×480, letterboxing
   it by adding 40px each to the front and back porch.
.. [#portrait] saragossa.net lists both “Apple” and “Color” (e.g.
   Radius) versions with different sense codes. I don’t know what
   differences exist.
.. [#21] saragossa.net lists both “Mono” and “Color” versions with
   different sense codes. I don’t know what differences exist.
.. [#24.48] While this resolution shares the overall scan rate (60.15
   Hz) and dot clock (15.6672) with the Compact 8” resolution, the
   line rate differs. Despite having the same total pixel size, the
   total area is more squarish. Reusing the 8” screen’s parameters would
   have been impossible, because its total height is less than 384px.

Generation 3: More Displays
~~~~~~~~~~~~~~~~~~~~~~~~~~~

With more resolutions, new sense codes were needed. In order to prevent
older computers from detecting these newer monitors and trying to
display to them, the three sense pins were left ungrounded, and some
combination of them were tied together, yielding 4 additional
possibilities:

1. 19” (1024×768)
2. VGA (640×480 or 800×600)
3. 16” (832×624)
4. PAL

.. list-table::
   :widths: auto
   :header-rows: 1
   :stub-columns: 1

   * * Size
     * 16”
     * 19”
   * * Visible area
     * 832×624
     * 1024×768
   * * Total area
     * 1152×667
     * 1328×804
   * * Scan rate
     * 75 Hz
     * 75 Hz
   * * Line rate
     * 49.73 kHz
     * 60.24 kHz
   * * Dot clock
     * 57.2832 MHz
     * 80 MHz
   * * Width
     * 832px
     * 1024px
   * * Total width
     * 1152px
     * 1328px
   * * HBlank
     * 320px
     * 304px
   * * Front porch
     * 32px
     * 32px
   * * HSync
     * 64px
     * 96px
   * * Back porch
     * 224px
     * 176px
   * * Height
     * 624px
     * 768px
   * * Total height
     * 667px
     * 804px
   * * VBlank
     * 43px
     * 36px
   * * Front porch
     * 1px
     * 3px
   * * VSync
     * 3px
     * 3px
   * * Back porch
     * 39px
     * 30px

Generation 4: Multi-resolution
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Eventually monitors became able to support multiple resolutions. The
minimum resolution supported by such monitors was 640×480, so the 13”
sense code (grounding pin 4) became the baseline for multiple-resolution
monitors. Then, diodes were wired between pins 7 and 10:

1. No diodes for a 13” (640×480), preserving compatibility [#compat]_
2. Both directions for a 14” (max 800×600)
3. From 7 to 10 for a 17” (max 1024×768)
4. From 10 to 7 for a 21” (max 1152×870)

.. [#compat] Though, older monitors would probably require a 66.67 Hz
   scan rate, so I don’t know if it would be safe to output a different
   rate.

Appendix: Apple IIe
~~~~~~~~~~~~~~~~~~~

Machines that can host an Apple IIe card are capable of outputting
560×384, which is double the IIe’s 280×192 “Hi Resolution” graphics
mode:

.. list-table::
   :widths: auto
   :header-rows: 1
   :stub-columns: 1

   * * Size
     * Quad Hi-Res
   * * Visible area
     * 560×384
   * * Total area
     * 704×407
   * * Scan rate
     * 60.15 Hz
   * * Line rate
     * 24.48 kHz
   * * Dot clock
     * 17.2340 MHz
   * * Width
     * 560px
   * * Total width
     * 704px
   * * HBlank
     * 144px
   * * Front porch
     * 16px
   * * HSync
     * 48px
   * * Back porch
     * 80px
   * * Height
     * 384px
   * * Total height
     * 407px
   * * VBlank
     * 23px
   * * Front porch
     * 1px
   * * VSync
     * 3px
   * * Back porch
     * 19px

Adapters
--------

Generic adapter
~~~~~~~~~~~~~~~

.. image:: images/display-adapter.svg

For a VGA adapter:

1. Omit the dip switches and diodes.
2. Wire Sense1 and Sense2 (DA-15 pins 7 and 10) together directly.

For a multi-scan adapter:

1. Omit the dip switches.
2. Wire VGAGnd and Sense0 (D-15 pin 4 and ground) together directly.
3. Wire diodes between Sense1 and Sense2 (DA-15 pins 7 and 10) according
   to the maximum resolution of the monitor:

   * 1152×870: cathode on Sense1 (DA-15 pin 7)
   * 1024×768: cathode on Sense2 (DA-15 pin 10)
   * 800×600: two diodes, both ways
   * 640×480: no diodes

See Also
--------

* http://www.saragossa.net/intfcing.html
* http://www.codesrc.com/mediawiki/index.php/Macintosh_VGA
* http://www.3dexpress.de/displayconfigx/timings.html
* http://mirror.informatimago.com/next/developer.apple.com/documentation/Hardware/Developer_Notes/Macintosh_CPUs-68K_Desktop/Mac_LC_III.pdf

..  -*- tab-width: 3; fill-column: 72 -*-

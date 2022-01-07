tarbot
======

.. contents::
    :local:
    :backlinks: none

Introduction
------------

Tarbot (an acronym for "**T**\ arbot: **a** **r**\ andom **b**\ unch **o**\ f **t**\ ools") is a collection of utility bash scripts.

The rest of this document consists of the ``--help`` output of the scripts.

aloop
-----
::

  Usage: aloop MESSAGE NUMITERATIONS

  'aloop' runs a 'for' loop NUMITERATIONS times.
  At every iteration, MESSAGE is printed to stdout, together with
  the iteration number, and the script sleeps for 1 second before
  going to the next iteration.

  Example:
      $ aloop Hello 3
      Hello 1
      Hello 2
      Hello 3

gm2png
------
::

  Usage: gm2png TYPE Z XMIN XMAX YMIN YMAX [FILENAME_PREFIX] [LANG]

  'gm2png' downloads individual tiles from Google Maps, stitches
  them together to form a mosaic and saves the result in a .png file.

  TYPE is either 'sat' for satellite imagery, 'ter' for terrain, 'map' for
  street map or 'hyb' for hybrid (satellite/street).

  Z is the zoom level.

  The tiles form a rectangular area determined by XMIN, XMAX, YMIN
  and YMAX. The top left tile is at (XMIN,YMIN) and the bottom right
  tile at (XMAX, YMAX).

  The downloaded tiles are stored in '~/build/gm2png/tiles'. Saved
  tiles are not downloaded again in subsequent runs of 'gm2png'.

  If FILENAME_PREFIX is specified, the filename of the saved .png
  file will start with FILENAME_PREFIX, followed by the values of
  the other arguments.

  The optional argument LANG allows you to change the annotations on
  the map to another language, if available. If you want to specify
  LANG without specifying FILENAME_PREFIX, use '-' for the latter.

  Examples:

  Creating a street map:

      $ gm2png map 15 16831 16834 10903 10907

  The same street map, but with some annotations in Dutch instead of English:

      $ gm2png map 15 16831 16834 10903 10907 - nl

htmlent-dec
-----------
::

  Usage: ... | htmlent-dec

  'htmlent-dec' converts html entities to their corresponding
  characters.

  Example:

    $ echo "Fish &amp; Chips" | htmlent-dec
    Fish & Chips


images2pdf
----------
::

  Usage: images2pdf OUTPUTFILE [DENSITY]

  'images2pdf' takes a list of image files from stdin
  and converts them to a pdf file (OUTPUTFILE), one page per
  image.
  The paper size is A4.
  The resolution and density (needed for conversion) are read
  from the input files. If the files don't contain density
  information, it can be given as the argument DENSITY.
  An example of a valid density string (for 300 dpi): 300x300

mcut
----
::

  Usage: mcut ARGS

  'mcut' works the same as 'cut',
  but allows for multi-character delimiters.

owntree
-------
::

  Usage: owntree [DIR] [USERNAME] [GROUPNAME]

  'owntree' changes ownership of all files and directories
  in the directory tree rooted at DIR, including DIR itself.

  The ownership is changed to USERNAME:GROUPNAME.

  The default value for GROUPNAME is USERNAME. The default value for USERNAME
  is the current user. The default value for DIR is the current directory.

  The user will be asked interactively for the sudo password.

promptfor
---------
::

  Usage: promptfor PROMPT [silent]

  'promptfor' asks for user input and prints
  the entered text on stdout.
  When 'silent' is added as a second argument, the
  input is not shown on the screen during typing.

punzip
------
::

  Usage: punzip NAME.zip

  'punzip' extracts the contents of NAME.zip
  into a folder called NAME.

  This tool is useful on host machines that don't have
  an 'unzip' tool, but do have 'python3'.

randitem
--------
::

  Usage: randitem ARGS ...

  'randitem' picks an item randomly from the given arguments
  and prints it on stdout.

  Examples:

  $ randitem One Two Three
  Three

  $ words=("One" "Two" "Three")
  $ randitem "${words[@]}"
  Two


randword
--------
::

  Usage: randword [NUM]

  'randword' generates a random word with NUM syllables.
  NUM is 3 by default. Every syllable has 2 letters: one
  consonant and one vowel. A subset of the alphabet is used.

  Example:

  $ randword 4
  dovileka


runjobs
-------
::

  Usage: runjobs WORKER [workers=J] [deadline="YYYY-MM-DD hh:mm:ss"] [count=C] [statusdir=DIR]

  'runjobs'

srvdir
------
::

  Usage: srvdir DIR

  'srvdir' instructs 'lighttpd' to re-load its
  configuration from DIR/etc/lighttpd.conf and to serve
  the direcory DIR/www.
  TODO : backend, scripts

stripesc
--------
::

  Usage: ... | stripesc

  'stripesc' removes bash escape sequences from stdin
  and prints the result on stdout.

  Example:

    $ ls -l --color=always | stripesc | less

  In the above example, without 'stripesc', a lot of
  ugly escape sequences would be visble in 'less'.

subtract
--------
::

  Usage: subtract FILE

  'subtract' subtracts the contents of FILE from stdin
  on a line-by-line basis and prints the result on stdout:
  only lines in stdin that are NOT found in FILE are printed.
  If FILE doesn't exist, the full contents of stdin are printed.

  Note that 2 entire lines in stdin and FILE must match exactly
  in order to be omitted from stdout.

  See also: 'subtractmatch'

subtractmatch
-------------
::

  Usage: subtractmatch FILE

  'subtractmatch' subtracts from stdin the lines containing
  a substring found as a complete line in FILE and prints the
  result on stdout: only lines in stdin that DON'T contain
  substrings found in FILE are printed.
  If FILE doesn't exist, the full contents of stdin are printed.

  See also: 'subtract'

surln
-----
::

  Usage: surln [STRING]

  'surln' surrounds every line of stdin with the
  string given as argument and prints the result on stdout.
  When no argument is given, the string will be the double
  quotes character (ASCII value 34).
  Special characters need to be escaped. Octal or hexadecimal
  notation can be used.

  Examples:

  Surround every line with double quotes:

      $ (echo One; echo Two) | surln
      "One"
      "Two"

  Surround every line with single quotes:

      $ echo Hello | surln \'
      'Hello'

  Do the same as in the previous example, but
  with hexadecimal notation:

      $ echo Hello | surln \x27
      'Hello'


vanilla2spigot
--------------
::

  Usage: vanilla2spigot DIR

  'vanilla2spigot' converts a Minecraft world created in the
  vanilla client to the Spigot folder layout.

  DIR is the vanilla world. A sibling directory called "DIR-spigot"
  is created containing Overworld, Nether & End in Spigot format.


# termtosvg manual page

## SYNOPSIS

<pre>
<b>termtosvg</b> [-g GEOMETRY] [-t TEMPLATE] [--verbose] [--help] [output_file]

<b>termtosvg record</b> [-g GEOMETRY] [--verbose] [--help] [output_file]

<b>termtosvg render</b> [-g GEOMETRY] [-t TEMPLATE] [--verbose] [--help] <i>input_file</i> [output_file]
</pre>

### DESCRIPTION
termtosvg makes recordings of terminal sessions in animated SVG format. If no output
filename is provided, a random temporary filename will be automatically generated.

#### COMMANDS
termtosvg provides the two following commands which may be useful in a few cases:

##### termtosvg record
Record a terminal session in asciicast v2 format. The recording is a text file which
contains timing information as well as what was displayed on the screen during the
terminal session. It may be edited to alter the timing of
the recording or the information displayed on the screen of the terminal.

##### termtosvg render
Render an animated SVG from a recording in asciicast v1 or v2 format. This allows
rendering in SVG format of any recording made with asciinema.

## OPTIONS

##### -g, --screen-geometry=GEOMETRY
Set the terminal screen geometry. GEOMETRY must follow the format COLUMNSxROWS where COLUMNS
and ROWS are positive integers.

##### -t, --template=TEMPLATE
Set the SVG template used for rendering the SVG animation. TEMPLATE may either be
one of the default templates (...) or a path to a valid template.

##### -h, --help
Print usage and exit

##### -v, --verbose
Increase log message verbosity


## SVG TEMPLATES
Templates make it possible to customize the SVG animation produced by termtosvg in a number
of ways including, but not limited to:

* Specifying the color theme and font used for rendering the terminal session
* Adding a custom terminal window frame to the animation to make it look like a real terminal
* Adding JavaScript code to pause the animation, seek to a specific frame, etc


### TEMPLATE STRUCTURE
structure


## ENVIRONMENT
##### SHELL
termtosvg will spawn the shell specified by this variable, or ``/bin/sh`` if the
variable does not exist. Spawning a new shell is necessary so that termtosvg can act
as an intermediary between the shell and the pseudo terminal and capture all the data sent
to the terminal.


## EXAMPLES

Record a terminal session and name the animation `animation.svg`:
```
termtosvg animation.svg
```

Record a terminal session and render it using a specific template:
```
termtosvg -t ~/templates/my_template.svg
```

Record a terminal session with a specific screen geometry:
```
termtosvg -g 80x24 animation.svg
```

Record a terminal session in asciicast v2 format:
```
termtosvg record recording.cast
```

Render an SVG animation from a recording in asciicast format
```
termtosvg render recording.cast animation.svg
```

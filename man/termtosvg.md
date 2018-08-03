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
The default behavior of termtosvg is to render an SVG animation 

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


```SVG
<?xml version="1.0" encoding="utf-8"?>
<svg id="terminal" baseProfile="full" viewBox="0 0 656 325" width="656" version="1.1"
     xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
    <defs>
        <termtosvg:template_settings xmlns:termtosvg="https://github.com/nbedos/termtosvg">
            <termtosvg:screen_geometry columns="82" rows="19"/>
        </termtosvg:template_settings>
        <style type="text/css" id="generated">
            <!-- [snip!] -->
        </style>
    </defs>
    <svg id="screen" width="656" viewBox="0 0 656 323" preserveAspectRatio="xMidYMin meet">
        <!-- [snip!] -->
    </svg>
</svg>
```

| Template | Color theme | JavaScript | Description |
| --- | --- | --- | --- |
| [**plain**](../termtosvg/data/templates/plain.svg) | gjm8 | No | No decoration |
| [**progress_bar**](../termtosvg/data/templates/progress_bar.svg) | gjm8 | No | Adds a progress bar at the bottom |
| [**carbon**](../termtosvg/data/templates/carbon.svg) | gjm8 | No | Terminal window frame |
| [**carbon_js**](../termtosvg/data/templates/carbon_js.svg) | gjm8 | Yes | Terminal window frame with animation controls (play, pause, seek) |

## ENVIRONMENT
##### SHELL
termtosvg will spawn the shell specified by the SHELL environment variable, or ``/bin/sh`` if the
variable does not exist. Spawning a new shell is necessary so that termtosvg can act
as an intermediary between the shell and the pseudo terminal and capture all the data sent
to the terminal.


## EXAMPLES

Record a terminal session and produce an SVG animation named `animation.svg`:
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

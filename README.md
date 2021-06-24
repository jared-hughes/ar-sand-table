# AR Sand Table

Operating instructions/scripts and parts list. Currently working on making recalibration instructions easier through more python scripts.

## Parts List

- BenQ Box

  - Projector

    - Attached to mount
    - Wrench for projector mount (missing?)
    - Lens cap
    - Power cord
    - HDMI Cord
    - Plastic end caps on HDMI (missing)

  - Kinect

    - USB cord (male orange tip) is attached
    - Y-shaped USB cord with orange tips, also has wall power plug

  - Calibration Lollipop (CD on stick)

- Pipe assembly

  - Two black pipes
  - Blue knob to hold them more tightly

- Table

  - 4 legs
  - Table top
  - Mini-table that connects table top and the legs

- Sand (in buckets)

- Hypnos bag

  - Hypnos laptop
  - Power cord

- Large plastic board (baseplane calibrator, white)
- Mouse (not optional)
- Power strip (depending on needs)

## Hardware Setup

1. Assemble wood parts of table and connect metal pipes (hangman shape)

2. Connect Kinect:

   - Using the attached magnet, stick the kinect above the center of the sand table
   - Should be approximately near the bottom of the top stick
   - PHOTO

3. Connect Projector

   - The two bolts at the back of the mount hook onto the top pipe into the two holes.
   - PHOTO

4. The wires can be pulled through the pipes if desired

## Recalibration instructions

[Original software installation instructions](http://idav.ucdavis.edu/~okreylos/ResDev/SARndbox/LinkSoftwareInstallation.html) ([archived](http://web.archive.org/web/20190922124245/http://idav.ucdavis.edu/~okreylos/ResDev/SARndbox/LinkSoftwareInstallation.html)), but it should already be installed on the laptop.

1. Enter the main directory

   - $ `cd ~/SARndbox-2.6`
   - Tip: copy-paste in terminal: ctrl-SHIFT-v or ctrl-SHIFT-c
   - Tip: press TAB for autocomplete

2. Line up kinect

   - `$ RawKinectViewer -compress 0`
   - (step 7 in the software installation instructions above)

3. Measure base plane

   - `$ RawKinectViewer -compress 0`
   - A mouse is necessary to perform the following actions because the touchpad is disabled while typing
   - Requires the flat plastic board to be set on top of the table
   - Bind the key <kbd>1</kbd> to extract planes:
     - Hold down the <kbd>1</kbd> key, then click on "Extract Planes" using the mouse
   - Right click > Average Frames
   - Press and hold <kbd>1</kbd> to make a rectangle on the left side
     - This should span as much of the flat green area as possible
     - After this, something like `Camera-space plane equation: x * (0.00765363, 0.0219367, 0.99973) = -89.77` should be logged.
   - Copy the Camera-space plane equation and Ctrl+C to close the viewer
   - `$ ./apply-camera-space `then paste the camera space equation
   - (step 8 in the software installation instructions above)

4. Measure Box corners

   - `$ RawKinectViewer -compress 0 `
   - Bind <kbd>1</kbd> = Measure 3D Positions

     - Hold down the <kbd>1</kbd> key, then click on "Measure 3D positions"

   - Move mouse to lower-left of box in depth view, then press <kbd>1</kbd>

     Move mouse to lower-right of box in depth view, then press <kbd>1</kbd>

     Move mouse to upper-left of box in depth view, then press <kbd>1</kbd>

     Move mouse to upper-right of box in depth view, then press <kbd>1</kbd>

   - Copy the four lines of vectors and Ctrl+C to close the viewer
   - `$ ./apply-box-corners`
   - Paste in the four lines of vectors
   - (step 9 in the software installation instructions above)

5. Align the Projector

   - `$ XBackground`
   - Windows Key + P to switch to "join displays"
   - Drag the new window into the projector screen
   - Press F11 to maximize
   - Adjust projector to include all of the table bed, possibly with some overprojection
   - (step 10 in the software installation instructions above)

6. Match the Projector and Camera

   - `$ ./bin/CalibrateProjector -s 1600 1200`
   - Drag into the projector window
   - Press F11
   - Press 2
   - Press 2 again to set background distance and wait until red screen leaves
   - Press 1 after lining up the lollipop to capture a tie point
   - Make sure the terminal has no error at the end ... otherwise press ctrl+c in the terminal to restart the calibration process
   - (step 11 in the software installation instructions above)

## Running instructions

## Other scripts for convenience

- Run using `./sandbox` in terminal
- `./lava` and `./water` to quick swap liquid shaders (activate by spreading hand with wide gap between fingers)

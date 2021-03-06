
Playing with Gradients
======================

I wondered if I could programmatically generate pleasing top navigation colors
for the Tsugi Bootswatch cerulean theme.  There are four colors, thres are used for
a very subtle top to bottom gradient and the fourth color id the highlight color
and a 1 pixel border at the bottom.

I was inspired by this blog post:

https://medium.com/the-mvp/finally-a-definitive-way-to-make-gradients-beautiful-6b27af88f5f

What I loved was the notion of "perceived brightness" - I was also fascinated with the HSL color space.
So I decided to write a program to wander through HSL space and look for pretty ranges.

The basic algorithm loops through HSL (Hue, Saturation, and Lightness) color wheel one degree
at a time.  For each hue it works through every combination of Saturation and Lightness 
(1-100 by 10) in each dimension and looks for a span of colors that is not to bright and not too dim
and not a pure primary color.

Once I found these dark muted color ranges, I grabbed four colors from dark to light within a range
so that all four colors met my not too light and not too dark and somewhat colorful.   Then I converted
the colrs to RGB ane ended up with a bunch of numbers like:

    #4c2119 #48241d #46261f #98331f

These look kind of random but within the HSL color space they are a straight line and very close
together.  The last number is a bit further along that hue line as it is supposed to be contrasting.

I found 53 gradients that my code "liked".

![Gradients](https://github.com/csev/gradients/raw/master/pretty.png)

To run this check it out and open index.htm in a browser.

To Activate this, in your Tsugi, edit the `config.php` and add these lines:

    $CFG->bootswatch = 'cerulean';
    $CFG->bootswatch_color = 32;

If you want to test a different color scheme on each refresh, use this config option:

    $CFG->bootswatch_color = rand(0,52);
    
As you navigate the site it will switch colors.  Of if you are really crazy,
the code does a modulo operation before selecting the them so you could even
do something like:

    $CFG->bootswatch_color = crc32($CFG->context_title);

And this means that Tsugi will choose amongst its themes bases on a checksum hash of 
the title of your Koseu course.


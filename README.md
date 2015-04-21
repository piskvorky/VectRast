What is VectRast?
-----------------

A tool for creating levels out of bitmaps (or vice versa) for the [Elastomania game](http://www.moposite.com).

Also, as a by-product, you can convert levels into levels (with transformations such as rotation or scaling) and bitmaps into bitmaps.

Why should I want that?
-----------------------

Mainly for Elma battles.. no more "omg i cant use the editor u make lev!!" whining :P
Just use Gimp/photoshop to draw the level as bitmap, then use VectRast to convert the bitmap into the vector format used by Elastomania.

The opposite direction (level to bitmap) can be useful for inspecting some large levels, I suppose...

What can it do?
---------------

VectRast converts a bitmap into the polygonal level format used internally by Elastomania.

It also allows you to transform the resulting polygons, i.e. rotate them, scale along either axis and displace them.

Conversely, it takes a level and creates a bitmap out of it.

Another thing, suggested by sk0nce, is including a bitmap into an existing level.

What can it NOT do?
--------------------

It does not place any apples.
Also you still have to open the file in the editor and move start/flowers to their desired positions -- the program always places them around the center.

How about the vectorization algorithm, how robust is it?
--------------------------------------------------------

Since polygons in Elastomania are not allowed to touch or intersect, I disallowed this also.

Among these ambiguous situations that allow incorrect interpretations are one pixel wide lines; do not use one pixel wide lines.
Still, the program detects these faulty situations and will yell at you the location in terms of pixel coordinates.

TL;DR **use line width of at least two when drawing shapes**.

How do I use it?
-----------------

The tool operates through command line arguments (YEAH!)

Recognized parameters are:

* **IO parameters**
  * `-loadbmp filename` : specify bitmap to load from; white color means empty space, anything else is ground
  * `-loadlev filename` : specify level to load from
  * `-loadlevbmp level bitmap` : specify level to load from and bitmap to include in the level; transformations are only done over the bitmap<br>
  * `-savelev filename` : specify level file to save to
  * `-savebmp filename` : specify bitmap file to save to
* **transformation parameters**
  * `-translate x y` : displace all polygons
  * `-rotate x` : rotate around the center (in degrees)
  * `-scale x y` : scale x and y axis resp; the values can be interpreted as 'how many pixels on the screen is going to be one pixel in the bitmap'. Negative quantity results in mirroring around the respective axis.
* **other parameters**
  * `-warnings true/false` : print warnings (default `false`)
  * `-flowers number` : number of flowers in the created level (effective only with `-loadbmp`); default is `1`

You can use the transformations one on top of another; for example you can rotate by 30 degrees, then displace 10 pixels to the left, then rotate again and then stretch x axis to 2 and mirror y axis to -1.

Run the example batches from `examples folder`. Look at the files created. Tweak the parameters in the batches.

What do I need to run it?
-------------------------

You need the [Microsoft .NET framework](http://msdn.microsoft.com/netframework/downloads/howtoget.asp) installed.

So now I can convert any picture whatsoever into a level?
--------------------------------------------------------

Almost, but... Firstly, only white color is considered empty space (not red, not gray, not yellow).
Secondly, you must use a precise (loss-less) format such as bmp or png.
If you use a lossy format like jpeg, the most likely result is the illegal pixel configuration mentioned above.

Also, VectRast creates *vectors* -- if there are no distinct edges and shapes in the bitmap,
there is not much to vectorize in the first place and the resulting level will look like jaggy shit.

The bitmap looks so nice and smooth on my screen, why not so in the level?
---------------------------------------------------------------------------

Ok, I see this is one common pitfall: people draw a level in Paint so that it fills
one screen (700x700 or whatever) and then expect it to be precise when magnified
to like 4000x3000 (six screens in elma, not a big level). Think of the bitmap
you are drawing as **the actual level when played**, not as the minimap!

Check the example directory for a sample bitmap. Use meaningful scales for `bmp2lev`, like 2 or 3, not 40... unless you know what you are doing.

I have a question not answered here, what now?
------------------------------------------------

[Ask me](mailto:xrehurek@fi.muni.cz?subject=vectrast) and I'll add it here. Also be sure you're using the latest version of VectRast.

**NOTE: I created this tool many years ago (2003). Elma the game is still around and kicking,
but don't send me any emails about VectRast, please** :-)

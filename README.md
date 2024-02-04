# Path2PolyNet
![cubic_nets](https://github.com/egoughnour/path2polynet/assets/457471/da531e7c-affe-4c33-8119-f4e6573b16bf)
Starting from a directed path we ought to be able to make boxes or polyhedral nets out of it.  A plotter will facilitate rapid testing if we generate the corresponding g-code. 

### Curve to Path and Derived Boxes
Take a closed, simple planar curve (a [Jordan curve](https://en.wikipedia.org/wiki/Curve#Jordan)) and quantize it by curvature, so that we end up with long sections (line segments) in flat places and short sections in curvy places.
If we have a path of traversal (as in the case of a spline interplolation) then this carries over to the quantized curve, meaning the quantized curve has an outward normal available for free.
Suppose the directed path is defined in terms of the endpoints, c_0 and c_1, given in terms of values in the complex plane.  Then if we traverse the curve in the counterclockwise (mathematically positive) direction, we are making the equivalent of infinitesimal left turns everywhere.
Then turning left (multiplying by i) from our segment, c_1 - c_0, we point inward.  On the other hand multiplying by -i gives us the outward normal.

From here we can see how traversing rectangular loops with one side in on the initial path will provide a set of sides for a (generally non-rectangular) prism.  The only remaining trick is to duplicate the base of the shape and connect the copy (the top) via one of the sides.
Once we have both a top and a bottom of the prism, it only remains to permute the attachment points of each side (in the sense of attaching the side to either the top or bottom face).
For a convex curve this is not needed, but in the other cases we have to fiddle with the location of the sides until they no longer overlap in the plane.

At this point we can plot the curve and its net.  Generate the g-code, then plot.

If we are satisfied with this net we need tabs, latches, or some means of connecting the faces once we have liberated it from the plane.
These can be added in exactly the same manner as the sides were added to the base, that is, by extending the side face in the direction of the outward normal.

Once these are added, we still have a slight problem.  With an idealized (or practically, merely very thin) surface--say a paper model, there is no intersection between adjacent faces when we fold them into place.
With a solid net, we need to chamfer the edges of every inward face--this just keeps things foldable.

### 3D Print

Relative to our plot we need infill within the base (and first layer of each face) and simply to reduce the next layer of each face by the layer height in the inward normal direction.
That's it. We simply stop layering once we reach the desired thickness.
So this is all our final g-code needs to accomplish in order to create a box that approximates the initial Jordan curve.

## Why?

Frankly this method seems much easier than modeling in most CAD software.

## Installation
Not yet available via pypi, but you can always clone the source and work from there.

# Prusa Mini Skew

A compiled list of fixes for skew issues with the Prusa Mini. Storing this in github so I can continue to refine this as I make new discoveries. If you would like to contribute, please submit a PR.

I have decided to remove any reference to the axis in the naming of skew. Ultimately terms like XZ skew and XY skew are confusing, and it's simpler to explain skew in terms of the problem it creates than in these terms.

* X axis - the horizontal arm where the print nozzle travels (left and right).
* Z axis - the vertical arm, that holds the horizontal arm (up and down).
* Y axis - the rods where the print bed travels along (forward and backward).

## Skew Fixes

### Squareness Skew

![xy-skew-1](https://github.com/s-taylor/prusa-mini-skew/blob/main/assets/printer-skew-xy-1.jpg?raw=true)

#### What is it?

This occurs when the horizontal arm of the printer is not perpendicular (at at 90 degree angle) to the Y axis below (which the print bed travels along). It is either pulling forward towards the front of the printer, or backwards towards the back of the printer.

#### Issue

This will affect if a print is square, specifically how a line of filament is printed from right to left (or left to right) on the bed.
A line of filament printed from the front to back (or back to front) will be unaffected as this is reliant on the Y-axis.

#### What do you need?

* Calipers for most accuracy OR a set square

#### Measuring

You can test this by printing [something square](https://www.thingiverse.com/thing:4140075) and then either using a set square to check if all 4 corners are square, looking for any visible gaps. OR if you have calipers, you can measure corner to corner inside the square (both diagonals) and compare the values. If it is perfectly square, the values will be the same.

#### Fixes

* Refer [Prusa Mini Shims](https://github.com/pgooch/Prusa-Mini-Shims), these are the [screws](https://help.prusa3d.com/en/guide/building-your-mini_6384#6952) you'll need to unscrew to install the shim.
* Refer [Prusa Mini + _ Squaring X Y Axis Skew](https://www.youtube.com/watch?v=Zee6GDZ9ZEo&list=PLeLEMdcW0IhKBHVQ4vMCfjI5uVHgufpgQ&index=28).

- - -

### Bed Level Skew Left/Right

#### What is it?

This occurs when the horizontal arm of the printer is not parallel on the X axis with the print bed below. It is either tilting downward towards the print bed, or upwards towards the ceiling. As a result, your printers bed will be sloping from left to right or right to left.

#### Issue

This affects the first layer calibration, the left hand side of the x-axis will be either too close or too far away from the print bed causing a slant. The printer can only compensate for an uneven bed so much, so depending on how severe the slant is, it may or may not affect your prints.

#### What do you need?

If you follow the Prusa solution below, they suggest simply moving the print head from one side to the other and visually checking the height from the bed. In all honestly, I think that is a waste of time as it will never be anything close to accurate. I highly recommend setting up a Raspberry Pi with Octoprint and the Bed Visualiser plugin.

#### Measuring

As above, I suggest running the Bed Visualiser plugin on Octoprint. This makes it very clear to see if you have an issue or not. This is a [good example](https://forum.prusaprinters.org/wp-content/uploads/2021/02/5DB11A81-76E6-4A66-B461-33506FFDEC8C.jpeg) of what to look for. Once you have run the visualiser you will know whether the arm needs to move up or down. Ensure you turn on "Descending y axis" if you are looking at the "Current Mesh Data", this orientates the data as it would be if you are looking at your printer from the front.

Do not worry about any dips or raised areas you see in the corners when running the visualiser, there is a separate fix required for this. The aim here is just to get it as level as possible from left to right.

#### Fixes

There are two potential causes for this...

1. The Z axis arm is not perpendicular to the bed
2. The X axis arm is not perpendicular to the Z axis arm (and therefore not parallel with the bed)
3. Both

**Solution 1 - Z axis arm not perpendicular to the bed**

![xz-skew-2](https://github.com/s-taylor/prusa-mini-skew/blob/main/assets/printer-skew-xz-2.jpg?raw=true)

You can loosen the three screws holding the Z axis arm and adjust it to ensure it is at a 90 degree angle from the print bed. I did this by placing a small set square on my print bed, adjusting the position of the arm, then retightening the screws in the order specified. Unfortunately if you have the print bed positioned such that you can place a set square on it and touch the arm, you won't be able to reach the main print arm, you'll just have to keep checking it until you get it right.

Another option would be a digital level e.g. Klein Tools 935DAG Digital Electronic Level. You can hold the level against the Y axis while you are tightening the screws and try and align it at 90 degrees. One thing to consider though, is unless your print bed is perfectly level and it may not be, you may want to factor in any discrepancy into how you align the Z axis.

Refer to Prusa's guide to see which screws need to be loosened [source](https://help.prusa3d.com/en/guide/building-your-mini_177717#178546).

There are also some mods that may help here, I have not tried these

* [Prusa Mini XZ Support](https://www.prusaprinters.org/prints/40128-prusa-mini-xz-support)
* [Prusa MINI Z-Axis Support Brace](https://www.prusaprinters.org/prints/32054-prusa-mini-z-axis-support-brace)

**Solution 2 - X axis arm is not perpendicular to the Z axis arm**

![xz-skew-1](https://github.com/s-taylor/prusa-mini-skew/blob/main/assets/printer-skew-xz-1.jpg?raw=true)

Follow the steps as provided by Prusa.

* Highly recommend using Octoprint bed visualizer before and after to visualise your changes, by eye this will not be accurate
* If you loosen the belt tension screws, you should push the orange piece that holds the screws inward towards the z-axis arm, while holding the other end with your other hand. This is not mentioned in the guide, but is mentioned in a [video](https://youtu.be/Z5N9oDwrUu0) I watched and you will feel the orange piece move inward when you do this.

[source](https://help.prusa3d.com/en/article/xz-axis-skew-correction-mini_158518)

- - -

### Bed Level Skew Forward/Backward

This is the skew that occurs as your print bed moves along the Y axis, the print bed's height from the nozzle is not consitent. This will occur if your print bed itself is not perfectly level from front to back. This is best seen with octoprint bed visualizer.

Unfortunately there is no simple fix for this.

If both front or both back corners are dipped, it might be possible that the Z axis arm is tilted slightly forward or slightly backward (that's pure speculation though I'm unsure if this can happen).

If one corner is dipped and one is raised (on the front or the back) there is no quick fix. In my case my front right and my back left corner were both dipped, which is not easily fixable. 

Someone recommended to me to perhaps try the [masking tape mod](https://forum.prusaprinters.org/forum/user-mods-octoprint-enclosures-nozzles/prusa-mini-silicone-bed-leveling-mod/paged/9/#post-336934). This was actually an incredibly quick and easy way to level the print bed at a very low cost. Using octoprint each time I made an adjustment I focused on getting the front left and back left corners the same height, and likewise with the front right and rear right. I then leveled the bed almost completely using the [XZ skew adjustments by Prusa](https://help.prusa3d.com/en/article/xz-axis-skew-correction-mini_158518). Unfortunately I quickly realised why this method is not a good idea, in one area where I had three layers of tape the plastic would not adhere to the steel sheet because the masking tape was insulating the heat. Because of this, I cannot recommend this mod.

So what is the solution? It's [this](https://github.com/bbbenji/PMSBLM) and while it is the perfect solution it's also pretty involved and requires a lot of care to execute.

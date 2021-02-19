# Prusa Mini Skew

A compiled list of fixes for skew issues with the Prusa Mini. Storing this in github so I can continue to refine this as I make new discoveries. If you would like to contribute, please submit a PR. If this was helpful to you and you want to say thanks, please star the repo.

I have decided to remove any reference to the axis in the naming of skew. Ultimately terms like XZ skew and XY skew are confusing, and it's simpler to explain skew in terms of the problem it creates than in these terms.

* X axis - the horizontal arm where the print nozzle travels (left and right).
* Z axis - the vertical arm, that holds the horizontal arm (up and down).
* Y axis - the rods where the print bed travels along (forward and backward).

The [original thread](https://forum.prusaprinters.org/forum/hardware-firmware-and-software-help/oh-no-were-skewed-prusa-mini-edition/) on the Prusa forums.

## Skew Fixes

### Squareness Skew

![squareness-skew](https://github.com/s-taylor/prusa-mini-skew/blob/main/assets/squareness-skew.jpg?raw=true)

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
* Refer [goskew](https://github.com/Kranex/goskew)

- - -

### Bed Level Skew Left/Right

#### What is it?

This occurs when the horizontal arm of the printer is not parallel on the X axis with the print bed below. It is either tilting downward towards the print bed, or upwards towards the ceiling. As a result, your printers bed will be sloping from left to right or right to left.

#### Issue

This affects the first layer calibration, the left hand side of the x-axis will be either too close or too far away from the print bed causing a slant. The printer can only compensate for an uneven bed so much, so depending on how severe the slant is, it may or may not affect your prints.

#### What do you need?

If you follow the Prusa solution below, they suggest simply moving the print head from one side to the other and visually checking the height from the bed. In all honestly, I think that is a waste of time as it will never be anything close to accurate. I highly recommend setting up a Raspberry Pi with Octoprint and the Bed Visualiser plugin.

I also highly recommend that you should have a mechanism to measure belt tension (for Solution 2 below). Without this, you will be completely in the dark as to how tight your x-axis belt is, and if you are messing with those screws, you would want to know. This is what I [recommend](https://www.prusaprinters.org/prints/46639-tension-meter-for-the-gt2-belts-of-i3-mk3s-or-prus), it's very good. I verified its accuracy on my friends MK3S, which can give you a belt tension reading which I then compared to the meter.

#### Measuring

As above, I suggest running the Bed Visualiser plugin on Octoprint. This makes it very clear to see if you have an issue or not. This is a [good example](https://forum.prusaprinters.org/wp-content/uploads/2021/02/5DB11A81-76E6-4A66-B461-33506FFDEC8C.jpeg) of what to look for, in this case you'd need to lower the arm, by tightening the top screw. Once you have run the visualiser you will know whether the arm needs to move up or down. Ensure you turn on "Descending y axis" if you are looking at the "Current Mesh Data", this orientates the data as it would be if you are looking at your printer from the front.

Do not worry about any dips or raised areas you see in the corners when running the visualiser, there is a separate fix required for this. The aim here is just to get it as level as possible from left to right.

#### Fixes

There are two potential causes for this...

1. The Z axis arm is not perpendicular to the bed
2. The X axis arm is not perpendicular to the Z axis arm (and therefore not parallel with the bed)
3. Both

**Solution 1 - Z axis arm not perpendicular to the bed**

![skew-left-right-1](https://github.com/s-taylor/prusa-mini-skew/blob/main/assets/skew-left-right-1.jpg?raw=true)

You can loosen the three screws holding the Z axis arm and adjust it to ensure it is at a 90 degree angle from the print bed. I did this by placing a small set square on my print bed, adjusting the position of the arm, then retightening the screws in the order specified. Unfortunately if you have the print bed positioned such that you can place a set square on it and touch the arm, you won't be able to reach the main print arm, you'll just have to keep checking it until you get it right.

Another option would be a digital level e.g. Klein Tools 935DAG Digital Electronic Level. You can hold the level against the Y axis while you are tightening the screws and try and align it at 90 degrees. One thing to consider though, is unless your print bed is perfectly level and it may not be, you may want to factor in any discrepancy into how you align the Z axis.

Refer to Prusa's guide to see which screws need to be loosened [source](https://help.prusa3d.com/en/guide/building-your-mini_177717#178546).

There are also some mods that may help here, I have not tried these

* [Prusa Mini XZ Support](https://www.prusaprinters.org/prints/40128-prusa-mini-xz-support)
* [Prusa MINI Z-Axis Support Brace](https://www.prusaprinters.org/prints/32054-prusa-mini-z-axis-support-brace)

**Solution 2 - X axis arm is not perpendicular to the Z axis arm**

![skew-left-right-2](https://github.com/s-taylor/prusa-mini-skew/blob/main/assets/skew-left-right-2.jpg?raw=true)

Follow [the steps as provided by Prusa](https://help.prusa3d.com/en/article/xz-axis-skew-correction-mini_158518).

Remember, if you tighten the lower screw, this moves the arm upwards, towards the ceiling.
If you tighten the upper screw, this moves the arm downwards, towards the bed.
This is counterintuitive, so it's worth mentioning.

Once you have made the adjustments, check that both of the horizontal bars are straight and not twisted. Look at your printer from the top and check the two bars are perfectly aligned. If you need to adjust turn the orange piece with the screws a little to correct. If they are not aligned your print nozzle will turn slightly as it moves along the x-axis.

If you loosen the belt tension screws, you should push the orange piece that holds the screws inward towards the z-axis arm, while holding the other end with your other hand. This is not mentioned in the Prusa's, but is mentioned in a [video](https://youtu.be/Z5N9oDwrUu0) I watched and you will feel the orange piece move inward when you do this. Otherwise loosening the screws may not have an effect.

Once you have made an adjustment, you should check the belt tension! See "What do you need?" above.

- - -

### Bed Level Skew Corners

![bed-level-skew-corners](https://github.com/s-taylor/prusa-mini-skew/blob/main/assets/bed-level-skew-corners.png?raw=true)

#### What is it?

This is the skew that occurs when your print bed is not level. With the "Bed Level Skew" fixes above, you should be able to achieve a level bed from left to right in the very center of the print bed (or at any single point on the Y-axis). However the print bed itself may not be consistently level from front to back and as it moves backward and forward on the Y-axis, the level changes.

In my particular case, my print bed actually droops in the front right and back left corners, and is elevated in the back right corner.  As the bed moves forward or backwards the level will change since the leveling is not consistent.

#### Issue

Depending on the severity this may or may not cause you issues. The Prusa Mini (and MK3) both have auto bed leveling, which detects any variance in your print bed, and accomodates this by raising or lowering the nozzle height accordingly in those areas. However if the variance is too high, your printer may not be able to compensate for these differences. The other potential issue, is although the nozzle compensates for an uneven bed, the bottom surface of your print will follow the contours of your bed.

#### Measuring

Your only option here is Octoprint with the Bed Visualiser plugin, this makes it very clear how level your bed is.
Before going any further you should decide if this is worth the effort. If your differences are small I honestly don't think you should worry about it.

How small is acceptable? I'm not sure I can answer that. I feel like I read somewhere up to 0.5mm from corner to corner is acceptable, but don't quote me on that.
In my case my front right corner was -0.16mm and my front right corner was +0.38mm, so just over a 0.5mm slope.
I can't say I can definitively attribute any issues I've had to my print bed, but I decided I wanted it as level as possible as that's the kind of perfectionist I am.

#### Fixes

**Solution 1 - Masking Tape Mod**

Someone recommended to me to perhaps try the [masking tape mod](https://forum.prusaprinters.org/forum/user-mods-octoprint-enclosures-nozzles/prusa-mini-silicone-bed-leveling-mod/paged/9/#post-336934). This was actually an incredibly quick and easy way to level the print bed at a very low cost. Using octoprint each time I made an adjustment I focused on getting the front left and back left corners the same height, and likewise with the front right and rear right. I then leveled the bed almost completely using the [XZ skew adjustments by Prusa](https://help.prusa3d.com/en/article/xz-axis-skew-correction-mini_158518). 

One caveat with this fix though, is this "may" affect your print bed temperature as the masking tape will insulate the heatbed from the steel sheet. If you are printing PLA that should not affect your first layer, as you can technically print on a cold bed (I believe), but it may cause warping if your bed is not evenly heated. It's hard to say if this is an issue and probably depends on how much masking tape you use and where you put it. You'll need to experiment for yourself.

**Solution 2 - Silicone Mod**

So what is the ultimate solution? It's [this](https://github.com/bbbenji/PMSBLM) and while it is the perfect solution it's also pretty involved and requires a lot of care to execute.

Normally, any sound or texture that you want to modify is relatively simple. However, this isn't entirely the case for water and lava...

1. The texture you provide, is the still-frame image for use on browsers/computers that can't generate an animation.
2. Fluid blocks animation's appear to use programmatic approach to animate the fluid block.
    * Lava: search for `BABYLON.DynamicTexture("lavaTexture"` in app.js
    * Water: search for `BABYLON.DynamicTexture("waterTexture"` in app.js
   You'll find that it uses a means of locating pixels in the image and changes each one, where in water's case it's with pixel transparencies.
3. Changing the texture file alone won't work because you'll also need to change the colors in the dynamic texture animation in RGB, and each value must be integers from 0 to 255.
    * p = red
    * m = green
    * g = blue
4. The fluid colors when submerged are not so easily made clear, but goes as follows:
    * Lava: search for `fogLava` in app.js
    * Water: search for `fogWater` in app.js
   You'll find an area where it first sets a variable to the fogBlock, and then sets two different color attributes:
    * `diffuseColor`: When submerged and there is no fog, this is the color you'll primarily see
    * `fogColor`: When submerged and there is fog, you'll see a mix of the diffuseColor and this color (unless you set render distance to it's lowest, then it'll primarily be this color)
   IMPORTANT: You need to use decimal values from 0 to 1 when setting the RGB
5. There is one more color that is set with the initialization of the fluid blocks, and they don't appear to have much of an effect at all, but I suspect that they were supposed to be the start of map colors of blocks:
    * Lava: search for `"lava"==(Z=Q[L])&&(q=` in app.js
    * Water: search for `"water"==(Z=Q[L])&&(q=` in app.js
   As you'll find, it's relatively darker and simple colors of the type of block (and it's the same fogColor for the fluid block).
   IMPORTANT: You need to use decimal values from 0 to 1 when setting the RGB

Now that all that is out of the way. I'm not sure what the best way is for editing the fluid animation, but I know that it would definitely need to be remade to accept textures that contain more than one base color (like how water is primarily blue and lava is primarily a warm color).
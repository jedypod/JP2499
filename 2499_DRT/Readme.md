# The 2499 DRT Process: A Breakdown of the most important stuff

The DRT process consists of mainly four key steps, some focused on technical aspects and others on aesthetics. 
Let's explore them in the order they are applied:

**1. Density/luminance Adjustment:** 
This step acts like exposure control but specifically targets saturated areas. 
It multiplies each red, green, and blue (RGB) value by a specific amount. While primarily an aesthetic choice, 
it also helps prevent overly bright areas produced by the IDT matrix. This step is extremely smooth to prevent rings around 
achromatic areas, or blurred areas, this is normally something that happens with other similar adjustments.

**2. Gamut Mapping/Guard Rail:** 
This step ensures colors stay within the open domain representable range. 
It's a non-linear process, as chromaticity linear mapping often produces undesirable results. 
This approach achieves a similar effect to a per-channel sigmoid function, smoothly compressing negative values and creating continuous gradients. 
Additionally, it includes an "energy fix" to recover detail loss that can occur during other gamut mapping options.

**3. Aesthetic Matrices:** 
These are two matrices that significantly impact the final look. 
One affects the entire image, while the other targets only the brightness values. They are crucial for achieving the desired visual style 
and should be adjustable by the user, as a single setting won't work for all scenarios. While consistency within a project is recommended, 
different projects may require unique parameters for these matrices.

**4. Attenuation refinement:** 
This final step ensures there are no abrupt changes in saturation at high values.
It builds upon the adjustments made in the previous step, it's very subtle but important. For example, 
it helps with sensor that clip early at high exposures.

The rest of the operations are a sigmoid, and a final purity matrix, this matrix will re-introduce some negative values aswell as above 1, an extra gamut mapping helps to prevent emissive looking values for objects that shouldn't be emissive and clipping at the display level

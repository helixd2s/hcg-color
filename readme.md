# HCG (color model)
> Color model [HCG](https://github.com/acterhd/hcg-color/blob/master/convert/hcg.js) is an alternative to [HSV and HSL](https://en.wikipedia.org/wiki/HSL_and_HSV), derived by Munsell color system.

## Revision for 2020 

I found new use cases for HCG in 2020 years...


### Inverse your RGB color...

Normal RGB equal normal HCG conversion i.e. `H % 360deg, C (between 0.0 and 1.0), G (between 0.0 and 1.0)`.
But invert RGB equal to `(H + 180deg) % 360deg, C, 1.0 - G`. 
Why? Because minimal value of RGB inverts into maximal, maximal value of RGB inverts into minimal, but Chroma doesn't changing... 
About 180deg rotate known from internet facts (for example, here https://stackoverflow.com/questions/1165107/how-do-i-invert-a-colour).


### Dark and light theme

When I watch that or such video (https://www.youtube.com/watch?v=qimopjP6YoM), I understand that HCG color space can be used for dark and light themes themes. 

```scss
.dark-theme {
  filter: invert(100%) hue-rotate(180deg);
  color: rgb(0, 0, 127);
  //color: rgb(127, 127, 255);
}

.light-theme {
  color: rgb(0, 0, 127);
}
```

Can be represented as... 

```scss
.light-theme {
  $mod: 0; /* dark font */
  color: hcg(240, 50, $mod);
}

.dark-theme {
  $mod: 100; /* light font */
  color: hcg(240, 50, $mod);
}
```

## HCG (Article)

### Description
HCG - is HSV/HSL based color model. This color model use 3 channel: H, C, and G. Changing mixed gray color, instead of changing the brightness (luminance). This differs from the other color models, such as HSV and HSL.

### Behavior
Color model HCG has its own behavior. When you change the second channel (chroma), hue is mixed with a selected shade of gray (third channel). In this regard, there are some features in the conversion of RGB. If the C channel is set to 1, the G channel becomes undefined. If channel C is set to 0, the hue channel H is undefined. In this connection, RGB value must be chosen so that it was not a fully chromatic, nor completely achromatic.

### Visualization
<img src="images/diagram.png" alt="#" height="200">

Figure 1. HCG diagram and visual shader

Color model HCG has shades of gray in the middle, while the hue shades are not shaded at the edges of the cylinder (like HSV). This means that the HCG relies still on the hue. This is useful when you want to change the mixed shade of gray, without changing the value saturation.

### Simple conversion between HCG and RGB

The whole algorithm for obtaining RGB color that is similar to the mixed hue (pure RGB) with a shade of gray, as the blending coefficient used chroma. The expression `G * (1 - C)` is the minimum value of RGB, and the value of channel C (chroma) is the delta of the minimum and maximum values of RGB. For these and crosstalk can find the inverse of H, C and G of RGB.

### Conclusion
This color model is fairly easy to learn, easy to implement and has a variety of applications. For example a color picker, or editing graphics. It may also help in the virtual vision.

### Reference
-	HSL and HSV (https://en.wikipedia.org/wiki/HSL_and_HSV)
-	Munsell color model (https://en.wikipedia.org/wiki/Munsell_color_system)
-	Github repository (https://github.com/acterhd/hcg-color)


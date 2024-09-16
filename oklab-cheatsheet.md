# Oklab Color Space
A uniform perceptual color space for device independent color. `oklch()` is easier to udnerstand for most devs. It is based on data collectd about how the human eye detects light, hence perceptual color space.




```css
oklch(from var(--aColor) l c h / alpha);
oklch(from oklch(l c h / alpha) l c h / alpha);
oklch(from red l c h);
```


```css
.button {
  background: var(--button-color);
}
.button:hover {
  /* One :hover for normal, secondary, and error states */
  background: oklch(from var(--button-color) calc(l + 0.1) c h);
}
```

# Tools

* [OKLCH Color Picker & Converter](https://oklch.com/) at oklch.com by EvilMartians. Defaults to RGB as a converter. [https://lch.oklch.com/](https://lch.oklch.com/) for one that defaults to LCH but is the same otherwise.
* [Huetone](https://huetone.ardov.me/) has color pallets and show contrast data and recomendations for colours. Allows you to download CSS of the pallet.
* [OKlch palette generator](https://oklch-palette.vercel.app/) is a fork of the above OILCH Color Picker that creates a lightness gradient and will push in in to Huetone.
* [The good colors](https://thegoodcolors.com/) allows you to paste in a comma seperatd list of colours in any CSS format and shows them all in `oklch()`. Will normalize the lightness and chroma to make them more consistent.

# Further Reader

* [OKLCH in CSS: why we moved from RGB and HSL](https://evilmartians.com/chronicles/oklch-in-css-why-quit-rgb-hsl) from Evil Martians. An excellent primer on what oklch() is and it's benefits for developers. "Extra: OKLCH/Oklab in gradients" shows examples of how gradients look worse in sRGB, and even Oklab, when compared to OKLCH. It also talks about some JavaScript libraries.
* [It's Time to Learn oklch Color](https://keithjgrant.com/posts/2023/04/its-time-to-learn-oklch-color/) by Keith J Grant is a less serious introduction talking about colours, rather than the developer experience. I like that he specified some key color points:
  * Red: 30
  * Orange: 60
  * Yellow: 90
  * Green: 140
  * Cyan/teal: 195
  * Blue: 260
  * Magenta: 330

* [An interactive review of Oklab](https://raphlinus.github.io/color/2021/01/18/oklab-critique.html) has a neat demonstration of gradients in different color spaces. The Blue/Yellow one is especially interesting. Doesn't use `Oklch()`.

## Technical Readeing

* [oklch()](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/oklch) on MDN Web Docs (Mozilla Developer Network)
* [A perceptual color space for image processing](https://bottosson.github.io/posts/oklab/) by Björn Ottosson. The post that started it all.
* [Oklab color space](https://en.wikipedia.org/wiki/Oklab_color_space) on Wikipedia






# Other CSS stuff

```
--button-color
--accent
--dimmed
--error
```
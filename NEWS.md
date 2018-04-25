# ggplotify 0.0.2

+ add NEWS.md, README and example in man <2018-04-24, Tue>

# ggplotify 0.0.1

+ `as.grob` by combining `ggimage::toGrob` and `base2grob` package (will be
  deprecated)
  - `as.grob` can convert base plot or grid plot (e.g. vcd, UpSetR packages) to
    `grob` object
+ `as.ggplot` supports all `as.grob`-supported plots.


# History

## embed base to grid plot (2015, ChIPseeker)

I figured out a way to embed base plot (`vennpie`) to grid plot (`upset`) when
developing `upsetplot` function in `ChIPseeker` package for visualizing overlap
of ChIPseq data in
2015, <http://guangchuangyu.github.io/2015/07/upsetplot-in-chipseeker/>.

## embed ggplot (2015, ggtree and ggimage)

I developed a `subview` function in `ggtree` package in 2015, for embeding
subplots,
<https://github.com/GuangchuangYu/ggtree/commit/2ab2876d5e92454869c3307ea6f3c8e2656630ef>.

This function was re-implemented as `geom_subview` and packed in the `ggimage`
package.

## embed plots (base, lattic, ggplot or image) to ggplot (2017, ggimage and hexSticker)

In the early of 2017, I started to develop R script to produce `ggtree` sticker.
[@lgatto](https://github.com/lgatto) first came out with an idea of makeing an R package for producing hex
sticker by packing my script into a function, <https://github.com/Bioconductor/BiocStickers/issues/12>. I have
several ideas to improve the package, including producing print-ready figure,
employing modular design and supporting grammar of graphics, as well as supporting
subplot generated by base and lattice. I started to develop the
`hexSticker` package, <https://github.com/GuangchuangYu/hexSticker/issues/2>,
with base plot, lattice, ggplot2 and image file supported as subplot, which was
actually implemented in `ggimage` (`toGrob` function, image file are supported
by `geom_image`).


## convert base to grob (2018, base2grob)

I wrote a blog
post, <http://guangchuangyu.github.io/cn/2018/03/five-questions-of-meme/>, to
ask questions based on the `meme` package to help users understand `ggplot2`.

After I wrote the sentence:

> if you know how `ggsave` works, you can even extend it to support base plot

I started to extend `ggsave` to support base plot by using formula or
expression, *e.g.* `ggsave(~base_plot)`.

After that, I asked myself, why not extending `cowplot` to support base plot
with the fact that I already have source code to convert base plot to `grob`
object (`ggimage:::toGrob`). Then I developed the `base2grob` package and submit
it to CRAN.

## convert (almost all) plots to ggplot (2018, ggplotify)

I wrote a blog post, http://guangchuangyu.github.io/cn/2018/04/ggvenn/, to
introduce `ggvenn` function (in `yyplot` package, only available on GitHub), and started
to play with the `UpSetR` package. I believe `upset` plot contains too much
empty space and can embed a `venn` plot as I did in 2015 with `vennpie`. I created a
PR, <https://github.com/hms-dbmi/UpSetR/pull/112>, to make it possible to
capture `upset` output and be able to be converted to `grob` object. I thought it would be more
easy if I further convert the object to `ggplot` then I can directly use
`ggimage::geom_subview()` to embed `ggvenn` inside `upset` plot. With this idea,
I started to implement `as.ggplot` function.

Then, I suddenly realized that I should packed `as.ggplot`, `ggimage:::toGrob` and
`base2grob` into a single package. That's why we have `ggplotify`, which
contains `as.grob` to convert plots to `grob` and `as.ggplot` to convert plots
to `ggplot` objects.

# Rendering rmarkdown to HTML

Before rendering the rmarkdown to a markdown file for Jekyll, you can inspect
how it would look as an HTML file. For instance, if your rmarkdown file was
`crux-of-bayes-statistics.Rmd`, you could run:

```bash
make crux-of-bayes-statistics.html
```

This would generate a `crux-of-bayes-statistics.html` file that is 
self-contained (i.e. all generated images are incorporated into the HTML file).

## Depending on images not generated by the rmarkdown

If there are images that the rmarkdown depends on, but is not generated by the 
rmarkdown file, then these files should be placed into 
`../assets/[RMD_FILE_NAME]` folder. And then a symlink should be created from 
this location into `{{ site.url }}/assets/[RMD_FILE_NAME]`. For instance, the
`crux-of-bayes-statistics.Rmd` rmarkdown depends on the 
`../assets/crux-of-bayes-statistics/meghan-trainor-bayes-stats.jpg` image, which
was generated outside of R. So a symlink should be created to this file:

```bash
tmp_img_dir="{{ site.url }}/assets/crux-of-bayes-statistics";
[[ ! -d "${tmp_img_dir}" ]] || mkdir -p "${tmp_img_dir}";
ln -rs \
  ../assets/crux-of-bayes-statistics/meghan-trainor-bayes-stats.jpg \
  "${tmp_img_dir}/meghan-trainor-bayes-stats.jpg";
```

Thus when the rmarkdown is being knitted into an HTML it will be able to find 
this image.

# Rendering rmarkdown to markdown files for Jekyll

```bash
./r_to_jekyll_wrapper.sh --rmd-file why-bayes-statistics.Rmd
```

The images will be temporarily placed into the subfolder:

```
{{ site.url }}/assets/[RMD_FILE_NAME]
```

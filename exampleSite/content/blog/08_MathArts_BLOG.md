---
date: "2021-07-13"
title: MathArt with R
image: "images/blog/08_cover_BLOG.png"
author_info: 
  name: "DannyJRa"
  image: "images/author/derick.jpg"
draft: false
---




Add summary desdcription here
 
<!--more-->





# Creating Art with R


```r
#install.packages(c("devtools", "mapproj", "tidyverse", "ggforce"))
devtools::install_github("marcusvolz/mathart")
devtools::install_github("marcusvolz/ggart")
```


```r
library(mathart)
library(ggart)
library(ggforce)
library(tidyverse)
```



```r
df1 <- harmonograph(A1 = 1, A2 = 1, A3 = 1, A4 = 1,
                    d1 = 0.004, d2 = 0.0065, d3 = 0.008, d4 = 0.019,
                    f1 = 3.001, f2 = 2, f3 = 3, f4 = 2,
                    p1 = 0, p2 = 0, p3 = pi/2, p4 = 3*pi/2) %>% mutate(id = 1)

df2 <- harmonograph(A1 = 1, A2 = 1, A3 = 1, A4 = 1,
                    d1 = 0.0085, d2 = 0, d3 = 0.065, d4 = 0,
                    f1 = 2.01, f2 = 3, f3 = 3, f4 = 2,
                    p1 = 0, p2 = 7*pi/16, p3 = 0, p4 = 0) %>% mutate(id = 2)

df3 <- harmonograph(A1 = 1, A2 = 1, A3 = 1, A4 = 1,
                    d1 = 0.039, d2 = 0.006, d3 = 0, d4 = 0.0045,
                    f1 = 10, f2 = 3, f3 = 1, f4 = 2,
                    p1 = 0, p2 = 0, p3 = pi/2, p4 = 0) %>% mutate(id = 3)

df4 <- harmonograph(A1 = 1, A2 = 1, A3 = 1, A4 = 1,
                    d1 = 0.02, d2 = 0.0315, d3 = 0.02, d4 = 0.02,
                    f1 = 2, f2 = 6, f3 = 1.002, f4 = 3,
                    p1 = pi/16, p2 = 3*pi/2, p3 = 13*pi/16, p4 = pi) %>% mutate(id = 4)

df <- rbind(df1, df2, df3, df4)

p <- ggplot() +
  geom_path(aes(x, y), df, alpha = 0.25, size = 0.5) +
  coord_equal() +
  facet_wrap(~id, nrow = 2) +
  theme_blankcanvas(margin_cm = 0)

ggsave("harmonograph01.png", p, width = 20, height = 20, units = "cm")
```

## And here are the results

### Example 1

![Art 1](/images/blog/harmonograph01.png)

### Example 2

![Art 2](/images/blog/lissajous001.png)

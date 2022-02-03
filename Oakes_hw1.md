Homework1
================
Jacqueline Oakes
2/1/2022

# Problem 2.1

``` r
#create a tibble with mean and sd
normsample <- tibble(
            x = rnorm(1000, mean = 0, sd = 1),
            y = rnorm(1000, mean = 1, sd = 2))
normsample$sum_indicator <- ifelse(normsample$x + normsample$y > 0.5, TRUE, FALSE)

#use mutate to change T/F to Y/N
normsample <-  normsample %>%
   mutate(sum_indicator = as.factor(ifelse(sum_indicator == TRUE, "Yes", "No")))

#relevel so Y is before N 
normsample$sum_indicator <- forcats::fct_relevel(normsample$sum_indicator, "Yes")

#check work
view(normsample)

#create data visualization
normsample %>%
ggplot() +
  geom_point(aes(x = x, 
                 y = y, 
                 color = sum_indicator)) +
  scale_colour_discrete(name = "") +
  labs(x = "Sample1", y = "Sample2",
       title = "Independent Bivariate Normal Random Sample") +
    theme(plot.title = element_text(face = "bold")) +
    theme(panel.background = element_blank()) +
    theme(axis.line = element_line(colour = "black")) +
    theme(plot.title = element_text(hjust = 0.5))
```

<img src="Oakes_hw1_files/figure-gfm/unnamed-chunk-1-1.png" width="90%" height="90%" style="display: block; margin: auto;" />

# Problem 2.2

``` r
penguin.df <- read_rds("./data/penguin.RDS")

str(penguin.df)
#see how many rows are in the dataset
nrow(penguin.df)
#see how many columns are in the dataset
ncol(penguin.df)

mean(penguin.df$bill_length_mm, na.rm = TRUE)
sd(penguin.df$bill_length_mm, na.rm = TRUE)

mean(penguin.df$flipper_length_mm, na.rm = TRUE)
sd(penguin.df$flipper_length_mm, na.rm = TRUE)

ggplot(na.omit(penguin.df)) +
  geom_point(aes(x = bill_length_mm, 
                 y = flipper_length_mm, 
                 color = species)) +
  labs(x = "Bill Length", y = "Flipper Length",
       title = "Penguins of Antarctica") +
    theme(plot.title = element_text(face = "bold")) +
    theme(panel.background = element_blank()) +
    theme(axis.line = element_line(colour = "black")) +
    theme(plot.title = element_text(hjust = 0.5))
```

<img src="Oakes_hw1_files/figure-gfm/unnamed-chunk-2-1.png" width="90%" height="90%" style="display: block; margin: auto;" />

``` r
ggplot(na.omit(penguin.df)) +
  geom_point(aes(x = bill_length_mm, 
                 y = flipper_length_mm, 
                 color = species)) +
  facet_grid(~sex, scales="free") +
  labs(x = "Bill Length", y = "Flipper Length",
       title = "Penguins of Antarctica") +
    theme(plot.title = element_text(face = "bold")) +
    theme(panel.background = element_blank()) +
    theme(axis.line = element_line(colour = "black")) +
    theme(plot.title = element_text(hjust = 0.5))
```

<img src="Oakes_hw1_files/figure-gfm/unnamed-chunk-2-2.png" width="90%" height="90%" style="display: block; margin: auto;" />

-   The Penguin dataset for each observation shows the size measurements
    for adult foraging penguins near Palmer Station Antarctica.
-   The number of rows is 344
-   The number of columns is 8
-   Each variable is a penguin located in Antarctica and the features of
    that specific penguin, such as, bill length and depth, flipper
    length, body mass, and sex.
-   The mean penguin bill length is 43.9219298
-   The standard deviation penguin bill length is 5.4595837
-   The mean penguin flipper length is 200.9152047
-   The standard deviation penguin flipper length is 14.0617137

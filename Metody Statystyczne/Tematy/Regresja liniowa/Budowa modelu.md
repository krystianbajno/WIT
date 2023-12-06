
```
x <- c(36, 64, 49, 21, 28, 47, 58, 19, 32)
y <- c(129, 310, 260,	92,	126, 242,	288, 81, 134)

abline(lm(y~x), col = 2, lwd = 2)
text(40,180, 'y = -30.344 +  5.466*x', col = 2)

model <- lm(y~x)
model$coefficients
model$coefficients[2]

summary(model)
```
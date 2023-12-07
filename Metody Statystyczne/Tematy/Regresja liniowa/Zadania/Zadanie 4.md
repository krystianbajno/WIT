```
library(lmtest)

# Zadanie 4 
# Pośrednik w handlu nieruchomościami jest zainteresowany oszacowaniem wpływu powierzchni budynku i jego odległości od
# centrum miasta na wartość budynku. Poniższa tabela zawiera informacje o dziewięciu losowo wybranych budynkach.

# Wartość budynku (tys. $) 345 320 452 422 328 375 660 466 290 520
# Powierzchnia (m2) 150 180 200 160 175 180 300 170 135 270
# Odległość od centrum (km) 5,6 1,2 2,4 7,2 2,9 2,5 5,5 4,8 1,6 5,0

# a) Wyznacz liniową funkcję regresji opisującą zależność, którą interesuje się ów pośrednik.
# b) Zweryfikuj dopasowanie modelu.
# c) Podaj przewidywaną wartość domu o powierzchni 160 m2, położonego w odległości 3 km od centrum miasta

y <- c(345, 320, 452, 422, 328, 375, 660, 466, 290, 520)
x1 <- c(150, 180, 200, 160, 175, 180, 300, 170, 135, 270)
x2 <- c(5.6, 1.2, 2.4, 7.2, 2.9, 2.5, 5.5, 4.8, 1.6, 5.0)

cor(x1, x2)

# Niska wartość korelacji reszt

model1 = lm(y ~ x1 + x2)

summary(model1)

model2 = lm(y ~ 0 + x1 + x2)

# Y = 20.837608 + 1.693011 * x1 + 18.579923 * x2 + epsilon
coef(model2)

# Dopasowanie modelu
summary(model2)$sigma

100*(summary(model2)$sigma)/mean(y)
# 10 % error rate

# R^2
summary(model2)$r.squared
# 0.9921772

summary(model2)$fstatistic

summary(model2)

# Analiza reszt

# Test Shapiro-Wilka
shapiro.test(model2$residuals)
# p-value > 0.05
# Reszty nie podążają za rozkładem normalnym, to dobrze

# Test Goldfelda-Quandta
# p-value = 0.4059 brak podstaw że wariancja reszt nie jest stała, więc 
# przyjmujemy, że jest stała
gqtest(model2)

# Losowość reszt wizualnie graficzna
plot(model2$residuals)

# Test niezależności reszt
# Durbin-Watson
dwtest(model2)

# DW = 1.5691, co wskazuje na lekką pozytywną autokorelację pomiędzy resztami
# Jednakże, p-value = 0.2977 co wskazuje na nieistotność wyniku
cor(x1, x2)

# 0.2604269 jest słaba korelacja pomiędzy resztami

# Podaj przewidyhwaną wartość domu o powierzchni 160m^2 położonego w odległości 3 km od centrum miasta
predict(model2, list(x1=160, x2=3))

# 342.8

# Przewidywana wartość domu to 342 800 dolarów
```
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

# Niska wartość korelacji zmiennych niezależnych ze sobą

model1 = lm(y ~ x1 + x2)

# Y = 20.837608 + 1.693011 * x1 + 18.579923 * x2 + epsilon
coef(model1)

summary(model1)

# Wyraz wolny jest nieistotny w modelu (p-value > 0.05)
# ---
  
model2 = lm(y ~ 0 + x1 + x2)

# Y = 0 + 1.780676 * x1 + 19.297304 * x2 + epsilon
coef(model2)

# Dopasowanie modelu
summary(model2)$sigma
# 42.63909 <- to dość duża wartość świadcząca o możliwym niedopasowaniu modelu

100*(summary(model2)$sigma)/mean(y)
# 10 % error rate

# R^2
summary(model2)$r.squared
# 0.9921772 - dobre dopasowanie

summary(model2)$fstatistic
# 507.3268 - dobre dopasowanie

summary(model2)

# Analiza reszt

# Test Shapiro-Wilka
shapiro.test(model2$residuals)
# p-value = 0.9208 > 0.05
# Reszty nie podążają za rozkładem normalnym, to dobrze

# Test Goldfelda-Quandta
# p-value = 0.4059 brak podstaw że wariancja reszt nie jest stała, więc 
# przyjmujemy, że jest stała (homoskedastycznosc)
gqtest(model2)

# Losowość reszt - wizualnie wygląda jak chmura punktów
plot(model2$residuals)

# Test niezależności reszt
# Durbin-Watson
dwtest(model2)

# DW = 1.5691, co wskazuje na pozytywną autokorelację pomiędzy resztami
# Jednakże, p-value = 0.2977 co wskazuje na nieistotność wyniku

# Podaj przewidywaną wartość domu o powierzchni 160m^2 położonego w odległości 3 km od centrum miasta
predict(model2, list(x1=160, x2=3))

# 342.8

# Przewidywana wartość domu to 342 800 dolarów
```
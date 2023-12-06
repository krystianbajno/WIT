```
#W zamieszczonej poniżej tabeli podano wysokość rocznego dochodu i wartość posiadanego domu dziewięciu rodzin
#wybranych w sposób losowy spośród mieszkańców pewnego okręgu:
#  Roczny dochód ($ 1000) 36 64 49 21 28 47 58 19 32
#Wartość domu ($ 1000) 129 310 260 92 126 242 288 81 134

#a) Wyznacz prostą regresji wartości domu względem dochodu.
#b) Przeanalizuj dopasowanie modelu.
#c) Oszacuj wartość domu rodziny, której roczny dochód wynosi $40000.
#d) Wyznacz 95% przedział ufności dla szacowanej wartości domu tej rodziny. 

x <- c(36, 64, 49, 21, 28, 47, 58, 19, 32) #roczny dochod
y <- c(129, 310, 260, 92, 126, 242, 288, 81, 134) #wartosc domu

plot(x,y)

model1 = lm(y~x)

summary(model1)

# ) wyznacz prostą ...

#Call:
#  lm(formula = y ~ x)

#Residuals:
#  Min      1Q  Median      3Q     Max 
#-37.445  -9.504   3.286   7.550  22.492 #

#Coefficients:
#  Estimate Std. Error t value Pr(>|t|)    
#(Intercept)  -30.344     17.484  -1.736    0.126    
#x              5.466      0.415  13.172 3.39e-06 ***
#  ---
#  Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1#
#
#Residual standard error: 18.8 on 7 degrees of freedom
#Multiple R-squared:  0.9612,	Adjusted R-squared:  0.9557 
#F-statistic: 173.5 on 1 and 7 DF,  p-value: 3.394e-06

abline(model1, col=2, lwd=2)

text(40, 180, "Y = -30.344 +  5.466 * x", col=2)

# b przeanalizuj model

summary(model1)
#Estimate Std. Error t value Pr(>|t|)    
#(Intercept)  -30.344     17.484  -1.736    0.126    
#x              5.466      0.415  13.172 3.39e-06 ***

# Analizujemy R^2 dla modelu, wynosi on 0.9905, co jest bardzo bliskie 1. Im bliższe 1 tym lepiej
# Analizujemy RSE
summary(model1)$sigma

# RSE = 21.02994
# (średnia odległość obserwacji od prostej)
100*(summary(model1)$sigma)/mean(y)

# H0 nie jest związek pomiędzy punktem przecięcia (intercept) a zmienną Y
# H1 jest związek

# Intercept jest słabo dopasowany na podstawie p-value > 0.05 więc przyjmujemy H0 i wyrzucamy intercept z modelu

# H0 nie jest związek pomiędzy zmienną X a zmienną Y
# H1 jest związek

# p-value jest mniejsze od 0.05 dla zmiennej X i jest ona istotna w modelu, więc odrzucamy H0

model2 = lm(y~x+0)
summary(model2)
abline(model2, col=3, lwd=2)
#text(200, 10, text="Y = 4.7940 * X")

# Analizujemy R^2 dla modelu, wynosi on 0.9905, co jest bardzo bliskie 1. Im bliższe 1 tym lepiej
# Analizujemy RSE
summary(model2)$sigma

# RSE = 21.02994
# (średnia odległość obserwacji od prostej)
100*(summary(model2)$sigma)/mean(y)

# 11.38805 %, jest to niska-srednia wartość jest według tego wskaźnika dopasowane

# Normalnosc reszt
# Test Shapiro wilka
shapiro.test(model2$residuals)

#model2$residuals
#W = 0.96291, p-value = 0.8283

# H0 nie udaje się nie wykazać zbliżenia do rozkładu normalnego
# H1 jest normalność i zasada że ma nie być normalności nie jest wykazana

# p-value 0.8283 > 0.05, więc przyjmujemy H0 i zasada normalności reszt jest spełniona

# stałość wariancji reszt
# test goldfelda-quandta

install.packages("lmtest")
library(lmtest)
gqtest(model2)

# GQ = 0.26236, df1 = 4, df2 = 3, p-value = 0.8855
# H0 spełniona stałość wariancji (homokedastyczność)
# H1 niespełniona stałośc wariancji (heterokedastyczność)

# p-value = 0.8855

# Losowość reszt
# Wizualnie

plot(model2$residuals)

# Jest bardzo losowo, jest chaos, więc przyjmujemy, że reszty są losowe :)

# Test niezależności reszt
# Test Durbin Watsona

dwtest(model2)

# DW = 1.4025, co wskazuje na lekko pozytywną autokorelację pomiędzy resztami, co może wskazywać na lekki bias

# C) Oszacuj wartość domu rodziny której roczny dochód wynosi 40k

predict(model2, list(x=40))

# Wartośc domu rodziny wynosi według modelu 191 tysięcy.

# d) Wyznacz 95% przedział ufności dla szacowanej wartości domu tej rodziny.

predict(model2, list(x=40), interval="prediction", level=0.95)

# od 140 894 dolarów do 242 625 dolarów.
```
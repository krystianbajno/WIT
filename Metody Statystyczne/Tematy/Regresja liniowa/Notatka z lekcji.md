
```

# MST Lab 2

# zadanie 1

# zaleznosc Y = wartosci domu od X = dochodu

x <- c(36, 64, 49, 21, 28, 47, 58, 19, 32)
y <- c(129, 310, 260,	92,	126, 242,	288, 81, 134)

# a)
plot(x,y)
# widac zaleznosc liniowa (punkty ukladaja sie monotonicznie)
# wyznaczmy rownanie prostej metoda MNK

y =lm(y~x) # czyt. ~ wzgledem

# y = -30.344 +  5.466*x

abline(lm(y~x), col = 2, lwd = 2)
text(40,180, 'y = -30.344 +  5.466*x', col = 2)

# Czy ta prosta moze opisywac zaleznosc w populacji (w okregu)?

# b)  Y = -30.344 +  5.466*X + eps

model <- lm(y~x)
model$coefficients
model$coefficients[2]

summary(model)

# 1) Czy istnieje zaleznosc miedzy Y a X?

# p-value = 3.39e-06 *** < 0.05 >>> TAK

# 2) Czy wyraz wolny jest istotny w modelu?

# p-value =  0.126 > 0.05 >>> NIE >> do usuniecia

model2 <- lm(y~x+0) # Y = Beta1*X + eps
summary(model2) 

# nasz nowy model = model2: Y = 4.7940 * X + eps

abline(model2, col = 4, lwd =2)

# 3) Ocena dopasowania (R^2)
# w jakim stopniu zachowanie (zmiennosc) Y jest wyjasniana przez X?

# Multiple R-squared:  0.9905 
# to jest wartosc b.bliska 1, czyli Y jest w b.wysokim stoponiu wyjasniane
# przez X :))


# 4) Czy sa spelnioen zalozenia dla reszt?

plot(x,y)
abline(model2, col=4, lwd=2)

segments(x,y,x,model2$fitted.values) # hat(y) = model2$fitted.values

model2$residuals
identify(x,y)

y - model2$fitted.values # to samo co residuals

# 4a) normalnosc reszt
# H0: jest
# H1: nie ma

shapiro.test(model2$residuals)
# p-value = 0.8283 > 0.05 >>> H0, czyli spelniona normalnosc reszt

# 4b) stalosc wariancji reszt
# H0: jest
# H1: nie ma

install.packages('lmtest')
library(lmtest)

gqtest(model2)

# p-value = 0.8855 > 0.05, czyli H0, czyli spelniona stalosc wariancji
# (homokedastycznosc)

# 4c) losowosc reszt (wizualnie)
plot(model2$residuals)
abline(h=0, lty=2)

# punkty ukladaja sie raczej chaotycznie, przyjmujemy wiec ze reszty sa losowe

# Podsumowanie:
# Mamy model z barzdo wysokim R^2 i spelnionymi zalozeniami o resztach >>> Prognozy

# c) Jakie y dla x = 40 tys $?

# Y = 4.7940 * 40 = 191.76 tys $ # PROGNOZA PUNKTOWA
plot(x,y)
abline(model2, col = 4)
points(x=40,y=4.7940 * 40, pch = 8)

predict(model2, list(x=40))

# d)
predict(model2, list(x=40), interval = "prediction", level = 0.95) # (140.89; 242.62)
# = prognoza przyszlego Y 
# Mamy 95% pewnosci, ze dowolna rodzina z dochodem 40 tys $ ma dom o wartosci 
# w tym zakresie.
lines(c(40,40), predict(model2, list(x=40), interval = "prediction")[2:3])

predict(model2, list(x=40), interval = "confidence") # (176.41; 207.10) 
# - prognoza sredniej wartosci Y, tzn.
# Mamy 95% pewnosci, ze rodziny z dochodem 40 tys$ maja wartosc w tym zakresie.

predict(model2, list(x=40), interval = "confidence")[2:3]


# --------------------------------

# Zadanie 2

data(cars)
View(cars)
?cars


# Jak zalezy Y od X? 
# Y = dist 
# X = speed 

#a) 
y = cars$dist * 0.3048 # w metrach
x = cars$speed * 1.6 # w km/h


# b) 
plot(x,y)
plot(x,y, col='blue', pch='+')
plot(x,y, col='blue', pch=20, 
     xlab = 'prędkość [km/h]', ylab = 'droga hamowania [m]')

# Widoczna zaleznosc monotoniczna 

# c) 
cor(x,y)
cor.test(x,y, conf.level = 0.95)

# wspolczynnik korelacji ma wartosc [-1, 1]
# im blizej 1 lub -1, tym silniejsza zaleznosc
# od 0.8 można przyjac za silna, -0.3 do 0.3 - slaba



# d)
# Budowa modelu Y = beta0 + beta1*X + epsilon, beta0 = ?, beta1 = ?

model1 = lm(y~x) 
summary(model1) # mamy beta0 =  -5.3581 , beta1 =  0.7491 


# str(model1) # typ lista
# names(model1) # nazwy elementow listy
# model1$coefficients # wektor liczbowy (z atrybutem names roznym od NULL)
# model1$coefficients[2] # beta1

abline(model1, col=2, lwd=2)
text(20, 20, 'y = -5.358 + 0.749*x ', col=2)

summary(model1)
confint(model1)
# Czyli przy zwiększeniu prędkości o 1km/h długosc drogi hamowania
# wzrosnie od 0.59m do 0.91m.


# e) weryfikacja poprawnosci modelu Y = -5.3581 + 0.7491*X + epsilon

summary(model1)

# (1) Czy jest zaleznosc pomiedzy Y a X?
# H0: beta1 = 0 (nie)
# H1: beta1 != 0 (tak)

# test statystyczny 
# p-value = 1.49e-12 < 0.0001 < 0.05, zatem odrzucamy H0 i przyjmujemy H1


# (2) Czy stala beta0 jest istotna w modelu?
# H0: beta0 = 0 (nie)
# H1: beta0 != 0 (tak)

# test statystyczny 
# p-value = 0.0123 < 0.05, zatem odrzucamy H0 i przyjmujemy H1

# (3) ocena dopasowania modelu
# RSE = Residual standard error: 4.688 
summary(model1)$sigma
# (RSE/średnie_y)*100% = ? (średnia odległość obserwacji od prostej)
mean(y) # średnia arytmetyczna
100*4.688/mean(y) # = 35.78% - raczej duża wartość

# R^2 = współczynnik determinacji
# Multiple R-squared:  0.6511, czyli co najwyżej umiarkowane dopasowanie
# im bliżej 1 tym model lepiej dopasowany

summary(model1)$r.squared

# R^2 poniżej 0.5 = bezuzyteczny
# 0.5 - 0.6 - słabe dopasowanie
# 0.6 - 0.7 - co najwyżej umiarkowane dopasowanie
# 0.7 - 1 - b.dobre dopasowanie

# jaka część zmienności Y jest wyjaśniana na podstawie X


# (4) analiza reszt
model1$fitted.values # wartości przewidywne = hat(y) = wartosci y z prostej
segments(x,y,x,model1$fitted.values)

model1$residuals # reszty = y - hat(y) = y - model1$fitted.values
which.max(model1$residuals)
identify(x,y) # identyfikacja obserwacji na wykresie

plot(model1$residuals) # wykres reszt
abline(h=0, lty=2)

# mean(model1$residuals) # srednia reszt bliska jest 0
# t.test(model1$residuals)

# test Goldfelda-Quandta
install.packages("lmtest")
library(lmtest) # ładowanie pakietu lmtest

gqtest(model1)
# p-value = 0.1498 > 5% zatem przyjmujemy H0, czyli brak podstaw
# do stwierdzenia, że wariancja nie jest stała = przyjmujemy, ze stala wariancja


# test Shapiro-Wilka
shapiro.test(model1$residuals)

# p-value = 0.02152 < 5%, odrzucamy H0, czyli nie jest spełnione założenie 
# o normalności reszt

hist(model1$residuals, col=3)

# f) 
# Z czego może wynikać niespełnioe założenie o normalności reszt?
# Może wynikać z niepoprawnie przyjętej postaci modelu.

# sprawdzimy model nieliniowy logY = beta0 + beta1*logX + epsilon

model2 <- lm(log(y)~log(x))

plot(log(x), log(y))
abline(model2, col = 'blue')

# czy jest lepszy od modelu1?

summary(model2)

# model2: logY = -2.6709 +  1.6024*logX + epsilon
# (1) istnieje zaleznosc miedzy logY a logX, bo p-value = 2.26e-15 ***< 0.05
# (2) wyraz wolny jest istotny w modelu, bo p-value = 2.03e-07 ***<0.05

# (3) Multiple R-squared:  0.7331 i jest większe niż w modelu1
# czyli w wiekszym stopniu wyjasnia zmiennosc logY na podstawie logX.
summary(model1)$r.squared # R^2
summary(model2)$r.squared # :))) wieksze R^2 lepsze

summary(model1)$sigma # RSE
summary(model2)$sigma # :))) mniejszy RSE lepszy

summary(model1)$fstatistic # F
summary(model2)$fstatistic # :))) Im wieksze F tym lepsze



# (4)
plot(model2$residuals)
abline(h=0, lty=2)

gqtest(model2)
# p-value = 0.9965 > 5%, czyli wariancja jest stała

shapiro.test(model2$residuals)
# p-value = 0.9684 > 5%, czyli w modelu 2 reszty mają rozkład normalny

# Wniosek: Model2 jest lepszy od modelu1, bo ma wieksze R^2 i ma spelnione
# zalozenia dla reszt.


# g) Prognoza 
# Jaka jest droga hamowania (Y=?) dla predkosci x=30[km/h]?

model2 # logY = -2.671 + 1.602  * log(X) + eps

predict(model2, list(x=30)) # prognoza punktowa dla logY w modelu 2 

# logY = -2.6709 +  1.6024*log(30) = 2.779 to jest oszacowanie logY
# logY = 2.779 >>> Y=?
# exp(logY)=Y
exp(2.779) # szacowane Y, odp 16.1 m

exp(predict(model2, list(x=30))) # prognoza punktowa dla Y w modelu 2 
# przy predkosci 30 km/h prognozowana droga hamowania to 16.1 m


# Y dla jednego samochodu z 30km/h
# prognoza punktowa + 95% prognoza przedzialowa przyszlej wartosci Y
exp(predict(model2, list(x=c(30,35)), interval = "prediction")) 

# srednie Y dla wielu samochodow z 30km/h
# prognoza punktowa + 95% prognoza przedzialowa sredniej wartosci Y
exp(predict(model2, list(x=c(30,35)), interval = "confidence")) 


# --------------------

# Zadanie 3

data(trees)
View(trees)
names(trees)
?trees

# Y = Volume 
# X1 = Girth
# X2 = Height

pairs(trees)

# Model 1
m1 <- lm(Volume~Girth, data=trees)
summary(m1)

# Model1: Y = -36.9435 + 5.0659 * X1 + eps
# R-squared:  0.9353 :)))

# Model 2
m2 <- lm(Volume~Girth+Height, data=trees)
m2 <- lm(Volume~., data=trees) # rownowazny zapis
summary(m2)


# Weryfikacja poprawnosci modelu m2

# 1) czy Y zalezy od przynajmniej jednego z X1, X2?
# H0: nie
# H1: tak

# dla testu F p-value: < 2.2e-16  < 5%, zatem H1, czyli Y jest zalezne 
# od przynajmniej jednego z tych X1, X2.

# 2) Ktore X1, X2 sa istotne?
# Girth  = X1: < 2e-16 *** < 5%, czyli X1 istotne
# Height  = X2: 0.0145 * <5%, czyli X2 istotne
# 
# stala istotna, bo 2.75e-07 *** < 0.05

# uwaga: gdyby stala nie byla istotna, to usuwamy ja z modelu
# m2 <- lm(Volume~.+0, data=trees)

# Model 2: Y = -57.9877 + 4.7082 * X1 + 0.3393 * X2 + eps

# 3) Multiple R-squared:  0.948 czyli w wysokim stopniu Y jest wyjasniane 
# przez X1, X2

# 4) analiza reszt
reszty <- m2$residuals

# wykres reszt
plot(reszty)
abline(h=0, lty=2)

# trudno stwierdzic ze to jest chmura

shapiro.test(reszty) ## :))
gqtest(m2) ## :((

# prawdopodobnie blednie przyjeta postac modelu - moze jakis nieliniowy?


# wykres studentyzowanych reszt ri
rstudent(m2) # ri
plot(rstudent(m2))
abline(h=0, lty=2)

# wydaje si?, ?e na wykresie reszt nie mamy chmury punkt?W, a ze ukladaj? si?
# wzd?u? paraboli >>> prawdopodobnie b??dna specyfikacja modelu m2

# w tym przypadku prawdopodobnie jest jaka? zale?no?? nieliniowa miedzy Y a X1, X2.

# Typowe zabiegi na wykrycie nieliniowo?ci:
plot(trees$Girth, reszty) # brak chmury punkt?W >>>> czyli mozna dodac Girth^2
plot(trees$Height, reszty) # jest chmura

# lub mo?na po prostu przekszta?ci? nasze zmienne: log(), sqrt(), 1/X.


# Uwaga:
# lm(Y~X1+X2+X3+X4+X5+X6) np. okazuje sie ze X1,X2,X3 sa nieistotne
# wtedy nie usuwamy ich wszystkich jednoczesnie, lecz w pierwszej kolejnosci 
# usuwamy Xi z najwyzszym p-value > 5%, np. X2
# lm(Y~X1+X3+X4+X5+X6), ew. lm(Y~.-X2)

# porownanie m1 i m2
# dla m1
# Residual standard error: 4.252
# Multiple R-squared:  0.9353
# F-statistic: 419.4

# dla m2 
# Residual standard error: 3.882 mniejsze niz w m1 :)
# Multiple R-squared:  0.948 wieksze niz w m1 :)
# F-statistic:   255 

# # m1 i m2 to modele zagniezdzone
# # H0: m1 jest adekwatny
# # H1: m2 jest adekwatny
# 
# anova(m1, m2, test='F')
# # p-value = 0.01449 * < 5%, przyjmujemy H1, zatem m2 jest adekwatny



# model 3
m3 <- lm(log(Volume)~log(Girth)+log(Height), data=trees)
summary(m3)
# Multiple R-squared:  0.9777

# model 4
m4 <- lm(Volume~Girth+I(Girth*Girth)+Height, data=trees)
summary(m4)

# model 5
m5 <- lm(Volume~I(Girth*Height)+log(Girth), data=trees)
summary(m5)

m5 <- lm(Volume~I(Girth*Height), data=trees)
summary(m5)
# Multiple R-squared:  0.954

# wybór najepszego spośród m3, m4, m5
# na podsatwie R^2: m3
# na podstawie analizy reszt: czy założenia reszt sa spelnione?

# Analiza reszt
# 1) normalnosc reszt
shapiro.test(m3$residuals)
shapiro.test(m4$residuals)
shapiro.test(m5$residuals)

# 2) stalosc wariancji reszt
par(mfrow=c(2,2))
plot(rstudent(m3))
plot(rstudent(m4))
plot(rstudent(m5))
par(mfrow=c(1,1))


gqtest(m3)

# ------------- dalej na Lab 3 ---------------------


# Identyfikacja obserwacji odstających dla m5
plot(rstudent(m5), ylim=c(-3,3))
abline(h=2, col=2)
abline(h=-2, col=2)

identify(rstudent(m5)) # Esc = zakonczenie dzialania tej funkcji
trees[18,]

# Identyfikacja obserwacji wpływowych
# - na podstawie hatvalues
hatvalues(m5)
plot(hatvalues(m5))

m = 2 # liczba zmiennych niezaleznych
n = nrow(trees) # liczba obserwacji
abline(h=2*m/n, col=3) # czy hatvalues > 2*m/n?
identify(hatvalues(m5)) 

# obserwacja 31 jest wpływowa

# - na podstawie Cook's distance Di
cooks.distance(m5)
plot(cooks.distance(m5))

# wybieramy te obserwacje, ktore maj? wyra?nie wi?ksze Di od pozosta?ych
identify(cooks.distance(m5)) 
# obserwacja 31 jest wpływowa

# Można zbudować model z pominięciem obserwacji 31.


# Prognoza na podstawie m5
# Girth=20, Height=70, Volume=??

predict(m5, list(Girth=20, Height=70), interval = 'prediction') # wartosc przyszla

```
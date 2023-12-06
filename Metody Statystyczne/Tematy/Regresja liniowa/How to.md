
```
# 1) weryfikacja poprawnosci modelu Y = -5.3581 + 0.7491*X + epsilon

(1) Czy jest zaleznosc pomiedzy Y a X? (Ma być)
# H0: beta1 = 0 (nie)
# H1: beta1 != 0 (tak)
# test statystyczny 
# p-value = 1.49e-12 < 0.0001 < 0.05, zatem odrzucamy H0 i przyjmujemy H1

(2) Czy stala beta0 jest istotna w modelu?
# H0: beta0 = 0 (nie)
# H1: beta0 != 0 (tak)

# test statystyczny 
# p-value = 0.0123 < 0.05, zatem odrzucamy H0 i przyjmujemy H1

(3) ocena dopasowania modelu
# RSE = Residual standard error: 4.688 Ma być jak najmniejsza

# R^2 = współczynnik determinacji
# im bliżej 1 tym model lepiej dopasowany
# R^2 poniżej 0.5 = bezuzyteczny
# 0.5 - 0.6 - słabe dopasowanie
# 0.6 - 0.7 - co najwyżej umiarkowane dopasowanie
# 0.7 - 1 - b.dobre dopasowanie

# jaka część zmienności Y jest wyjaśniana na podstawie X

(4) analiza reszt
test Goldfelda-Quanta (ma być jak największe p-value)
test Shapiro-Wilka (ma być jak największe p-value)
test Durbina-Watsona (ma być jak najbliżej 2)
```


# RSE - Residual Standard Error
```
# RSE = Residual standard error: 4.688 
Mniejsze RSE jest lepsze
summary(model1)$sigma

1. **Bardzo wysoka wartość RSE:**
    - Powyżej 30% wartości średniej zmiennej zależnej.
2. **Wysoka wartość RSE:**
    - Od 20% do 30% wartości średniej zmiennej zależnej.
3. **Średnia wartość RSE:**
    - Od 10% do 20% wartości średniej zmiennej zależnej.
4. **Niska wartość RSE:**
    - Poniżej 10% wartości średniej zmiennej zależnej.

--------------------------------------------------------------

# (RSE/średnie_y)*100% = ? (średnia odległość obserwacji od prostej)
mean(y) # średnia arytmetyczna
100*4.688/mean(y) # = 35.78% - raczej duża wartość

Interpretacja jakości dopasowania modelu w oparciu o procentową średnią odległość obserwacji od prostej regresji może być przedstawiona w kontekście następujących zakresów:

1. **Bezużyteczny:**
    - Procentowa średnia odległość jest bardzo wysoka, np. powyżej 30-40%.
    - Oznacza to, że model jest bardzo słaby i nie dostarcza istotnych informacji ani dobrego dopasowania do danych. Procentowa odległość jest znacząca w stosunku do średniej wartości zmiennej zależnej.
2. **Słabe dopasowanie:**
    
    - Procentowa średnia odległość wynosi od 20% do 30%.
    - Model ma słabe dopasowanie do danych, a jego zdolność przewidywania jest ograniczona. Procentowa odległość jest znaczna, co sugeruje słabsze dopasowanie.
3. **Co najwyżej umiarkowane dopasowanie:**
    
    - Procentowa średnia odległość mieści się w zakresie od 10% do 20%.
    - Model dostarcza umiarkowane dopasowanie do danych, ale pozostawia pewien poziom reszt. Procentowa odległość jest umiarkowana, co sugeruje, że model tłumaczy większość, ale nie wszystkie zmienności w danych.
4. **Dobre dopasowanie:**
    
    - Procentowa średnia odległość wynosi poniżej 10%.
    - Model doskonale dopasowuje się do danych, a reszty są niewielkie. Procentowa odległość jest niska, co oznacza, że model jest w stanie precyzyjnie przewidywać zależną zmienną.

Warto pamiętać, że te wartości są ogólne i mogą się różnić w zależności od konkretnego kontekstu badawczego, danych i problemu analizy. Ostateczna ocena jakości dopasowania modelu powinna być oparta na kompleksowej analizie wielu metryk i zrozumieniu kontekstu danego zadania


```
# Ocena dopasowania (R^2)
```
# R^2 = współczynnik determinacji

# R^2 poniżej 0.5 = bezuzyteczny
# 0.5 - 0.6 - słabe dopasowanie
# 0.6 - 0.7 - co najwyżej umiarkowane dopasowanie
# 0.7 - 1 - b.dobre dopasowanie

# Multiple R-squared:  0.6511, czyli co najwyżej umiarkowane dopasowanie
# im bliżej 1 tym model lepiej dopasowany

summary(model1)$r.squared
```

# F Statistic
```
summary(model1)$r.squared # R^2
summary(model2)$r.squared # :))) wieksze R^2 lepsze

summary(model1)$sigma # RSE
summary(model2)$sigma # :))) mniejszy RSE lepszy

summary(model1)$fstatistic # F
summary(model2)$fstatistic # :))) Im wieksze F tym lepsze
```
## w jakim stopniu zachowanie (zmiennosc) Y jest wyjasniana przez X?
```
Multiple R-squared:  0.9905 to jest wartosc b.bliska 1, czyli Y jest w b.wysokim stoponiu wyjasniane
```


```
predict(model2, list(x=40), interval = "prediction", level = 0.95) # (140.89; 242.62)

# = prognoza przyszlego Y 
# Mamy 95% pewnosci, ze dowolna rodzina z dochodem 40 tys $ ma dom o wartosci 
# w tym zakresie.
lines(c(40,40), predict(model2, list(x=40), interval = "prediction")[2:3])

interval = "confidence"
predict(model2, list(x=40), interval = "confidence") # (176.41; 207.10) 
# - prognoza sredniej wartosci Y, tzn.
# Mamy 95% pewnosci, ze rodziny z dochodem 40 tys$ maja wartosc w tym zakresie.

predict(model2, list(x=40), interval = "confidence")[2:3]

```


```
model2 # logY = -2.671 + 1.602  * log(X) + eps
predict(model2, list(x=30)) # prognoza punktowa dla logY w modelu 2 

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
```
  
Przedział ufności (confidence interval) i przedział predykcji (prediction interval) mają różne zastosowania w kontekście regresji liniowej. Oto sytuacje, w których stosuje się każdy z nich, razem z przykładami zadań na kolokwium i ich rozwiązaniem:


------------
----------
### Przykład Zadania na Kolokwium:

1. **Przedział Ufności (Confidence Interval):**
    
    - **Zastosowanie:** Jeśli chcesz oszacować średnią wartość Y dla konkretnej wartości x z pewnym poziomem ufności.
    - **Przykład Zadania:** Osoba A chce oszacować przeciętną ilość produktów sprzedanych przez sklep w dniu, gdy X (wydatki na reklamę) wynoszą 20 tys. zł. Użyj przedziału ufności 95% dla średniej wartości Y.
    
    `# Przykładowe R code predict(model, newdata = data.frame(X = 20), interval = "confidence", level = 0.95)`
    
2. **Przedział Predykcji (Prediction Interval):**
    
    - **Zastosowanie:** Jeśli chcesz prognozować indywidualną wartość Y dla konkretnej wartości x z pewnym poziomem ufności.
    - **Przykład Zadania:** Osoba B chce przewidzieć ilość produktów sprzedanych przez sklep w konkretnym dniu, gdy X (wydatki na reklamę) wynoszą 20 tys. zł. Użyj przedziału predykcji 95% dla indywidualnej wartości Y.
    
    RCopy code
    
    `# Przykładowe R code predict(model, newdata = data.frame(X = 20), interval = "prediction", level = 0.95)`


### Rozwiązanie Zadania:

1. **Przedział Ufności (Confidence Interval):**
    
    - Wynik: [�,�][a,b] (np. [50,80][50,80])
    - Interpretacja: Z 95% pewnością przeciętna ilość produktów sprzedanych przez sklep w dniu, gdy wydatki na reklamę wynoszą 20 tys. zł, mieści się w przedziale od �a do �b.
2. **Przedział Predykcji (Prediction Interval):**
    
    - Wynik: [�,�][c,d] (np. [40,90][40,90])
    - Interpretacja: Z 95% pewnością pojedyncza ilość produktów sprzedanych przez sklep w konkretnym dniu, gdy wydatki na reklamę wynoszą 20 tys. zł, mieści się w przedziale od �c do �d.

W skrócie, przedział ufności ocenia przeciętną wartość Y, podczas gdy przedział predykcji uwzględnia większą niepewność związana z indywidualnymi prognozami. Wybór między nimi zależy od tego, czy interesuje Cię prognozowanie średnich wartości (przedział ufności) czy pojedynczych obserwacji (przedział predykcji).
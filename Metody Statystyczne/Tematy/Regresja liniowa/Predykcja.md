
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


This answer is for those readers who could not fully understand the previous answers. Let's discuss a specific example. Suppose you try to predict the people's weight from their height, sex (male, female) and diet (standard, low carb, vegetarian). Currently, there are more than 8 billion people on Earth. Of course, you can find many thousands of people having the same height and other two parameters but different weight. Their weights differ wildly because some of them have obesity and others may suffer from starvation. Most of those people will be somewhere in the middle.

One task is to predict the average weight of all the people having the same values of all three explanatory variables. Here we use the confidence interval. Another problem is to forecast the weight of some specific person. And we don't know the living circumstances of that individual. Here the prediction interval must be used. It is centered around the same point, but it must be much wider than the confidence interval.

[Serhii Kushchenko](https://stats.stackexchange.com/users/218389/serhii-kushchenko)

27122 silver badges55 bronze badges

- Thanks for the good example. So in your example for the first case, we have an uncertainty because we still only have a sample out of the entire population, so is the uncertainty we have here between the estimated mean and the true mean of the population? While in the second case, we have sampling variance as well as the residual error? 
    
    – [Pugl](https://stats.stackexchange.com/users/20395/pugl "1,481 reputation")
    
     [Apr 25, 2020 at 1:08](https://stats.stackexchange.com/questions/16493/difference-between-confidence-intervals-and-prediction-intervals#comment855965_423366)
    
- I'm not sure about your second case. Which interval to use, depends on the goal. 
    
    – [Serhii Kushchenko](https://stats.stackexchange.com/users/218389/serhii-kushchenko "271 reputation")
    
     [Apr 25, 2020 at 18:34](https://stats.stackexchange.com/questions/16493/difference-between-confidence-intervals-and-prediction-intervals#comment856126_423366)
    
- 2
    
    In short. Confidence Interval - A range for the expected AVERAGE Prediction Interval - A range for a SINGLE DATA POINT 
    
    – [kiwicomb123](https://stats.stackexchange.com/users/157474/kiwicomb123 "111 reputation")
    
     [Feb 6, 2021 at 21:18](https://stats.stackexchange.com/questions/16493/difference-between-confidence-intervals-and-prediction-intervals#comment938712_423366)
    
- 1
    
    Don't you think you can explain both with just the first example: confidence interval is the interval for true mean to lie within; whilst prediction interval is for all possible outcomes? Which is obviously wider. 
    
    – [Sergey Bushmanov](https://stats.stackexchange.com/users/76910/sergey-bushmanov "1,187 reputation")
    
     [Aug 30, 2021 at 18:12](https://stats.stackexchange.com/questions/16493/difference-between-confidence-intervals-and-prediction-intervals#comment995395_423366)


----

Przedział ufności (confidence interval) i przedział predykcji (prediction interval) mają różne zastosowania w kontekście regresji liniowej. Oto sytuacje, w których stosuje się każdy z nich, razem z przykładami zadań na kolokwium i ich rozwiązaniem:

----------
# GPT
### Przykład Zadania:

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
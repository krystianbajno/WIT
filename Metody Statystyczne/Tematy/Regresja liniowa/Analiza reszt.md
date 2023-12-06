# Czy sa spelnione zalozenia dla reszt?

Dla dobrze dopasowanego modelu reszty układają się jako chmura punktów wokół osi OX, tj nie wykazują żadnej struktury ani tendencji.

- weryfikacja rozkładu normalnego reszt (np. test Shapiro-Wilka),
- sprawdzenie stałości wariancji reszt (np. analiza wykresu reszt względem zmiennej zależnej, test
Goldfelda-Quandta),
- testowanie niezależności reszt (np. test Durbina-Watsona)

Dla dobrze dopasowanego modelu reszty układają się jako chmura punktów wokół osi OX,
tj. nie wykazują żadnej struktury ani tendencji

## Normalnosc reszt

```
# test Shapiro Wilka

model2$residuals
y - model2$fitted.values // to samo co $residuals

shapiro.test(model2$residuals)
shapiro.test(model2$residuals)

hist(model1$residuals, col=3)

- If p-value > 0.05: Fail to reject the null hypothesis.
- If p-value ≤ 0.05: Reject the null hypothesis.

# p-value = 0.8283 > 0.05 >>> H0, czyli spelniona (nie)normalnosc reszt (residuals do not follow normal distribution, to dobrze)

# p-value = 0.02152 < 5%, odrzucamy H0, czyli nie jest spełnione założenie 
# o (nie)normalności reszt, to źle

In simpler terms, the Shapiro-Wilk test helps you assess whether the residuals of your linear regression model follow a normal distribution. A normal distribution of residuals is one of the assumptions of linear regression, and violating this assumption can affect the reliability of your model's results.

In the output, if the p-value is less than 0.05 (or your chosen significance level), you may reject the null hypothesis and conclude that the residuals are not normally distributed.

Failing to reject the null hypothesis is generally good for your linear regression model. It suggests that the residuals are reasonably close to a normal distribution, supporting the validity of your regression results.

If you reject the null hypothesis, it indicates that the normality assumption may be violated. In such cases, you might need to consider transformations of the dependent or independent variables, or explore alternative modeling approaches.

```
## stalosc wariancji reszt

```
# test Goldfelda-Quandta

install.packages("lmtest")
library(lmtest) # ładowanie pakietu lmtest
gqtest(model2)

# p-value = 0.8855 > 0.05, czyli H0, czyli spelniona stalosc wariancji
# (homokedastycznosc)

# p-value = 0.1498 > 5% zatem przyjmujemy H0, czyli brak podstaw
# do stwierdzenia, że wariancja nie jest stała = przyjmujemy, ze stala wariancja

1. **Wysokie p-value (powyżej 0.05):** Brak istotnych dowodów na odrzucenie hipotezy o stałej wariancji. To jest pozytywne i wskazuje, że wariancja reszt jest w miarę stała, co jest jednym z założeń regresji.
    
2. **Niskie p-value (poniżej 0.05):** Istnieją istotne dowody na odrzucenie hipotezy o stałej wariancji. To może sugerować heteroskedastyczność, czyli niestałość wariancji reszt w zależności od wartości zmiennych niezależnych.

```
## losowosc reszt (wizualnie)

```
plot(model2$residuals)
abline(h=0, lty=2)
```

```
model1$fitted.values # wartości przewidywne = hat(y) = wartosci y z prostej
segments(x,y,x,model1$fitted.values)
which.max(model1$residuals)
```

### Testowanie niezależności reszt

```
install.packages('lmtest') 
library('lmtest')

dwtest(rt_model)

- If **`DW = 2`**, there is no autocorrelation in the residuals.
- If **`DW < 2`**, there is positive autocorrelation in the residuals.
- If **`DW > 2`**, there is negative autocorrelation in the residuals.

We can see that the results from the Durbin-Watson test output suggest positive autocorrelation in the residuals of the linear regression model rt_model. This implies that the errors are not independent and may violate the assumption of independent errors in the linear regression model. If this were real data, we would have to be cautious as this can lead to biased parameter estimates and incorrect inference.

The **`durbinWatsonTest()`** function from the **`car`** package is used to perform a Durbin-Watson test on a linear regression model. The function takes several arguments:

durbinWatsonTest(model, max.lag=1 simulate=TRUE, reps=1000, method=c("resample", "normal"), alternative=c("two.sided", "positive", "negative"))

```
  
The Durbin-Watson (DW) statistic is used to test for the presence of autocorrelation in the residuals of a regression model. The DW statistic ranges from 0 to 4, with a value of 2 indicating no autocorrelation. Generally:

- **DW close to 2:** Suggests no significant autocorrelation in the residuals.
    
- **DW significantly less than 2 (approaching 0):** Indicates positive autocorrelation (residuals are correlated in a positive manner).
    
- **DW significantly greater than 2 (approaching 4):** Indicates negative autocorrelation (residuals are correlated in a negative manner).
    

Here's how to interpret the DW statistic:

1. **DW = 2:** No autocorrelation (residuals are independent).
    
2. **DW < 2:** Positive autocorrelation (residuals are positively correlated).
    
3. **DW > 2:** Negative autocorrelation (residuals are negatively correlated).
    

Now, to address your questions:

- **Is DW equal to 2 good?** Yes, a DW value close to 2 is generally considered good because it suggests no significant autocorrelation in the residuals. It indicates that the assumption of independence of residuals is not violated.
    
- **Is negative autocorrelation good?** Negative autocorrelation (DW > 2) in the residuals is not considered "good" in the sense that it violates the assumption of independent errors. However, the degree to which it is a problem depends on the specific context. It can lead to inefficient estimates and incorrect standard errors, affecting the validity of hypothesis tests. Correcting for autocorrelation might involve using models that account for the correlation structure, such as autoregressive models.

- **Is positive autocorrelation good?** Positive autocorrelation (DW < 2) in the residuals is also not desirable. Like negative autocorrelation, positive autocorrelation violates the assumption of independent errors. It can lead to inefficient parameter estimates and incorrect inferences. Addressing positive autocorrelation may involve using alternative modeling techniques or transformations.

In summary, a DW value close to 2 is generally good, indicating no significant autocorrelation. Positive or negative autocorrelation, as indicated by extreme DW values, is not desirable and may require additional modeling considerations or diagnostic measures.

1. **Negative Autocorrelation:**
    - **Definition:** Negative autocorrelation occurs when a high residual at a particular time point is followed by a low residual at the next time point, and vice versa.
    - **Implication:** In the context of regression, negative autocorrelation suggests that the errors are inversely related over time. If one error is larger than expected, the next error is more likely to be smaller than expected.
2. **Positive Autocorrelation:**
    - **Definition:** Positive autocorrelation occurs when a high residual at a particular time point is followed by another high residual at the next time point, and a low residual is followed by another low residual.
    - **Implication:** In the context of regression, positive autocorrelation suggests that the errors are positively related over time. If one error is larger than expected, the next error is more likely to be larger than expected as well.

In summary, autocorrelation, whether positive or negative, indicates a systematic pattern in the residuals over time. It violates the assumption of independent errors in the regression model, and addressing autocorrelation is crucial for obtaining reliable parameter estimates and making valid statistical inferences.

```
# c) 
cor(x,y)
cor.test(x,y, conf.level = 0.95)

# wspolczynnik korelacji ma wartosc [-1, 1]
# im blizej 1 lub -1, tym silniejsza zaleznosc
# od 0.8 można przyjac za silna, -0.3 do 0.3 - slaba
```

```
# 1) Czy istnieje zaleznosc miedzy Y a X?
summary(model)

# p-value = 3.39e-06 *** < 0.05 >>> TAK
```

```
# 2) Czy wyraz wolny jest istotny w modelu?

# p-value =  0.126 > 0.05 >>> NIE >> do usuniecia
```

wizualnie

```
plot(x,y)
plot(x,y, col='blue', pch='+')
plot(x,y, col='blue', pch=20, 
```


In the context of linear regression modeling, it is generally assumed that the residuals (the differences between the observed and predicted values) are independent of each other. Independence of residuals is one of the key assumptions of linear regression. If residuals are correlated, it can have implications for the reliability of your regression analysis and may affect the validity of statistical inferences.

 If residuals are correlated, it can lead to biased parameter estimates. The estimated coefficients may be influenced by the correlation structure of the residuals, leading to unreliable results.

Violations of the independence assumption can also affect the validity of hypothesis tests and confidence intervals. Standard errors may be underestimated, potentially leading to overly optimistic assessments of statistical significance.
    
Correlated residuals may also affect the accuracy of predictions. If the correlation is systematic, it suggests that there is still information in the data that the model has not captured.
    
In some cases, autocorrelation (correlation between residuals at different time points) is expected and appropriate, especially in time series analysis. However, this is a specialized scenario and typically not applicable to standard linear regression models.

To check for the independence of residuals, you can examine residual plots, perform residual autocorrelation tests, or use other diagnostic tools. If you find evidence of correlated residuals, you might need to consider additional modeling techniques or transformations to address the issue.

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
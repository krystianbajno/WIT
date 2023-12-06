```
2+3 # Ctrl+Enter (Run)

10*10+10

# ----------------- wektory ----------

c(5, 2, 0, -4, 1)
-3:3
-3:2.5
seq(0,10,2.5)

rep(10,5)

rep(c(5, 2, 0, -4, 1), 2)
rep(c(5, 2, 0, -4, 1), each=2)

?rep # help

rep(x=c(5, 2, 0, -4, 1), times=2)
3

c(3)
2:5
c(2:5)

-2:5
-(2:5)
-c(2:5)

czas <- c(5, 30, 90, 15, 25, 35)

# indeskowanie (numery elementów) []

czas[1]
czas[0] # numeric(0) = wektor pusty
czas[0:2]

czas[c(1,3:4)]
czas[-1] # bez pierwszego
czas[-(1:2)]
czas[-c(3,5,6)]

length(czas)

czas[length(czas)] # ostatni
czas[length(czas):1]

rev(czas)

typeof(czas)
str(czas) # num = numeric
#
TRUE
FALSE

x <- c(TRUE, FALSE, FALSE)

#'Ania'

c('a', 't', 'h')
rep(c('a', 't', 'h'), 10)

-20:58
rm(x) # usuniecie obiektu x

ls() # wyswietlenie nazw wszystkich obiektow
rm(list = ls()) # usuniecie wszystkich obiektow  

#  +,-,*,/, %%

x <- c(1,5,10)
x + x # zasada element po elemencie
x^2 # zasada zawijania + zasada element po elemencie
x*2

x + c(100, 1000)
x + TRUE # + zasada uzgadniania typow

sum(c(TRUE,FALSE))

as.numeric(TRUE)
as.character(TRUE)
as.logical(100)

is.numeric(100)
is.logical(x)

# NA = brak danych

wiek <- c(30, 36, NA, 43, 45)
imie <- c('Ola','Jan','Ala','Maks','Rys')

imie[wiek > 30]

is.na(wiek)
!is.na(wiek)

imie[!is.na(wiek)] # imiona tych co maja wiek rozny od NA
imie[wiek > 30 & !is.na(wiek)] # wiek > 30 i wiek rozny od NA

# >, >=, <, <=,
# !, &, |, &&, ||

# c(TRUE,FALSE) & c(TRUE,TRUE)
# c(TRUE,FALSE) || c(TRUE,TRUE)

'pilka' > 'rower'

letters
set.seed(123) # ziarno generatora

letters[sample(5)]
sort(letters[sample(5)])
sample(1:49,6)

# ---------------- zadanie ------------
install.packages('nycflights13')

library(nycflights13)

data(planes)
?planes
View(planes)

planes$seats
min(planes$seats)
summary(planes$seats)

s <- planes$seats

summary(s)

hist(s) # hsitogram

hist(s, labels = TRUE)
hist(s, labels = TRUE, ylim = c(0,1200))
hist(s, labels = TRUE, ylim = c(0,1200), ylab = 'liczba samolotow')

colors()

hist(s, labels = TRUE, ylim = c(0,1200), ylab = 'liczba samolotow',
     col = "burlywood1")

hist(s, labels = TRUE, ylim = c(0,1200), ylab = 'liczba samolotow',
     col = 5)

hist(s, labels = TRUE, ylim = c(0,1200), ylab = 'liczba samolotow',
     col = c(5,7))

h <- hist(s)
h

h$counts
str(h) # info o h

boxplot(s)
boxplot(s, horizontal = TRUE)

points(s, rnorm(3322,1,0.05), col=2, cex=0.5)

# ------------ wyklad nr 1 --------------
mean(s)

sd(s)

# srednio samoloty maja 154 miejsca +- 73

mean(s, trim = 0.10)
median(s) # 50% samolotow ma max.149 miejsc
quantile(s)

abline(v = quantile(s), lty=2)

IQR(s)

1.5*IQR(s) # max. dlugosc wasa

?quantile

range(s)
length(range(s))
range(s)[1]

#skosnosc

install.packages('e1071')
library(e1071)

skewness(s) # :)
kurtosis(s)


# dwie zmienne ilosciowe
plot(planes$year, planes$seats) # wykres rozpreoszenia (scatterplot)

  
# jedna zmienna ilosciowa + jedna jakosciowa
boxplot(planes$seats~planes$engine)
table(planes$engine)
#

barplot(table(planes$engine), col = rainbow(6)) # wykres slupkowy

pie(table(planes$engine), col = 2:9)
```
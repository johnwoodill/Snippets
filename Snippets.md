# Snippets

Below are a list of common snippets used in various programming languages.  Most of the code will be in R and Python.  Feel free to use what you need.

### Contents
***
* Econometrics
  + [Dummy Variable Creator [R]] (### Dummy Variable Creator) 

* ggplot2
  + [Graph Function [R]] (### Graph Function) 

***
### Dummy Variable Creator
```
# Dummy Creator Function
dummyCreator <- function(invec, prefix = NULL) {
     L <- length(invec)
     ColNames <- sort(unique(invec))
     M <- matrix(0L, ncol = length(ColNames), nrow = L,
                 dimnames = list(NULL, ColNames))
     M[cbind(seq_len(L), match(invec, ColNames))] <- 1L
     if (!is.null(prefix)) colnames(M) <- paste(prefix, colnames(M), sep = "_")
     M
} 

#Usage
dummy <- dummyCreator(DATA$VARIABLE, prefix = "VARIABLE TO FACTOR")
DATA <- cbind(DATA, dummy)

#Example
dummy <- dummyCreator(DustBowlData_Pre$year, prefix = "year")
DustBowlData_Pre <- cbind(DustBowlData_Pre, dummy)
```

### Graph Function
```
qplot(X-RANGE, stat = "function", 
  fun = function(x) { FUNCTION }, 
  geom = "line")

# Example
qplot(c(0,10), stat = "function", 
  fun = function(q) 20 - 2*q, 
  geom="line", 
  xlab = "Quantity", 
  ylab = "Price") + 
  ggtitle("Demand Fn : P = 20 - 2Q")

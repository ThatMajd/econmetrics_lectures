# Lecture 1

## Types of Data

**Time Series Data:**

- Time series data consists of observations on a variable or several variables over time.
- Example: Monthly unemployment rates, daily stock prices.
- Characteristics: Trends, seasonality, and serial correlation.

**Cross Sectional Data:**

- Cross-sectional data is a random sample of observations at a single point in time.
- Example: Income levels of different individuals at one point in time.
- Challenges: Sample-selection problems if data is not a random sample.

## The Linear Regression Model

- Used to study the relationship between a dependent variable and one or more independent variables.
- General form:
  $$
  y = f(x_1, x_2, \ldots, x_K) + \epsilon
  $$
  or
  $$
  y = \beta_1 x_1 + \beta_2 x_2 + \cdots + \beta_K x_K + \epsilon
  $$

### Example – Demand Function

- Demand equation:
  $$
  \text{quantity} = \beta_1 + \text{price} \times \beta_2 + \text{income} \times \beta_3 + u
  $$
- Inverse demand equation:
  $$
  \text{price} = \gamma_1 + \text{quantity} \times \gamma_2 + \text{income} \times \gamma_3 + \epsilon
  $$

$$\epsilon, u \sim N(0,\sigma^2)$$

### Example: Returns to Education

- Basic model:
  $$
  \text{Earnings} = \beta_0 + \beta_1 \text{Education} + \epsilon
  $$
    this model isn't expressive enough, since older people make more money so we =>
- Considering age:
  $$
  \text{Earnings} = \beta_0 + \beta_1 \text{Education} + \beta_2 \text{Age} + \epsilon
  $$
    the relationship between earnings and age is not linear, usually we square the age (done in real life)
- Including non-linear effect of age:
  $$
  \text{Earnings} = \beta_0 + \beta_1 \text{Education} + \beta_2 \text{Age} + \beta_3 \text{Age}^2 + \epsilon
  $$

### Assumptions of the Classical Linear Model

1. **Linearity**: Model specifies a linear relationship between dependent and independent variables.
2. **Full Rank**: No exact linear relationship among the independent variables.
3. **Exogeneity**: Expected value of the disturbance is not a function of the independent variables, for any $i, j$
$$E[\epsilon_i|x_{j1}, x_{j2}, ...x_{jK}]=0$$
4. **Homoscedasticity and Non-autocorrelation**: Disturbances have the same finite variance and are **uncorrelated**.
$$Var(\epsilon_i)=Var(\epsilon_j)$$
5. **Normal Distribution**: Disturbances are normally distributed.
$$\epsilon_i \sim N(0,\sigma^2)$$

**Note:**

Having 2 variables that are correlated with each other complicates the analysis of the regression, to check for that we use VIF or look at correlation matrix.

If two variables are correlated and cause a certain error with the dependant variable, the error will cumulate from both

### The Loglinear Model

- Used for demand and production functions.
- Model:
  $$
  y = Ax^{\beta_2} e^\epsilon
  $$
- Taking logs:
  $$
  \ln y = \beta_1 + \beta_2 \ln x + \epsilon
  $$
- $\beta_1 = \ln A$

- $\beta_2$ is the elasticity of $y$ with respect to $x$, This means it measures the percentage change in the dependent variable $y$ for a 1% change in $x$.

### Interpretation of Log Models

1. If $ \ln y = \beta_1 + \beta_2 \ln x + u $:
   - $\beta_2$ is the elasticity of $y$ with respect to $x$.
2. If $ \ln y = \beta_1 + \beta_2 x + u $:
   - $\beta_2$ is the percentage change in $y$ given a 1 unit change in $x$.
3. If $ y = \beta_1 + \beta_2 \ln x + u $:
   - $\beta_2$ is the change in $y$ for a 100 percent change in $x$.

**Note**: $ln$ = percent change

### Example – The U.S.

$$
\begin{aligned}
    y &= \beta_0 + \beta_1 \ln(x_1) + \beta_2 \ln(x_2) + \ldots + \beta_K \ln(x_K) + u
\end{aligned}
$$

In the above equation:

- $ y $ is the dependent variable.
- $x_1, x_2, \ldots, x_K $ are the independent variables.
- $\beta_0, \beta_1, \ldots, \beta_K $ are the parameters to be estimated, and  represent elastisity
- $u$ is the error term.

This model is often used to study relationships where percentage changes in the independent variables are expected to have a multiplicative effect on the dependent variable.

### Example – Demand Function

**The Demand equation:**
$$ \text{quantity} = \beta_0 + \beta_1 \times \text{price} + \beta_2 \times \text{income} + u $$

**The inverse demand equation:**
$$ \text{price} = \gamma_0 + \gamma_1 \times \text{quantity} + \gamma_2 \times \text{income} + \epsilon $$

Random disturbances arise primarily since we cannot capture every influence on an economic variable in a model.

### Testing for Heteroskedasticity

Essentially want to test
$$ H_0: \text{Var}(u|x_1, x_2, \ldots, x_k) = \sigma^2 $$
which is equivalent to
$$ H_0: E(u^2|x_1, x_2, \ldots, x_k) = E(u^2) = \sigma^2 $$

since $$E[u]=0$$

If we assume the relationship between $u^2$ and $x_j$ will be linear,

We can test as a linear restriction. So, for $$ u^2 = \delta_0 + \delta_1 x_1 + \ldots + \delta_k x_k + v $$
this means testing $$ H_0: \delta_1 = \delta_2 = \ldots = \delta_k = 0 $$

**(WENT THROUGH QUICKLY)**

### The Breusch-Pagan Test

We do not observe the error, but we can estimate it with the residuals from the OLS regression. 

After regressing the residuals squared on all of the $ x $, we can use the $ R^2 $ to form an $ F $ or LM test.

The $ F $ statistic is just the reported $F$ statistic for overall significance of the regression,
$F = \frac{R^2/k}{(1 - R^2)/(n - k - 1)} $, which is distributed
$ F_{k, n - k - 1} $ 
The LM statistic is $LM = nR^2 $, which is distributed \( \chi^2_k \).

### The White Test

The Breusch-Pagan test will detect any linear forms of heteroskedasticity. The White test allows for nonlinearities by using squares and crossproducts of all the \( x \)'s. Still, just using an \( F \) or LM to test whether all the \( x_j, x_j^2 \), and \( x_j x_h \) are jointly significant.

### Case of form being known up to a multiplicative constant

Suppose the heteroskedasticity can be modeled as \( \text{Var}(u|x) = \sigma^2 h(x) \), where the trick is to figure out what \( h(x) \equiv h_i \) looks like. \( E(u_i / \sqrt{h_i} | x) = 0 \), because \( h_i \) is only a function of \( x \), and \( \text{Var}(u_i / \sqrt{h_i} | x) = \sigma^2 \), because we know \( \text{Var}(u|x) = \sigma^2 h_i \). So, if we divided our whole equation by \( \sqrt{h_i} \) we would have a model where the error is homoskedastic.

### Seasonality

Often time-series data exhibits some periodicity, such as stock prices. Since not a random sample, different problems to consider. Trends and seasonality will be important.


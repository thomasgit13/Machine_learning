
# Shapley Values

How to fairly distribute a payout among the player? 

Axioms: 

- Symmetry: If two players worked equally then they should receive equal payout.
- Dummy: Irrelevant players should get zero payout.
- Additivity: If a game has two sessions, then total payout for a player is the sum of contributions in the separate sessions.
- Efficiency: All players’ contributions must sum up to the total payout.

---

What is the contribution of the a feature in the prediction (for a particular instance).

There is an average value for the prediction. 

How much each feature contributes in the difference between average prediction and current prediction. 

We can have all the subsets and can find each marginal contribution for a particular feature.

If we have three features $x,y$ and $z$; we need to find the contribution of x in the prediction.

$f(x,y,z)-f(y,z)$ - marginal contribution of $x$  to $(x,y,z)$

$f(x)-f()$

$f(x,y)-f(y)$ 

$f(x,z)-f(z)$

Since it takes a lot of time if we have many number of features, we have a method to estimate shapley value. 

- we select a number of iterations - m , input instance - x , data matrix.
- Select a random instance - z
- Get a random permutation o
- arrange both the random instance and input instance as per the permutation.
- Create two vectors as follow
    - with feature j : $x_1, x_2, ...., x_{j-1}, x_j, z_{j+1}, ..., z_p.$
    - without the feature j: $x_1,x_2, ...,x_{j-1},z_j, ....,z_p$
- find the contribution by $f(x_{j+})- f(x_{j-})$
- Complete the iteration and find the average contribution
- Repeat for all the features.

---

## Shap- Shapely Additive Explanations

Shap combines lime and shapley values to provide explanations for a model prediction.

In Shap we fit a linear model with Shap Kernel and the coefficients of that linear model will be shapley values. 

$g(x)= \phi_o + \sum\phi_j$; here $\phi_o$ represents the expected value of the prediction(using training data) 

We need to get the training data and targets for fitting the explanatory model $g.$

First step is create multiple coalitions. ($(1,0,1,0),(0,1,0,0) ...)$ 

Coalition of $(1,0,1,0)$ represents we have a coalition of first and third features. 

Then we use a function $h(x)$ for converting these coalitions to valid data instance. These instances will become the training instance for the explanatory model $g$.

Now we can have the predictions of these coalitions from our original model $f$. These predictions will become the targets of the upcoming explanatory model $g.$

We give weights each coalitions in such a way that small coalitions and large coalitions will get largest weights. - we get more information about a feature when we study it in isolation. 

$\pi_x(z')= \frac{M-1}{\binom{M}{|z'|}|z'|(M-|z'|)}$, $M$  is the number of features and $z'$ represents the number of ones in the coalition vector. 

we take the loss function as follows;  

$L(f,g,\pi_x) = \sum{(f(x)-g(x))^2}\pi_x$

Fit weighted linear model. 

Return the Shapley values $\phi_k$ , the  coefficients from the linear model.
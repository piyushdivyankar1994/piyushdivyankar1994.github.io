# Asset Returns

For a financial time series we usually have a list of prices at a certain times. Now do we analyze these list of prices directly? The answer is we could but we will run into following problems. 
1. Different assets can have widely different prices. For example at the time writing this article TATA Steel share price was around 600 and SAIL share price was 74. So how do we compare these two. Does this mean that TATA steel share is more valueable than SAIL? 
2. The price keeps on increasing so there the mean of the price keeps increasing which isn't very helpful if we want to our analysis to hold over time.

So if not price then what is the right choice for the time series variable for analyzing financial time series. The variable chosen for time series analysis is the **returns**. Returns means how much has the price of stock changed relatively compared to the previous price. 
Here we see various type of returns that can be possible for time series. 

### One-period simple return
This is the relative change in price from time $t-1$ to $t$. If the return is $R_t$ then simple return for period $t$ is given by $$1+R_t=\frac{P_t}{P_{t-1}} \\ R_t=\frac{P_t-P_{t-1}}{P_{t-1}}$$

### Multi-period simple return
This is the relative change in price from time $t-k$ to $t$. Lets say the that the return is $R_{t_k}$. So we have that 
$$1+R_{t_k}=\frac{P_t}{P_{t-k}}=\frac{P_t}{P_{t-1}}\times\frac{P_{t-1}}{P_{t-2}}\times\frac{P_{t-1}}{P_{t-2}}\times\cdots\times\frac{P_{t-k+1}}{P_{t-k}}\times \\ 
1+R_{t_k} = (1+R_t)(1+R_{t-1})\cdots(1+R_{t-k+1}) = \product_{j=0}^{k-1}(1+R_{t-i})$$
This $R_{t_k}$ is the total return. Since this is a variable which changes over time it helps to know what is the mean return for a single time period. Here we have taken k time periods. One way to do this is take a arithmetic mean of the returns $R_i$, which is $$\bar{R}=\frac1k\sum_{i=0}^{k-1}R_{t-i}$$

This turns out to not be very useful as the returns are compunded. For example say that my returns in $3$ periods are $10\%, 20\%, -30\%$ the arithmetic mean gives us that average return should be $0\%$. Let's start with protfolio of $100$ units of capital, value after first year is $110$, after second year is $132$ and after third period is $92.4$. But the average tells that it should be $100$. 

Let's consider geometric mean of the gross returns(gross returns are $1+returns$). 
$$1+\bar{R}(k)=[\product__{i=0}^{k-1}(1+R_{t-i})]^{1/k}$$
If we plug in values above we get $\bar{R}(k)$ equal to $0.026$, this is more accurate representation of the average returns. 

We make a small change to this formula to make it computationally efficient. Computers are not very good at multiplying small fractional numbers make it so that it has to sum rather than multipy the gross returns. 
$$1+\bar{R}(k)=exp[\frac1k\sum_{i=0}^{i=k}\ln(1+R_{t-i})]$$

### Continuously compunded return 
This is simply the logarithm of the gross returns this has some nice properties that can be useful $$r_{t}=\ln(1+R_t)=\ln (P_t) - \ln(P_{t-1})$$
So this means $$r_{t_k}=\ln(1+R_{t_k})=\ln[(1+R_t)(1+R_{t-1})\cdots(1+R_{t-k+1})] \\ = \ln(P_t)-\ln(P_{t-k})$$

### Protfolio returns
The methods to describe returns above are applicable to a single asset. A protfolio is a collection of assets. So returns on a protfolio is the weighted average of the returns of the individual assets, where is the weight is the fraction of protfolio value allocated to the asset. Say there are $N$ assets in a protfolio with weights $w_1, w_2, ..., w_N$ and with returns at time $t$ equal to $R_{t,1}, R_{t,2}, ...R_{t,N}$ so the protfolio return is $$R_{p,t}=\sum_{i=1}^{N}w_iR_{t,i}$$

However continuously compunded returns are inconvinient for protfolio returns however as a first order approximation we can write the following. $$r_{p,t}=\sum_{i=1}^Nw_ir_{t,i}$$ 

### Dividends 
The simple returns during a period which gives dividends is slightly different. Say we get a dividend of $D_t$ in the period between $t-1$ and $t$ and $P_t$ be the price of the asset at the end of period $t$.  So return is given by $$R_t=\frac{P_t+D_t}{P_{t-1}}-1$$

### Excess return
Let's say we have a stock that gives us a return of $10\%$, is this return good or bad. How do we tell if a return is good or bad? One thing is for sure that all negative returns are bad, as we don't want to lose money. We need some sort of benchmark to determine if a return is good or bad. Some of the most common benchmarks are the risk-free interest rate, the market index returns, rate of inflation etc. These are the benchmarks because these returns are available without any activity on our part. To get a market return you can simply keep investing in a index fund, to get a risk free interest rate you can buy government securities. So if we are making a protfolio we want to know how well we perform relative to these benchmarks. The excess return is the return we get over and above the benchmark we have decided. 

---
title: We Finally Have a Believable Life Cycle Model
exports:
  - format: pdf
    template: arxiv_nips
    output: report.pdf
---

+++ { "part": "abstract" }

Anyone who has taken an economics class in high school or college will have heard of the \`life cycle model' of optimal saving for retirement.  When they hire a financial advisor, they might suppose that the advisor's job is to just to tailor standardized optimal planning tools to their own particular circumstances.  What they are unlikely to know is that the advice dispensed by traditional academic life cycle models has long been understood to be deeply problematic -- for example, such models tend to imply that retiree with a pension should plan to run their wealth down to zero (if they live long enough) and then (optimally!) live pension-check to pension-check.  This paper makes the case that new developments in the economics literature, when combined with the kinds of feedback that advisors get from their clients, can finally generate advice that is both mathematically optimal and intuitively plausible.

+++

# Introduction 

Franco Modigliani and Richard Brumberg (1954) were the first scholars to propose trying to understand consumer financial choices as reflecting optimal responses to the realities of the life cycle path of income and of spending needs. An enormous academic literature has followed their pioneering work, but only very recently have academic models of mathematically optimal behavior gotten within spitting range of matching the choices that real people actually make.

Three things have changed in the academic `life cycle mathematical optimization' literature that have jointly contributed to this success.

The first is that the rapid advance of computational capacity has finally made it possible to construct credible answers to the question "what saving and portfolio choices are actually optimal?" in a real world that has vast complexity.  In paticular, the incorporation of realistic descriptions of the uncertainties people face (about their own income, stock returns, interest rates, health expenditures, mortality, and more) makes the problem astonishingly difficult.  Vastly harder, say, than the computation of optimal trajectories for spacecraft, and comparable perhaps to the difficulty of driving a car (another problem where realistic computational (AI) solutions have only recently become available).

A second development has been a new openness by academic economists to the proposition that people's beliefs can be measured by asking them what they believe. The traditional academic approach had been to attribute to the optimial decisionmaker beliefs based on economists' own perceptions of the relevant facts (like the rate of return on the stock market). It turns out that economists' beliefs differ substantially from the beliefs that most people actually hold, and it seems reasonable to suppose that the decisions people make reflect their own beliefs rather than the beliefs of economists. Specifically with respect to stock returns, Mateo Velaszquez-Giraldo (2024) has shown that even college-educated people systematically have expected stock market returns substantially lower than the returns the stock market has historically delivered, and that the market performance, and have expected the riskiness of investment in stocks to be greater than the historical riskiness.

Finally, economists have also become more receptive to new kinds of evidence that go beyond the usual measurements of life cycle trajectories of wealth and income from traditional sources like the Federal Reserve's __Survey of Consumer Finances__ (SCF).  One particularly relevant example is feedback from the direct experience of financial advisors:  Many people do not appear to like the idea of running their wealth down to zero and then living pension-check to pension-check (which is what the traditional model says is optimal). The 'drawdown failure' has typically been patched up, in the academic literature, by adding a \`bequest motive' to the objectives of consumers.  But the available evidence finds that even childless people -- who presumably do not have much of a bequest motive -- do not draw down their wealth in ways consistent with the pure life cycle model (in which the only purpose of holding wealth is to finance your own future consumption). The model section of the paper advocates a direct and simple solution, which is to assume that people have an intrinsic desire to hold wealth which is distinct from the consequences those wealth holdings have for their ability to consume in the future.\footnote{See Carroll (2001) for an extended discussion of what those other motivations may be.} The main substantive/mathematical point of this paper (in the "Model Results" section) is to show that a model with \`wealth in the utility function' explains observed post-retirement behavior of both wealth-holding and portfolio choice at least as well as the traditional model with a standard bequest motive.

The thesis of this paper twofold.  The first is that when all of these elements are combined, a state-of-the-art mathematical optimization model can come reasonably close to explaining people's actual choices, given their actual beliefs. This provides an attractive resolution to the awkward fact that the financial industry's advice has, until now, had no underpinning but tradition. The resolution takes the satisfying form that perhaps financial advisors had a better idea all along what constituted good advice, and only now are the rigorous mathematical/computational models able to explain why.

# Literature Review

[](doi:10.3982/ecta16409)

[](doi:10.1257/000282802320189393)

# Model

## The Baseline Academic Model

### With No Bequest Motive

In each period, a consumer's utility depends on how much they consume. We assume that the utility function is of the standard Constant Relative Risk Aversion form:
\begin{align}
\uFunc(c) & = \frac{c^{1-\CRRA}}{1-\CRRA}
\end{align}
but of course the consumer is smart enough to realize that preserving some of their resources for the future is probably a good idea; this is why all wealth is not consumed immediately.

We follow tradition that consumer's financial circumstances are assumed to be measured by two variables. $\pLvl_{t}$ is the consumer's permanent income level (roughly, the income they would normally expect to receive), while $\mLvl_{t}$ is total market resources (the sum of financial assets and current income -- think of this as the pool of resources that can be immediately spent; \`money' in the colloquial sense of \`how much money does grandma have?').

The \`value' of having a given amount of market resources $\mLvl_{t}$ right now, and of knowing your current permanent income level to be $\pLvl_{t}$, is determined by the utility you will experience from consumption today, as well as the utility you expect to experience in the future. Any future period matters to you only to the extent that you expect to survive to that period. There are other reasons that the \`exchange rate' between current utility and future utility may not be one-for-one: For example, you may have some degree of present bias (which we denote by $\beth$ where $\beth < 1$ means that you are \`present-biased: You overweight your current self compared to your future self). An adjustment for household-size changes is also conventional in the literature, and is captured in our notation with an age-varying factor $\hat{\DiscFac}$.

In formal mathematical terms, the consumer's objective is to maximize present discounted utility from consumption over a life cycle that ends no later than date $T$ (often set to age 120):
\begin{equation}
  \pmb{\vFunc}_{t}(\mLvl_{t},\pLvl_{t})  =    \max_{\{\cFunc\}_{t}^{T}} ~ \uFunc(\cLvl_{t})+\Ex_{t}\left[\sum_{n=1}^{T-t} {\beth}^{n} \Alive_{t}^{t+n}\hat{\DiscFac}_{t}^{t+n} \uFunc(\cLvl_{t+n}) \right]   \label{eq:lifecyclemax}
\end{equation}

\begin{align}
    \\ \Alive _{t}^{t+n} & :  \text{probability to }\Alive\text{ive until age $t+n$ given you are alive at age $t$}
 
 \\ & {~~~}\bullet \text{$\Alive_{120}^{121} = 0.0$ says that a 120 year old has zero probability of living to 121}
 \\ & {~~~}\bullet \text{$\Alive_{80}^{90} = 0.3$ says that an 80 year old has a 30 percent chance of reaching 90}
% \\ & {~~~}\bullet \text{$\Alive_{81}      = 0.9$ says that an 80 year old has a 90 percent chance of reaching 91}
    \\ \hat{\DiscFac}_{t}^{t+n} & :  \text{age-varying discount factor between ages $t$ and $t+n$}
	\\ & {~~~} \bullet \text{captures age-varying spending needs (mainly, adjusts for family size)}
    \\ \beth & :  \text{time-invariant `pure' time preference factor}
	\\ & {~~~} \bullet \text{rate of `present bias'; $\beth=1$ corresponds to no present bias}
\end{align}

We use standard calibrations for the household-size adjustment (from Cagetti (2003)) and mortality (taken from actuarial mortality tables like those used by the Social Security administration). The time preference factor is estimated by the `indirect inference' procedure described below.

One of the fundamental discoveries of the past 30 years or so is the extent to which optimal choice is profoundly altered by the presence of uncertainty. Milton Friedman (1957) proposed a simple formulation that remains an excellent description of annual income shocks even today. Friedman said that there are two components to income: A \`permanent' component that is roughly what a person would expect to earn in a \`normal' year (say, their annual salary), and a \`transitory' component that reflects events like unemployment spells or lottery winnings; these make a given year's actual income deviate from its expected value.

To meld Friedmanian uncertainty with a Modlglianian life cycle, we need one more definition, whose purpose is to capture the predictable patterns that (noncapital) income follows over the lifetime (income starts low, rises with age and experience, and falls at retirement to the level of any regular pension payments):
\begin{align}
    \permGroFac_{t+1} & :  \text{typical life cycle permanent income growth factor by age}
\end{align}

But the typical life cycle pattern is altered, in any particular consumer's case, by \`permanent shocks' which we represent with the variable $\permShk$.  At any given age, actual permanent growth can deviate from the average experience of others of the same age in either a positive direction ($\psi>1$ would correspond to an unexpected promotion or a switch to a higher-paying job) or a negative direction ($\psi < 1$ might be the result of a failure to be promoted or a change to a lower paying job). 

This gives us the following description of the dynamics of permanent income $\pLvl$:
\begin{align}
\pLvl_{t+1} & = \pLvl_{t} \permGroFac_{t+1} \permShk_{t+1} 
\\ \Ex_{t}[\pLvl_{t+1}] & = \pLvl_{t} \permGroFac_{t+1} 
\end{align}
where the second line follows from the first because the expected value of the permanent shock is $\Ex_{t}[\permShk]=1$. 

The transitory shock to income has two modes. In unemployment spells, the consumer earns no income; we assume that such spells occur with probability $\pZero$.\footnote{It is straightforward to extend the model to allow for a more realistic treatment of unemployment, for example by taking account of the existence of an unemployment insurance system; such an adjustment does not change the substantive conclusions we are interested in.}. If the consumer remains employed, we will assume that the income shocks are lognormally distributed:
\begin{align}
\tranShkEmp_{s}  = &
    \begin{cases}
        0\phantom{/\pZero} & \text{with probability $\pZero>0$}
        \\ \xi_{s}/\pZero & \text{with probability $(1-\pZero)$}
    \end{cases}

  \end{align}

It is conventional to assume that shocks to permanent income and to the transitory income of the employed are lognormally distributed:
\begin{align}
\log \permShk_{s}   \thicksim \mathcal{N}(-\sigma_{[\permShk, t]}^{2}/2,\sigma_{[\permShk, t]}^{2})
\\ \log \xi_{s}\thicksim \mathcal{N}(-\sigma_{[\xi, t]}^{2}/2,\sigma_{[\xi, t]}^{2})
\end{align}
which, together with the other assumptions, guarantee that the expected value of the transitory and of the permanent shocks are both 1: $\Ex_{t}[\permShk_{t+1}]=\Ex_{t}[\tranShk_{t+1}]=1$.  (These are standard assumptions and we use standard calibrations of both of these shock processes.)

Under the assumptions we have made about the structure of the utility function (homotheticity) and budget constraint (linearity and geometric returns), it is possible to recast the problem entirely in terms of _ratios_ of the model variables to permanent income $\pLvl$. So, for example, italic $\cNrm = \cLvl/\pLvl$ is the ratio of the (boldface) level of consumption to the level of permanent income $\pLvl$ (cf. [](doi:10.3386/w10867) for the math). 

Another way to make the problem easier to understand is to combine several of the multiplicative terms into portmanteau variables.  Defining boldface $\pmb{\DiscFac}_{t+1}$ as 
\begin{align}
\pmb{\DiscFac}_{t+1} & = \beth \hat{\beta}_{t}^{t+1} (\permShk_{t+1} \PermGroFac_{t+1})^{1-\CRRA} 
%\\ \RNrm_{t+1} & = \left(\frac{\Rfree}{\permShk_{t+1}\permGroFac_{t+1}}\right)
\end{align}
%and simplifying the notation for the probability of survival to $\Alive_{t+1} \equiv \Alive_{t}^{t+1}$

Finally, under the assumptions we have made, it turns out that the consumer's problem can be expressed more simply by realzing that it boils down to a `now versus later' problem.
All the consumer really needs to know about the future is summarized by the value they will expect as a consequence of ending the current period with a certain ratio of assets to permanent income, $\aNrm = \aLvl/\pLvl$. We can represent the value of ending the period with assets of $\aNrm$ using the Gothic variant of the letter $\vFunc$:
\begin{align}
\mathfrak{v}_{t}(\aNrm_{t}) &= \Ex_{t}[\pmb{\DiscFac}\vFunc_{t+1}(\mNrm_{t+1})]
\end{align}

After all of these steps, the problem can be rewritten as
\begin{align}
    {\vFunc}_{t}({\mNrm}_{t}) & = \max_{\cNrm_{t}} ~ \uFunc(\cNrm_{t})+\Alive_{t+1} \mathfrak{v}_{t}(\aNrm_{t})
    \\ & \text{s.t.} & 
    \\ \aNrm_{t} & = {\mNrm}_{t}-\cNrm_{t} 
%    \\ {\mNrm}_{t+1} & = \aNrm_{t}\RNrm_{t+1} + ~\tranShkEmp_{t+1}
\end{align}

| object | meaning | 
| --- | --- | 
| $\mNrm, \cNrm, \aNrm$ | market resources, consumption, and end-of-period assets, normalized by permanent income |
|  $\vFunc$ |  the normalized value function |
| $\Alive_{t+1} \equiv \Alive_{t}^{t+1}$ | probability a person alive at date $t$ survives to date $t+1$ |

and since $\aNrm$ measures available resources that are unspent, this formulation makes it crystal clear that the consumer faces a tradeoff between the utility of consumption today and the expected value of preserving assets $\aNrm=\mNrm-\cNrm$ for the future.

\footnote{The normalization for value function involves more than just division by $\pLvl$; see \cite{ccarrollBufferStockTheory} for details.}
where $\cNrm$, $\aNrm$, and $\mNrm$ are consumption, assets, and market resources normalized by permanent income, and 
%; and $\RNrm_{t+1}$ is a permanent-income-growth-normalized return factor


### With A Standard Bequest Motive

A rough estimate might be that the behavior of a third of retired households (predominantly those with less education and lower lifetime permanent incomes) can be interpreted in a way that is explainable using the `pure life cycle' model articulated above -- including the prediction that retired people will tend to run down their wealth to zero and then live pension-check to pension-check.

On the other hand, the model can make no sense at all of the behavior of the very rich. Bill Gates, for example, has chosen to allocate a large portion of his lifetime wealth to the Bill and Melinda Gates foundation, and shows no sign of attempting to consume his remaining wealth over his remaining lifetime. 

% AL: Could you update my calculation from the WhyDoTheRichSave paper of how much he would need to spend each day to accomplish this?

But the focus of the academic literature has mostly been on broadly capturing the behavior of the bulk of the population - neither the pension-check to pension-check minority nor the superrich superminority. 

% explain why lit has added this:
% - people don't seem to draw down their wealth as they age

% AL: If you could make a figure from the SCF, or find one in a published paper, that would be great

The problem, in a nutshell, is that the mathematical model assumes that the only reason to hold wealth is to pay for one's own future consumption expenditures -- which means that eventually an age must come at which the consumer begins to spend the wealth down. For a sustantial portion of households, this point seems never to come -- this is the \`drawdown failure' mentioned in the introduction.

From the mathematical point of view, it is clear that some other motive for holding onto wealth must be added to the framework if it is to explain these facts. A natural candidate is a bequest motive: The idea that people take pleasure in the thought of leaving something to their heirs.

This can be accommodated very simply by adding another term to the sources of value: the value the consumer places on the bequest, which we will denote as $\ell(\aNrm)$ (think of this as they utility they experience from the thought of leaving a $\ell$egacy).

Defining the probability of passing away as the probability of not $\Alive$iving to the next period,
\begin{align}
\cancel{\Alive} & =(1-\Alive)
\end{align}
the flow of utility that the consumer receives now includes both their utility from consumption _and_ the pleasure they take from the thought that, if they pass away before next period (which happens with probability $\cancel{\Alive}$), their assets will pass to their heirs.

The consumer's new value function is therefore just
\begin{align}
    {\vFunc}_{t}({\mNrm}_{t}) & = \max_{\cNrm_{t}} ~ \overbrace{\uFunc(\cNrm_{t})}^{\text{present}}+\overbrace{\underbrace{\Alive_{t+1}\mathfrak{v}(\aNrm_{t})}_{\text{live}} + \underbrace{\cancel{\Alive}_{t+1}\ell({\aNrm}_{t})}_{\text{die}}
	}^{\text{future}}.
\end{align}

% Explain objections to bequest motive
% - childless save as much or more as those with heirs
% - people do not list bequests as important (in SCF survey questions)
% - typical household leaves only 2 percent of lifetime resources as bequests (Lutz Hendricks)
% - Modigliani versus Kotlikoff and Summers (1986) debate

## Wealth In the Utility Function (WIUF)

### Motivations

#### Why Do the Rich Save So Much?
Andrew Carnegie, then the richest man in the world, famously pledged to give away 90 percent of his wealth before his death (and made good on his promise). Carnegie was explicit: He had vastly more wealth than necessary to accommodate his wants (including maintenance of his beloved Scottish castle); he thought considerable social good could be accomplished by the charities he favored (especially libraries); and he felt that the expectation of receiving a colossal inheritance would `ruin' a child.\footnote{"I would as soon leave my son a curse as the almighty dollar." \cite{jaher:gildedage}.} The reason economists should be interested in extreme examples like Carnegie (or Bill Gates, or John D. Rockefeller) is the same reason physicists are interested in black holes: Stress tests of a theory can reveal its flaws (Einstein beats Newton only in such extreme cases). The historian Fredrick Cople \cite{jaher:gildedAge}'s chronicle of the behavior of the richest Americans since the 1800s (Carnegie is one of many examples) is striking in two ways. His book contains a feast of quotes, over a long time span, from the richest Americans articulating a host of motivations for wealth accumulation; and very few of these mention anything resembling the bequest motive as formulated in the academic life cycle literature.

This is consonant with the views of Max Weber (1905), who argued that the 'spirit of capitalism' was that it was intrinsically virtuous to accumulate wealth. And also in line with survey data from the modern __Surveys of Consumer Finances__, which find that only 5 percent of respondents, and only 4 percent of respondents in the richest 1 percent, put 'leaving an inheritance' among __the top 5__ reasons for saving (\cite{WhyDoTheRich}).

Financial advisors to 401(k) plans also report a strong allergy, on the part of corporate 401(k) fiduciaries, to any mention of leaving a bequest as a legitimate target of 401(k) saving advice. (Possibly this reflects the fact that pension plan sponsors owe a fiduciary duty to the plan participants, but not to their heirs.)
% JT: Can I say this? Is there a citation I can use?

Given these objections to the bequest motive, and given the problems of a model without a bequest motive, it seems natural to consider other modifications to the Modigliani-Brumberg assumption that the only purpose of holding wealth is to enable future consumption. 

#### Paper provides a Host of Reasons -- 
% For our purposes, the takeaway from this paper is that it presents a context in which the neither the Modgliani-Brumberg assumption that wealth is held only to finance future consumption, nor the standard augmentation of that model to accommodate the desire to leave a bequest to heirs, seems to suffice for explaining behavior with respect to wealth.

The most general way we economists have of incorporating motivations into our models of behavior is simply to assume that the decisionmaker gets utility, directly, from something -- in this case, from holding wealth. The next question is how best to structure the utility function to study any particular question. The \cite{WhyDoTheRich} paper, for example, proposed a utility function specifically designed to capture behavior as wealth approached infinity, and accomplishing that goal required some mathematical structure that delivered the desired results but was unwieldy (and not obviously necessary for explaining the behavior of the bottom 99 percent, whose wealth does not approach infinity).\footnote{Specifically, a separable utility-from-wealth function was added to the maximizer's objective and with a coefficient of relative risk aversion smaller than that for the utility from consumption, which delivers the desired result.}

#### Money in the Utility Function (Sidrauski; Rotermberg and Poterba)
In fact, it turns out that there is a literature in macroeconomics, pioneered by Miguel Sidrauski in his paper [Rational choice and 
Patterns of Growth in a Monetary Economy](), that has long included \`money' in the utility function of the representative agent in one form or another. 

A well-known paper by [](doi:10.1086/261207) proposed a specific utility function designed to capture the stability of the ratio of money to GDP, and Rotemberg along with James Poterba estimated this model on U.S. data in [](doi:10.3386/w1796).

The structure of their utility function is
\begin{align}
\uFunc(\cNrm,\ell) & = \frac{\left(
    \cNrm^{\delta}\ell^{1-\delta}
    \right)^{1-\CRRA}}{1-\CRRA}
\end{align}
where $\ell$ captures the the liquidity services provided by money-holding. 

To be clear, the aim of that literature was to explain the holding of dollar cash balances to study questions like the 'velocity' of money and the role of money supply and money demand in determining interest rates -- not to explain saving behavior.

But for the question of how to incorporate wealth in the utility function, Tzitzouris et al have proposed a mathematically very similar formulation,
\begin{align}
\uFunc(\cNrm,\aNrm) & = \frac{\left(
    \cNrm^{\delta}\aNrm^{1-\delta}
    \right)^{1-\CRRA}}{1-\CRRA}
\end{align}
where $\aNrm$ takes the place of $\ell$ in the Rotemberg-Poterba utility function.\footnote{If we assume, reasonably enough, that liquidity services are directly proportional to the holdings of the assets that provide those services, the two formulations become (mathematically) identical.}^{,}\footnote{The question of whether $\aNrm$ or $\mNrm$ should be in the utility function is not very consequential; here we prefer $\aNrm$ because assets after consumption are immune to considerations of whether the time period is a year, a quarter, a month, or a day.}

The upshot is that if we credit the proposition that the ownership of assets yields utility, then there is good precedent for the functional form of utility proposed by Tzitsouris et al in the work of Rotemberg and Poterba.  Henceforth we will call this Cobb-Douglas formulation of the utility provided by asset holdings the Tzitzouris-Rotemberg-Poterba or 'TRP' utility function.

% postulated a utility of wealth that implied that such ownership was a `luxury good' in the sense that the more lifetime resources a person had available, the larger was the proportion that would be devoted to the pleasures (whatever they may be) of wealth ownership _per se_. The model was constructed specifically to capture the fact that at the extreme upper reaches of the wealth distribution it seems likely that the amount of ordinary consumption expenditure the agent could accomplish during the span of a human lifetime becomes small.

It is a simple matter to solve the revised problem with wealth in the utility function using the TRP utility specification. The revised value function of the problem is:

%A simple extension to the stochastic Life Cycle model is to include wealth in the utility function directly. [](doi:10.3386/w6549) argues that models in which the only driver of wealth accumulation is consumption smoothing are not consistent with the saving behavior of the wealthiest households. Instead, they propose a model in which households derive utility from their level of wealth itself or they derive a flow of services from political power and social status, calling it the `Capitalist Spirit' model. In turn, we can add this feature to the LCIM model by adding a utility function with consumption and wealth. We call this the Wealth in the Utility Function Incomplete Markets (WUFIM) model. 

\begin{align}
    {\vFunc}_{t}({\mNrm}_{t}) & = \max_{\cNrm_{t}} ~ \uFunc(\cNrm_{t}, \aNrm_{t})+\Alive_{t+1}\mathfrak{v}_{t}(a_{t})
%    \\ & \text{s.t.} & 
%    \\ \aNrm_{t} & = {\mNrm}_{t}-\cNrm_{t} 
%    \\ {\mNrm}_{t+1} & = \aNrm_{t}\RNrm_{t+1}+ ~\tranShkEmp_{t+1}
\end{align}

The methods of solution are essentially the same as those for the model with a bequest.  

% **Separable Utility** [](doi:10.3386/w6549) presents extensive empirical and informal evidence for a LCIM model with wealth in the utility function. Specifically, the paper uses a utility that is separable in consumption and wealth:

# Estimation and Calibration

### Indirect Inference Described
Even if you knew all the parameters of the model (the consumer's coefficient of relative risk aversion; their time preference factor), solving an optimization problem that includes the many real-world complications described above (especially those due to uncertainty) is such a formidable problem that it only became possible about 25 years ago, and solving the models took days.

But of course we do not know the best values to choose for unobservable parameters like relative risk aversion and time preference rates.  The solution to this problem that is now becoming standard is to the method of 'indirect inference.'  Essentially, this means specifying the structure of your model except for the values of parameters that you cannot measure well (like time preference and risk aversion), and asking a numerical search algorithm to seek the values of parameters that makes the model fit the data as well as it is capable of doing.  This requires the computer to solve the problem perhaps thousands of times, which is why indirect inference is only coming into its own now - when computer speeds have gotten f---
title: We Finally Have a Believable Life Cycle Model
exports:
  - format: pdf
    template: arxiv_nips
    output: report.pdf
---

+++ { "part": "abstract" }

Anyone who has taken an economics class in high school or college will have heard of the \`life cycle model' of optimal saving for retirement.  They might suppose that a financial advisor's job is to just to tailor standardized optimal planning tools to their own particular circumstances.  What they are unlikely to know is that the advice dispensed by traditional life cycle models has long been understood to be deeply problematic -- for example, such models tend to imply that retiree with a pension should plan to run their wealth down to zero (if they live long enough) and then (optimally!) live pension-check to pension-check.  This paper makes the case that new developments in the economics literature, when combined with the kinds of feedback that advisors get from their clients, can finally generate advice that is both mathematically optimal and intuitively plausible.

+++

# Introduction 

Franco Modigliani and Richard Brumberg (1954) were the first scholars to propose trying to understand consumer financial choices as reflecting optimal responses to the realities of the life cycle path of income and of spending needs. An enormous academic literature has followed their pioneering work, but only very recently have academic models of mathematically optimal behavior gotten within spitting range of matching the choices that real people actually make.

Three things have changed in the academic `life cycle mathematical optimization' literature that have jointly contributed to this success.

The first is that the rapid advance of computational capacity has finally made it possible to construct credible answers to the question "what saving and portfolio choices are actually optimal?" in a real world that has vast complexity.  In paticular, the incorporation of realistic descriptions of the uncertainties people face (about their own income, stock returns, interest rates, health expenditures, and more) makes the problem astonishingly difficult.  Vastly harder, say, than the computation of optimal trajectories for spacecraft, and comparable perhaps to the difficulty of driving a car (another problem where realistic computational (AI) solutions have only recently become available).

A second development has been a new openness by academic economists to the proposition that people's beliefs can be measured by asking them what they believe. The traditional academic approach had been to attribute to the optimial decisionmaker beliefs based on economists' own perceptions of the relevant facts (like the rate of return on the stock market). It turns out that economists' beliefs differ substantially from the beliefs that most people actually hold, and it seems reasonable to suppose that the decisions people make reflect their own beliefs rather than the beliefs of economists. Specifically with respect to stock returns, Mateo Velaszquez-Giraldo (2024) has shown that even college-educated people systematically have expected stock market returns substantially lower than the returns the stock market has historically delivered, and that the market performance, and have expected the riskiness of investment in stocks to be greater than the historical riskiness.

Finally, economists have also become more receptive to new kinds of evidence that go beyond the usual measurements of life cycle trajectories of wealth and income from traditional sources like the Federal Reserve's __Survey of Consumer Finances__ (SCF).  One particularly relevant example is feedback from the direct experience of financial advisors:  Many people appear to dislike the idea of running their wealth down to zero and then living pension-check to pension-check (which is what the traditional model says is optimal). The 'drawdown failure' has typically been patched up, in the academic literature, by adding a \`bequest motive' to the objectives of consumers.  But the available evidence finds that even childless people -- who presumably do not have much of a bequest motive -- do not draw down their wealth in ways consistent with the pure life cycle model (in which the only purpose of holding wealth is to finance your own future consumption). The model section of the paper advocates a direct and simple solution, which is to assume that people have an intrinsic desire to hold wealth which is distinct from the consequences those wealth holdings have for their ability to consume in the future.\footnote{See Carroll (2001) for an extended discussion of what those other motivations may be.} The main substantive/mathematical point of this paper (in the "Model Results" section) is to show that a model with \`wealth in the utility function' explains observed post-retirement behavior of both wealth-holding and portfolio choice at least as well as the traditional model with a standard bequest motive.

The thesis of this paper twofold.  The first is that when all of these elements are combined, a state-of-the-art mathematical optimization model can come reasonably close to explaining people's actual choices, given their actual beliefs. This provides an attractive resolution to the awkward fact that the financial industry's advice has, until now, had no underpinning but tradition. The resolution takes the satisfying form that perhaps financial advisors had a better idea all along what constituted good advice, and only now are the rigorous mathematical/computational models able to explain why.

# Literature Review

[](doi:10.3982/ecta16409)

[](doi:10.1257/000282802320189393)

# Model

## The Baseline Academic Model

### With No Bequest Motive

In each period, a consumer's utility depends on how much they consume. We assume that the utility function is of the standard Constant Relative Risk Aversion form:
\begin{align}
\uFunc(c) & = \frac{c^{1-\CRRA}}{1-\CRRA}
\end{align}
but of course the consumer is smart enough to realize that preserving some of their resources for the future is probably a good idea; this is why all wealth is not consumed immediately.

We follow tradition that consumer's financial circumstances are assumed to be measured by two variables. $\pLvl_{t}$ is the consumer's permanent income level (roughly, the income they would normally expect to receive), while $\mLvl_{t}$ is total market resources (the sum of financial assets and current income -- think of this as the pool of resources that can be immediately spent; \`money' in the colloquial sense of \`how much money does grandma have?').

The \`value' of having a given amount of market resources $\mLvl_{t}$ right now, and of knowing your current permanent income level to be $\pLvl_{t}$, is determined by the utility you will experience from consumption today, as well as the utility you expect to experience in the future. Any future period matters to you only to the extent that you expect to survive to that period. There are other reasons that the \`exchange rate' between current utility and future utility may not be one-for-one: For example, you may have some degree of present bias (which we denote by $\beth$ where $\beth < 1$ means that you are \`present-biased: You overweight your current self compared to your future self). An adjustment for household-size changes is also conventional in the literature, and is captured in our notation with an age-varying factor $\hat{\DiscFac}$.

In formal mathematical terms, the consumer's objective is to maximize present discounted utility from consumption over a life cycle that ends no later than date $T$ (often set to age 120):
\begin{equation}
  \pmb{\vFunc}_{t}(\mLvl_{t},\pLvl_{t})  =    \max_{\{\cFunc\}_{t}^{T}} ~ \uFunc(\cLvl_{t})+\Ex_{t}\left[\sum_{n=1}^{T-t} {\beth}^{n} \Alive_{t}^{t+n}\hat{\DiscFac}_{t}^{t+n} \uFunc(\cLvl_{t+n}) \right]   \label{eq:lifecyclemax}
\end{equation}


# Harvard Online Data Science Probability Course

## Section 1: Discrete Probability (Introduction)

### Theory
#### Introduction

The probability of an event is the proportion of times the event occurs when we repeat the experiment independently under the same conditions.

```
Pr(𝐴)=probability of event A
```

An event is defined as an outcome that can occur when when something happens by chance.

We can determine probabilities related to discrete variables (picking a red bead, choosing 48 Democrats and 52 Republicans from 100 likely voters) and continuous variables (height over 6 feet).

#### Monte Carlo simulations

Monte Carlo simulations model the probability of different outcomes by repeating a random process a large enough number of times that the results are similar to what would be observed if the process were repeated forever.

```
beads <- rep(c("red", "blue"), times = c(2,3))    # create an urn with 2 red, 3 blue
beads    # view beads object
sample(beads, 1)    # sample 1 bead at random

B <- 10000    # number of times to draw 1 bead
events <- replicate(B, sample(beads, 1))    # draw 1 bead, B times
tab <- table(events)    # make a table of outcome counts
tab    # view count table
prop.table(tab)    # view table of outcome proportions
```

#### Probability distributions

The probability distribution for a variable describes the probability of observing each possible outcome.

For discrete categorical variables, the probability distribution is defined by the proportions for each group.

#### Interdependence

Conditional probabilities compute the probability that an event occurs given information about dependent events. For example, the probability of drawing a second king given that the first draw is a king is:

```
Pr(Card 2 is a king∣Card 1 is a king)=3/51
```

If two events  𝐴  and  𝐵  are independent,  Pr(𝐴∣𝐵)=Pr(𝐴) .

To determine the probability of multiple events occurring, we use the multiplication rule.

##### Equations

The multiplication rule for independent events is:

```
Pr(𝐴 and 𝐵 and 𝐶)=Pr(𝐴)×Pr(𝐵)×Pr(𝐶)
```

The multiplication rule for dependent events considers the conditional probability of both events occurring:

```
Pr(𝐴 and 𝐵)=Pr(𝐴)×Pr(𝐵∣𝐴)
```

We can expand the multiplication rule for dependent events to more than 2 events:

```
Pr(𝐴 and 𝐵 and 𝐶)=Pr(𝐴)×Pr(𝐵∣𝐴)×Pr(𝐶∣𝐴 and 𝐵)
```

### Exercises (no-code)

#### Probability of cyan

One ball will be drawn at random from a box containing: 3 cyan balls, 5 magenta balls, and 7 yellow balls.

What is the probability that the ball will be cyan?

> Answer: cyan balls / all balls = cyan balls / (cyan balls + magenta balls + yellow balls) = 3 / (3 + 5 + 7) = 0.2 (20%)

#### Probability of not cyan

One ball will be drawn at random from a box containing: 3 cyan balls, 5 magenta balls, and 7 yellow balls.

What is the probability that the ball will *not* be cyan?

##### Solution 1 (direct)

> Answer: all non-cyan balls / all balls = (magenta balls + yellow balls) / (cyan balls + magenta balls + yellow balls) = (5 + 7) / (3 + 5 + 7) = 0.8 (20%)

##### Solution 2 (non-direct)

> Answer: Since we already know that the P(draw cyan ball) = 0.2, then ! P (draw cyan ball) = 1 - 0.2 = 0.8

#### Sampling without replacement

Instead of taking just one draw, consider taking two draws. You take the second draw without returning the first draw to the box. We call this sampling without replacement.

What is the probability that the first draw is cyan and that the second draw is not cyan?

> Answer: P (A and B) = P (A) × P (B|A) = (3 / 15) * (12 / 14) = 0.17

#### Sampling with replacement

Now repeat the experiment, but this time, after taking the first draw and recording the color, return it back to the box and shake the box. We call this sampling with replacement.

What is the probability that the first draw is cyan and that the second draw is not cyan?

> Answer: P (A and B) = P (A) × P (B|A) = (3 / 15) * (12 / 15) = 0.16

### Exercises (code)

#### Probability of cyan - generalized

One ball will be drawn at random from a box containing: 3 cyan balls, 5 magenta balls, and 7 yellow balls.

What is the probability that the ball will be cyan?

<blockquote>
Answer:

<code>cyan <- 3
magenta <- 5
yellow <- 7

p <- cyan / (cyan + magenta + yellow) # Assign a variable `p` as the probability of choosing a cyan ball from the box

print(p) # Print the variable `p` to the console
</code>
</blockquote>

#### Probability of not cyan - generalized

We defined the variable p as the probability of choosing a cyan ball from a box containing: 3 cyan balls, 5 magenta balls, and 7 yellow balls.

What is the probability that the ball you draw from the box will NOT be cyan?

<blockquote>
Answer:

<code>1-p
</code>
</blockquote>

#### Sampling without replacement - generalized

Instead of taking just one draw, consider taking two draws. You take the second draw without returning the first draw to the box. We call this sampling without replacement.

What is the probability that the first draw is cyan and that the second draw is not cyan?

<blockquote>
Answer:

<code>cyan <- 3
magenta <- 5
yellow <- 7

p_1 <- cyan / (cyan + magenta + yellow) # The variable `p_1` is the probability of choosing a cyan ball from the box on the first draw.

p_2 <- (magenta + yellow) / (cyan - 1 + magenta + yellow) # Assign a variable `p_2` as the probability of not choosing a cyan ball on the second draw without replacement.

p_2 * p_1 # Calculate the probability that the first draw is cyan and the second draw is not cyan using `p_1` and `p_2`.
</code>
</blockquote>

#### Sampling with replacement - generalized

Now repeat the experiment, but this time, after taking the first draw and recording the color, return it back to the box and shake the box. We call this sampling with replacement.

What is the probability that the first draw is cyan and that the second draw is not cyan?

<blockquote>
Answer:

<code>cyan <- 3
magenta <- 5
yellow <- 7

p_1 <- cyan / (cyan + magenta + yellow) # The variable 'p_1' is the probability of choosing a cyan ball from the box on the first draw.

p_2 = 1 - p_1 # Assign a variable 'p_2' as the probability of not choosing a cyan ball on the second draw with replacement.

p_1 * p_2 # Calculate the probability that the first draw is cyan and the second draw is not cyan using `p_1` and `p_2`.
</code>
</blockquote>

## Section 1: Discrete Probability (Combinations and Permutations)

### Theory

#### How Many Monte Carlo Experiments are Enough?

The larger the number of Monte Carlo replicates  𝐵 , the more accurate the estimate.

Determining the appropriate size for  𝐵  can require advanced statistics.
One practical approach is to try many sizes for  𝐵  and look for sizes that provide stable estimates.

##### Estimating a practical value of B

This code runs Monte Carlo simulations to estimate the probability of shared birthdays using several B values and plots the results. When B is large enough that the estimated probability stays stable, then we have selected a useful value of B.

```
B <- 10^seq(1, 5, len = 100)    # defines vector of many B values
compute_prob <- function(B, n = 22){    # function to run Monte Carlo simulation with each B
	same_day <- replicate(B, {
    	bdays <- sample(1:365, n, replace = TRUE)
        any(duplicated(bdays))
    })
    mean(same_day)
}

prob <- sapply(B, compute_prob)    # apply compute_prob to many values of B
plot(log10(B), prob, type = "l")    # plot a line graph of estimates
```

### Exercises

#### Independence

Imagine you draw two balls from a box containing colored balls. You either replace the first ball before you draw the second or you leave the first ball out of the box when you draw the second ball.

Under which situation are the two draws independent of one another?

Remember that two events A and B are independent if Pr(A and B)=Pr(A)P(B).

> Answer: You do replace the first ball before drawing the next.

#### Sampling with replacement

Say you’ve drawn 5 balls from the a box that has 3 cyan balls, 5 magenta balls, and 7 yellow balls, with replacement, and all have been yellow.

What is the probability that the next one is yellow?

> Answer: The probability of drawing a yellow ball with replacement refers to an independent event. Thus, P (draw yellow ball) = yellow balls / (cyan balls + magenta balls + yellow balls) = ~0.46

#### Rolling a die

If you roll a 6-sided die once, what is the probability of not seeing a 6? If you roll a 6-sided die six times, what is the probability of not seeing a 6 on any of those rolls?

<blockquote>
Answer:

<code>p_no6 <- 5 / 6 # Assign the variable 'p_no6' as the probability of not seeing a 6 on a single roll.

p_no6 ^ 6 # Calculate the probability of not seeing a 6 on six rolls using `p_no6`. Print your result to the console: do not assign it to a variable.
</code>
</blockquote>

#### Probability the Celtics win a game

Two teams, say the Celtics and the Cavs, are playing a seven game series. The Cavs are a better team and have a 60% chance of winning each game.

What is the probability that the Celtics win at least one game? Remember that the Celtics must win one of the first four games, or the series will be over!

<blockquote>
Answer:

<code>p_cavs_win4 <- 0.6 ^ 4 # Assign the variable `p_cavs_win4` as the probability that the Cavs will win the first four games of the series.

1 - p_cavs_win4 # Using the variable `p_cavs_win4`, calculate the probability that the Celtics win at least one game in the first four games of the series.
</code>
</blockquote>

#### Monte Carlo simulation for Celtics winning a game

Create a Monte Carlo simulation to confirm your answer to the previous problem by estimating how frequently the Celtics win at least 1 of 4 games. Use `B <- 10000` simulations.

The provided sample code simulates a single series of four random games, `simulated_games`.

<blockquote>
Answer:

<code>simulated_games <- sample(c("lose","win"), 4, replace = TRUE, prob = c(0.6, 0.4)) # This line of example code simulates four independent random games where the Celtics either lose or win. Copy this example code to use within the `replicate` function.

B <- 10000 # The variable 'B' specifies the number of times we want the simulation to run. Let's run the Monte Carlo simulation 10,000 times.

set.seed(1) # Use the `set.seed` function to make sure your answer matches the expected result after random sampling.

\#Create an object called `celtic_wins` that replicates two steps for B iterations: (1) generating a random four-game series `simulated_games` using the example code, then (2) determining whether the simulated series contains at least one win for the Celtics.
celtic_wins <- replicate(B, {
  simulated_games <- sample(c("lose","win"), 4, replace = TRUE, prob = c(0.6, 0.4))
  any("win" %in% simulated_games)
})

\#Calculate the frequency out of B iterations that the Celtics won at least one game. Print your answer to the console.
mean(celtic_wins)
</code>
</blockquote>


## Section 1: Addition Rule and Monty Hall

### Theory
#### Addition Rule

The addition rule states that the probability of event  𝐴  or event  𝐵  happening is the probability of event  𝐴  plus the probability of event  𝐵  minus the probability of both events  𝐴  and  𝐵  happening together.

```
Pr(𝐴 or 𝐵)=Pr(𝐴)+Pr(𝐵)−Pr(𝐴 and 𝐵)
```

Note that  (𝐴 or 𝐵)  is equivalent to  (𝐴|𝐵) .

#### Monty Hall (3 doors) problem

Monte Carlo simulations can be used to simulate random outcomes, which makes them useful when exploring ambiguous or less intuitive problems like the Monty Hall problem.
In the Monty Hall problem, contestants choose one of three doors that may contain a prize. Then, one of the doors that was not chosen by the contestant and does not contain a prize is revealed. The contestant can then choose whether to stick with the original choice or switch to the remaining unopened door.
Although it may seem intuitively like the contestant has a 1 in 2 chance of winning regardless of whether they stick or switch, Monte Carlo simulations demonstrate that the actual probability of winning is 1 in 3 with the stick strategy and 2 in 3 with the switch strategy.

### Exercises

#### The Cavs and the Warriors

Two teams, say the Cavs and the Warriors, are playing a seven game championship series. The first to win four games wins the series. The teams are equally good, so they each have a 50-50 chance of winning each game.

If the Cavs lose the first game, what is the probability that they win the series?


<blockquote>
Answer:

<code>\# Assign a variable 'n' as the number of remaining games.
n <- 6

\# Assign a variable `outcomes` as a vector of possible game outcomes, where 0 indicates a loss and 1 indicates a win for the Cavs.
outcomes <- c(0, 1)

\# Assign a variable `l` to a list of all possible outcomes in all remaining games. Use the `rep` function on `list(outcomes)` to create list of length `n`.
l <- rep(list(outcomes), n)

\# Create a data frame named 'possibilities' that contains all combinations of possible outcomes for the remaining games.
possibilities <- expand.grid(l)

\# Create a vector named 'results' that indicates whether each row in the data frame 'possibilities' contains enough wins for the Cavs to win the series.
results <- c(rowSums(possibilities) >= 4)

\# Calculate the proportion of 'results' in which the Cavs win the series. Print the outcome to the console.

mean(results)
</code>
</blockquote>

#### The Cavs and the Warriors - Monte Carlo

Confirm the results of the previous question with a Monte Carlo simulation to estimate the probability of the Cavs winning the series after losing the first game.

<blockquote>
Answer:

<code>\# The variable `B` specifies the number of times we want the simulation to run. Let's run the Monte Carlo simulation 10,000 times.
B <- 10000

\# Use the `set.seed` function to make sure your answer matches the expected result after random sampling.
set.seed(1)

\# Create an object called `results` that replicates for `B` iterations a simulated series and determines whether that series contains at least four wins for the Cavs.

results <- replicate(B, {
  outcomes <- sample(c(0,1), 6, replace=TRUE)
  sum(outcomes) >= 4
})

\# Calculate the frequency out of `B` iterations that the Cavs won at least four games in the remainder of the series. Print your answer to the console.

mean(results)
</code>
</blockquote>

#### A and B play a series - part 1

Two teams, A and B, are playing a seven series game series. Team A is better than team B and has a p>0.5 chance of winning each game.

Use the function sapply to compute the probability, call it Pr of winning for p <- seq(0.5, 0.95, 0.025).

<blockquote>
Answer:

<code>\# Let's assign the variable 'p' as the vector of probabilities that team A will win.
p <- seq(0.5, 0.95, 0.025)

\# Given a value 'p', the probability of winning the series for the underdog team B can be computed with the following function based on a Monte Carlo simulation:
prob_win <- function(p){
  B <- 10000
  result <- replicate(B, {
    b_win <- sample(c(1,0), 7, replace = TRUE, prob = c(1-p, p))
    sum(b_win)>=4
    })
  mean(result)
}

\# Apply the 'prob_win' function across the vector of probabilities that team A will win to determine the probability that team B will win. Call this object 'Pr'.
Pr <- sapply(p, prob_win)

\# Plot the probability 'p' on the x-axis and 'Pr' on the y-axis.

plot(p, Pr)
</code>
</blockquote>


#### A and B play a series - part 2

Repeat the previous exercise, but now keep the probability that team A wins fixed at p <- 0.75 and compute the probability for different series lengths. For example, wins in best of 1 game, 3 games, 5 games, and so on through a series that lasts 25 games.

<blockquote>
Answer:

<code>\# Given a value 'p', the probability of winning the series for the underdog team B can be computed with the following function based on a Monte Carlo simulation:
prob_win <- function(N, p=0.75){
      B <- 10000
      result <- replicate(B, {
        b_win <- sample(c(1,0), N, replace = TRUE, prob = c(1-p, p))
        sum(b_win)>=(N+1)/2
        })
      mean(result)
    }

\# Assign the variable 'N' as the vector of series lengths. Use only odd numbers ranging from 1 to 25 games.
N <- seq(1, 25, 2)

\# Apply the 'prob_win' function across the vector of series lengths to determine the probability that team B will win. Call this object `Pr`.
Pr <- sapply(N, prob_win)

\# Plot the number of games in the series 'N' on the x-axis and 'Pr' on the y-axis.

plot(N, Pr)
</code>
</blockquote>

## Section 1: Assessment

### Olympic running

#### How many different ways can the 3 medals be distributed across 8 runners?

> Answer: In this case, order matters. Therefore, the result is `nrow(permutations(n=8, r=3)) = 356`

#### How many different ways can the three medals be distributed among the 3 runners from Jamaica?

> Answer: Similarly, order matters but this time just among 3 runners. `nrow(permutations(n=3, r=3)) = 6`

#### What is the probability that all 3 medals are won by Jamaica?

> Answer: Using the multiplication rule for dependent events, P(A and B and C) = Pr(C)×Pr((A and B)|C) = Pr(C)×Pr(B|A and C)×Pr(A|C) = (3/8)×(2/7)×(1/6) = 0.017

#### Run a Monte Carlo simulation on this vector representing the countries of the 8 runners in this race:

<blockquote>
Answer:

<code>runners <- c("Jamaica", "Jamaica", "Jamaica", "USA", "Ecuador", "Netherlands", "France", "South Africa")

set.seed(1)

results <- replicate(10000, {
  winners <- sample(runners, 3)
  winners[winners=='Jamaica']
  length(winners[winners=='Jamaica']) == length(winners)
})

mean(results) # = 0.174
</code>
</blockquote>

### Restaurant management

Use the information below to answer the following five questions.

A restaurant manager wants to advertise that his lunch special offers enough choices to eat different meals every day of the year. He doesn't think his current special actually allows that number of choices, but wants to change his special if needed to allow at least 365 choices.

A meal at the restaurant includes 1 entree, 2 sides, and 1 drink. He currently offers a choice of 1 entree from a list of 6 options, a choice of 2 different sides from a list of 6 options, and a choice of 1 drink from a list of 2 options.

#### How many meal combinations are possible with the current menu?

<blockquote>
Asnwer:

Since the choices of entree (E), sides (S) and drinks (D) are independent of each other and order is irrelevant, the result (R) will be a combination of all E, S and D options.

E = 6

S = C(6, 2) = 15

D = 2

Therefore, R = 6×15×2 = 180
</blockquote>

#### The manager has one additional drink he could add to the special. How many combinations are possible if he expands his original special to 3 drink options?

<blockquote>
Answer:

Following the same logic:

E = 6

S = C(6,2) = 15

D = 3

Therefore, R = 6×15×3 = 270
</blockquote>

#### The manager decides to add the third drink but needs to expand the number of options. The manager would prefer not to change his menu further and wants to know if he can meet his goal by letting customers choose more sides. How many meal combinations are there if customers can choose from 6 entrees, 3 drinks, and select 3 sides from the current 6 options?

<blockquote>
Answer:

E = 6

S = C(6,3) = 20

D = 3

Therefore, R = 6×20×3 = 360
</blockquote>

#### The manager is concerned that customers may not want 3 sides with their meal. He is willing to increase the number of entree choices instead, but if he adds too many expensive options it could eat into profits. He wants to know how many entree choices he would have to offer in order to meet his goal.

- Write a function that takes a number of entree choices and returns the number of meal combinations possible given that number of entree options, 3 drink choices, and a selection of 2 sides from 6 options.

- Use sapply() to apply the function to entree option counts ranging from 1 to 12.

What is the minimum number of entree options required in order to generate more than 365 combinations

<blockquote>
Answer:

<code>number_of_options = function(n) {
  n\*15\*2
}

sapply(seq(1,12), number_of_options)

\# Results are: [1]  45  90 135 180 225 270 315 360 405 450 495 540
</code>

Based on the results, the minimum number of options guaranteeing more than 365 combinations is
9, when the combinations will be 405.
</blockquote>


#### The manager isn't sure he can afford to put that many entree choices on the lunch menu and thinks it would be cheaper for him to expand the number of sides. He wants to know how many sides he would have to offer to meet his goal of at least 365 combinations.

- Write a function that takes a number of side choices and returns the number of meal combinations possible given 6 entree choices, 3 drink choices, and a selection of 2 sides from the specified number of side choices.

- Use sapply() to apply the function to side counts ranging from 2 to 12.

What is the minimum number of side options required in order to generate more than 365 combinations?

<blockquote>
Answer:

<code>library('gtools')

number_of_options = function(n) {
  6 \* choose(n, 2) \* 3
}

sapply(seq(2,12), number_of_options)
\# Results are: [1]   18   54  108  180  270  378  504  648  810  990 1188
</code>

Based on the results, the minimum number of options guaranteeing more than 365 combinations is
7, when the combinations will be 378.
</blockquote>

### Esophageal cancer and alcohol/tobacco use, part 1

Case-control studies help determine whether certain exposures are associated with outcomes such as developing cancer. The built-in dataset esoph contains data from a case-control study in France comparing people with esophageal cancer (cases, counted in ncases) to people without esophageal cancer (controls, counted in ncontrols) that are carefully matched on a variety of demographic and medical characteristics. The study compares alcohol intake in grams per day (alcgp) and tobacco intake in grams per day (tobgp) across cases and controls grouped by age range (agegp).

The dataset is available in base R and can be called with the variable name esoph:
```
head(esoph)
```

You will be using this dataset to answer the following four multi-part questions (Questions 3-6).

You may wish to use the tidyverse package:
```
library(tidyverse)
```

The following three parts have you explore some basic characteristics of the dataset.

Each row contains one group of the experiment. Each group has a different combination of age, alcohol consumption, and tobacco consumption. The number of cancer cases and number of controls (individuals without cancer) are reported for each group.

#### How many groups are in the study?

<blockquote>
Answer: The number of rows in the esoph vector:

<code>nrow(esoph) \# 88
</code>
</blockquote>

#### How many cases are there?

Save this value as all_cases for later problems.

<blockquote>
Answer:

<code>all_cases <- sum(esoph[,'ncases'])

all_cases # 200
</code>
</blockquote>

#### How many controls are there?

Save this value as all_controls for later problems.

<blockquote>
Answer:

<code>all_controls <- sum(esoph[,'ncontrols'])

all_controls \# 975
</code>
</blockquote>

#### What is the probability that a subject in the highest alcohol consumption group is a cancer case?

<blockquote>
Answer:

<code>highest_alcohol_group <- esoph[esoph[,'alcgp'] == '120+',]

sum(highest_alcohol_group[,'ncases']) / (sum(highest_alcohol_group[,'ncases']) + sum(highest_alcohol_group[,'ncontrols']))
\# 0.4017857
</code>
</blockquote>

#### What is the probability that a subject in the lowest alcohol consumption group is a cancer case?

<blockquote>
Answer:

<code>lowest_alcohol_group <- esoph[esoph[,'alcgp'] == '0-39g/day',]

sum(lowest_alcohol_group[,'ncases']) / (sum(lowest_alcohol_group[,'ncases']) + sum(lowest_alcohol_group[,'ncontrols']))
\# 0.06531532
</code>
</blockquote>

#### Given that a person is a case, what is the probability that they smoke 10g or more a day?

<blockquote>
Answer:

<code>smoke_more_than_10 <- esoph[esoph[,'tobgp'] != '0-9g/day',]

sum(smoke_more_than_10[,'ncases']) / sum(esoph[,'ncases'])
\# 0.61
</code>
</blockquote>

#### Given that a person is a control, what is the probability that they smoke 10g or more a day?

<blockquote>
Answer:

<code>smoke_more_than_10 <- esoph[esoph[,'tobgp'] != '0-9g/day',]

sum(smoke_more_than_10[,'ncontrols']) / sum(esoph[,'ncontrols'])
\# 0.4615385
</code>
</blockquote>


### Esophageal cancer and alcohol/tobacco use, part 2

#### For cases, what is the probability of being in the highest alcohol group?

<blockquote>
Answer:

<code>highest_alcohol_group <- esoph[esoph[,'alcgp'] == '120+',]

sum(highest_alcohol_group[,'ncases']) / sum(esoph[,'ncases'])
\# 0.225
</code>
</blockquote>

#### For cases, what is the probability of being in the highest tobacco group?

<blockquote>
Answer:

<code>highest_tobacco_group <- esoph[esoph[,'tobgp'] == '30+',]

sum(highest_tobacco_group[,'ncases']) / sum(esoph[,'ncases'])
\# 0.155
</code>
</blockquote>

#### For cases, what is the probability of being in the highest alcohol group and the highest tobacco group?

<blockquote>
Answer:

<code>highest_tobacco_group <- esoph[esoph[,'tobgp'] == '30+',]

pr_a = sum(highest_tobacco_group[,'ncases']) / sum(esoph[,'ncases'])

highest_alcohol_among_highest_tobacco <- highest_tobacco_group[highest_tobacco_group[, 'alcgp'] == '120+',]

pr_a_and_b = sum(highest_alcohol_among_highest_tobacco[,'ncases']) / sum(esoph[,'ncases'])
\# 0.05
</code>
</blockquote>

#### For cases, what is the probability of being in the highest alcohol group or the highest tobacco group?

<blockquote>
Answer:

<code>highest_tobacco_group <- esoph[esoph[,'tobgp'] == '30+',]
highest_alcohol_group <- esoph[esoph[,'alcgp'] == '120+',]

pr_a = sum(highest_tobacco_group[,'ncases']) / sum(esoph[,'ncases'])
pr_b = sum(highest_alcohol_group[,'ncases']) / sum(esoph[,'ncases'])

highest_alcohol_among_highest_tobacco <- highest_tobacco_group[highest_tobacco_group[, 'alcgp'] == '120+',]
pr_a_and_b = sum(highest_alcohol_among_highest_tobacco[,'ncases']) / sum(esoph[,'ncases'])

pr_a+pr_b - pr_a_and_b
\# 0.33
</code>
</blockquote>

#### For controls, what is the probability of being in the highest alcohol group?

<blockquote>
Answer:

highest_alcohol_group <- esoph[esoph[,'alcgp'] == '120+',]

sum(highest_alcohol_group[,'ncontrols']) / sum(esoph[,'ncontrols'])
\# 0.06871795
</code>
</blockquote>

#### How many times more likely are cases than controls to be in the highest alcohol group?

<blockquote>
Answer:

<code>highest_alcohol_group <- esoph[esoph[,'alcgp'] == '120+',]

ncontrols_highest_alcohol <- sum(highest_alcohol_group[,'ncontrols']) / sum(esoph[,'ncontrols'])
ncases_highest_alcohol <- sum(highest_alcohol_group[,'ncases']) / sum(esoph[,'ncases'])

ncases_highest_alcohol / ncontrols_highest_alcohol
\ #3.274254
</code>
</blockquote>

#### For controls, what is the probability of being in the highest tobacco group?

<blockquote>
Answer:

<code>highest_tobacco_group <- esoph[esoph[,'tobgp'] == '30+',]

highest_tobacco_group_pr <- sum(highest_tobacco_group[,'ncontrols']) / sum(esoph[,'ncontrols'])

highest_tobacco_group_pr
\# 0.08410256
</code>
</blockquote>

#### For controls, what is the probability of being in the highest alcohol group and the highest tobacco group?

<blockquote>
Answer:

<code>highest_tobacco_group <- esoph[esoph[,'tobgp'] == '30+',]

pr_a = sum(highest_tobacco_group[,'ncontrols']) / sum(esoph[,'ncontrols'])

highest_alcohol_among_highest_tobacco <- highest_tobacco_group[highest_tobacco_group[, 'alcgp'] == '120+',]

pr_a_and_b = sum(highest_alcohol_among_highest_tobacco[,'ncontrols']) / sum(esoph[,'ncontrols'])

pr_a_and_b
\# 0.01333333
</code>
</blockquote>

#### For controls, what is the probability of being in the highest alcohol group or the highest tobacco group?

<blockquote>
Answer:

<code>highest_tobacco_group <- esoph[esoph[,'tobgp'] == '30+',]
highest_alcohol_group <- esoph[esoph[,'alcgp'] == '120+',]

pr_a = sum(highest_tobacco_group[,'ncontrols']) / sum(esoph[,'ncontrols'])
pr_b = sum(highest_alcohol_group[,'ncontrols']) / sum(esoph[,'ncontrols'])

highest_alcohol_among_highest_tobacco <- highest_tobacco_group[highest_tobacco_group[, 'alcgp'] == '120+',]
pr_a_and_b = sum(highest_alcohol_among_highest_tobacco[,'ncontrols']) / sum(esoph[,'ncontrols'])

pr_a+pr_b - pr_a_and_b
\# 0.1394872
</code>
</blockquote>


#### How many times more likely are cases than controls to be in the highest alcohol group or the highest tobacco group?

<blockquote>
Answer:

<code>highest_tobacco_group <- esoph[esoph[,'tobgp'] == '30+',]
highest_alcohol_group <- esoph[esoph[,'alcgp'] == '120+',]

pr_a_controls = sum(highest_tobacco_group[,'ncontrols']) / sum(esoph[,'ncontrols'])
pr_b_controls = sum(highest_alcohol_group[,'ncontrols']) / sum(esoph[,'ncontrols'])

pr_a_cases = sum(highest_tobacco_group[,'ncases']) / sum(esoph[,'ncases'])
pr_b_cases = sum(highest_alcohol_group[,'ncases']) / sum(esoph[,'ncases'])

highest_alcohol_among_highest_tobacco <- highest_tobacco_group[highest_tobacco_group[, 'alcgp'] == '120+',]

pr_a_and_b_controls = sum(highest_alcohol_among_highest_tobacco[,'ncontrols']) / sum(esoph[,'ncontrols'])
pr_a_and_b_cases = sum(highest_alcohol_among_highest_tobacco[,'ncases']) / sum(esoph[,'ncases'])


pr_cases = pr_a_cases + pr_b_cases - pr_a_and_b_cases
pr_controls = pr_a_controls + pr_b_controls - pr_a_and_b_controls

pr_cases / pr_controls
\# 2.365809
</code>
</blockquote>

## Section 2: Continuous probability

### Theory

The cumulative distribution function (CDF) is a distribution function for continuous data `𝑥` that reports the proportion of the data below `𝑎`  for all values of `𝑎` :

```
𝐹(𝑎)=Pr(𝑥≤𝑎)

```

The CDF is the probability distribution function for continuous variables. For example, to determine the probability that a male student is taller than 70.5 inches given a vector of male heights `𝑥` , we can use the CDF:

```
Pr(𝑥>70.5)=1−Pr(𝑥≤70.5)=1−𝐹(70.5)
```

The probability that an observation is in between two values `𝑎,𝑏`  is `𝐹(𝑏)−𝐹(𝑎)`.

The probability of a single value is not defined for a continuous distribution.

The quantity with the most similar interpretation to the probability of a single value is the probability density function  𝑓(𝑥) .

The probability density  𝑓(𝑥)  is defined such that the integral of  𝑓(𝑥)  over a range gives the CDF of that range.

```
𝐹(𝑎)=Pr(𝑋≤𝑎)=∫𝑎−∞𝑓(𝑥)𝑑𝑥
```

### Exercises

#### Assume the distribution of female heights is approximated by a normal distribution with a mean of 64 inches and a standard deviation of 3 inches. If we pick a female at random, what is the probability that she is 5 feet or shorter?

<blockquote>
Answer:

<code>\# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

\# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

\# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is shorter than 5 feet. Print this value to the console.

pnorm(5*12, female_avg, female_sd)
\# 0.09121122
</code>
</blockquote>


#### Assume the distribution of female heights is approximated by a normal distribution with a mean of 64 inches and a standard deviation of 3 inches. If we pick a female at random, what is the probability that she is 6 feet or taller?

<blockquote>
Answer:

<code>\# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

\# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

\# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is 6 feet or taller. Print this value to the console.
1 - pnorm(6*12, female_avg, female_sd)
\# 0.003830381
</code>
</blockquote>


#### Assume the distribution of female heights is approximated by a normal distribution with a mean of 64 inches and a standard deviation of 3 inches. If we pick a female at random, what is the probability that she is between 61 and 67 inches?

<blockquote>
Answer:

<code>\# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

\# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

\# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.

pnorm(67, female_avg, female_sd) - pnorm(61, female_avg, female_sd)
\# 0.6826895
</code>
</blockquote>

#### Repeat the previous exercise, but convert everything to centimeters. That is, multiply every height, including the standard deviation, by 2.54. What is the answer now?

<blockquote>
Answer:

<code>\# Assign a variable 'female_avg' as the average female height. Convert this value to centimeters.
female_avg <- 64*2.54

\# Assign a variable 'female_sd' as the standard deviation for female heights. Convert this value to centimeters.
female_sd <- 3*2.54

\# Using variables 'female_avg' and 'female_sd', calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.

pnorm(67*2.54, female_avg, female_sd) - pnorm(61*2.54, female_avg, female_sd)
\# 0.6826895
</code>
</blockquote>

#### Compute the probability that the height of a randomly chosen female is within 1 SD from the average height.

<blockquote>
Answer:

<code>\# Assign a variable 'female_avg' as the average female height.
female_avg <- 64

\# Assign a variable 'female_sd' as the standard deviation for female heights.
female_sd <- 3

\# To a variable named 'taller', assign the value of a height that is one SD taller than average.
taller <- female_avg + female_sd

\# To a variable named 'shorter', assign the value of a height that is one SD shorter than average.
shorter <- female_avg - female_sd

\# Calculate the probability that a randomly selected female is between the desired height range. Print this value to the console.
pnorm(taller, female_avg, female_sd) - pnorm(shorter, female_avg, female_sd)
\# 0.6826895
</code>
</blockquote>

#### Imagine the distribution of male adults is approximately normal with an average of 69 inches and a standard deviation of 3 inches. How tall is a male in the 99th percentile?

<blockquote>
Answer:

<code>\# Assign a variable 'male_avg' as the average male height.
male_avg <- 69

\# Assign a variable 'male_sd' as the standard deviation for male heights.
male_sd <- 3

\# Determine the height of a man in the 99th percentile of the distribution.
qnorm(0.99, male_avg, male_sd)
</code>
</blockquote>

#### The distribution of IQ scores is approximately normally distributed. The average is 100 and the standard deviation is 15. Suppose you want to know the distribution of the person with the highest IQ in your school district, where 10,000 people are born each year. Generate 10,000 IQ scores 1,000 times using a Monte Carlo simulation. Make a histogram of the highest IQ scores.

<blockquote>
Answer:

<code>\# The variable `B` specifies the number of times we want the simulation to run.
B <- 1000

\# Use the `set.seed` function to make sure your answer matches the expected result after random number generation.
set.seed(1)

\# Create an object called `highestIQ` that contains the highest IQ score from each random distribution of 10,000 people.
dist_values <- 10000
avg_iq <- 100
iq_sd <- 15
highestIQ <- replicate(B, {
  iqs <- rnorm(10000, avg_iq, iq_sd)
  max(iqs)
})

\# Make a histogram of the highest IQ scores.
\# plot distribution of simulated_heights
hist(highestIQ)
</code>
</blockquote>

## Section 2: Assessment

### ACT scores part 1

The ACT is a standardized college admissions test used in the United States. The four multi-part questions in this assessment all involve simulating some ACT test scores and answering probability questions about them.

For the three year period 2016-2018, ACT standardized test scores were approximately normally distributed with a mean of 20.9 and standard deviation of 5.7. (Real ACT scores are integers between 1 and 36, but we will ignore this detail and use continuous values instead.)

First we'll simulate an ACT test score dataset and answer some questions about it.

Set the seed to 16, then use rnorm() to generate a normal distribution of 10000 tests with a mean of 20.9 and standard deviation of 5.7. Save these values as act_scores. You'll be using this dataset throughout these four multi-part questions.

#### What is the mean of act_scores?

<blockquote>
Answer:

<code>set.seed(16)

act_scores <- rnorm(10000, 20.9, 5.7)

mean(act_scores)
\# 20.84012
</code>
</blockquote>

#### What is the standard deviation of act_scores?

<blockquote>
Answer:

<code>set.seed(16)

act_scores <- rnorm(10000, 20.9, 5.7)

sd(act_scores)
\# 5.675237
</code>
</blockquote>

#### A perfect score is 36 or greater (the maximum reported score is 36). In act_scores, how many perfect scores are there out of 10,000 simulated tests?

<blockquote>
Answer:

<code>set.seed(16)

act_scores <- rnorm(10000, 20.9, 5.7)
act_scores

length(which(act_scores >= 36))
\# 41
</code>
</blockquote>

#### In act_scores, what is the probability of an ACT score greater than 30?

<blockquote>
Answer:

<code>set.seed(16)

act_scores <- rnorm(10000, 20.9, 5.7)

length(which(act_scores >= 30)) / length(act_scores)
\# 0.0527
</code>
</blockquote>

#### In act_scores, what is the probability of an ACT score less than or equal to 10?

<blockquote>
Answer:

<code>set.seed(16)

act_scores <- rnorm(10000, 20.9, 5.7)

length(which(act_scores <= 10)) / length(act_scores)
\# 0.0282
</code>
</blockquote>

### Set x equal to the sequence of integers 1 to 36. Use dnorm to determine the value of the probability density function over x given a mean of 20.9 and standard deviation of 5.7; save the result as f_x. Plot x against f_x. How does the plot look like?

<blockquote>
Answer:

<code>x <- seq(1, 36)

f_x <- dnorm(x, 20.9, 5.7)

plot(x, f_x)
</code>

<img src="/section_2_plot_1.png" alt="Plot image 1" />
</blockquote>

### ACT scores part 2

In this 3-part question, you will convert raw ACT scores to Z-scores and answer some questions about them.

Convert act_scores to Z-scores. Recall from Data Visualization (the second course in this series) that to standardize values (convert values into Z-scores, that is, values distributed with a mean of 0 and standard deviation of 1), you must subtract the mean and then divide by the standard deviation. Use the mean and standard deviation of act_scores, not the original values used to generate random test scores.

#### What is the probability of a Z-score greater than 2 (2 standard deviations above the mean)?

<blockquote>
Answer:

<code>set.seed(16)

act_scores <- rnorm(10000, 20.9, 5.7)

z_scores = (act_scores - mean(act_scores)) / sd(act_scores)

length(which(z_scores > 2)) / length(z_scores)
\# 0.0233
</code>
</blockquote>

#### What ACT score value corresponds to 2 standard deviations above the mean (Z = 2)?

<blockquote>
Answer:

<code>set.seed(16)

act_scores <- rnorm(10000, 20.9, 5.7)

mean(act_scores)+sd(act_scores)\*2
\# 32.1906
</code>
</blockquote>

#### A Z-score of 2 corresponds roughly to the 97.5th percentile. Use qnorm() to determine the 97.5th percentile of normally distributed data with the mean and standard deviation observed in act_scores. What is the 97.5th percentile of act_scores?

<blockquote>
Answer:

<code>set.seet(16)

qnorm(0.975, 20.9, 5.7)
\# 32.07179
</code>
</blockquote>

#### What is the minimum integer score such that the probability of that score or lower is at least .95?

<blockquote>
Answer:

<code>set.seed(16)

act_scores <- rnorm(10000, 20.9, 5.7)

ceiling(qnorm(0.95, mean(act_scores), sd(act_scores)))
\# 31
</code>
</blockquote>

#### Use qnorm() to determine the expected 95th percentile, the value for which the probability of receiving that score or lower is 0.95, given a mean score of 20.9 and standard deviation of 5.7. What is the expected 95th percentile of ACT scores?

<blockquote>
Answer:

<code>set.seed(16)

act_scores <- rnorm(10000, 20.9, 5.7)

qnorm(0.95, 20.9, 5.7)
\# 30.27567
</code>
</blockquote>

#### As discussed in the Data Visualization course, we can use quantile() to determine sample quantiles from the data. Make a vector containing the quantiles for p <- seq(0.01, 0.99, 0.01), the 1st through 99th percentiles of the act_scores data. Save these as sample_quantiles. In what percentile is a score of 26?


<blockquote>
Answer:

<code>set.seed(16)

act_scores <- rnorm(10000, 20.9, 5.7)

p <- seq(0.01, 0.99, 0.01)

sample_quantiles <- quantile(act_scores, p)

sample_quantiles
\# 82
</code>
</blockquote>


#### Make a corresponding set of theoretical quantiles using qnorm() over the interval p <- seq(0.01, 0.99, 0.01) with mean 20.9 and standard deviation 5.7. Save these as theoretical_quantiles. Make a QQ-plot graphing sample_quantiles on the y-axis versus theoretical_quantiles on the x-axis. What does the graph look like?

<blockquote>
Answer:

<code>set.seed(16)

act_scores <- rnorm(10000, 20.9, 5.7)

p <- seq(0.01, 0.99, 0.01)

sample_quantiles <- quantile(act_scores, p)

theoretical_quantiles <- quantile(qnorm(p, 20.9, 6.7), p)

qqplot(theoretical_quantiles, sample_quantiles)
</code>

<img src="/section_2_plot_2.png" alt="Plot image 2" />
</blockquote>

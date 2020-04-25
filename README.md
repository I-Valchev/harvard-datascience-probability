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

### Addition Rule

The addition rule states that the probability of event  𝐴  or event  𝐵  happening is the probability of event  𝐴  plus the probability of event  𝐵  minus the probability of both events  𝐴  and  𝐵  happening together.

```
Pr(𝐴 or 𝐵)=Pr(𝐴)+Pr(𝐵)−Pr(𝐴 and 𝐵)
```

Note that  (𝐴 or 𝐵)  is equivalent to  (𝐴|𝐵) .

# Harvard Online Data Science Probability Course

## Section 1: Discrete Probability

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

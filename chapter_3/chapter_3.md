### Solution 3.1

#### Example 1: Precision Farming

State: Current soil moisture level, weather forecast, crop growth stage, and water availability.

Action: Irrigate, fertilize, spray, or do nothing.

Reward: Increase in crop yield.

#### Example 2: Stock Portfolio Management

State: Current stock price, market sentiment, and available capital.

Action: Buy stock, sell stock, hold, reallocate into bonds.

Reward: Increase in portfolio value.

#### Example 3: Basketball Game Strategy

State: Current score difference, time left in game, player stamina levels, foul count.

Action: Attempt 2-point shot, attempt 3-point shot, pass, dribble, or defend.

Reward: Increase in score.

<br>

### Solution 3.2

- **Partial Observability**: In many real world tasks, it is not possible to know the exact state of the environment. For example, in autonomous driving, the agent cannot observe the intentions of other drivers or hidden obstacles. MDPs assume full observability, which is often unrealistic.

- **Markov Property Violation**: MDPs assume that the future depends only on the current state (Markov property). However, in many real world tasks, the future depends on the entire history of states and actions. For instance, in medical diagnosis, a patient's current symptoms alone may not be sufficient - the sequence of how symptoms developed over time is crucial for proper treatment decisions.

- **Non-Stationarity**: MDPs assume that the environment is stationary, meaning the transition probabilities and reward function remain constant over time. However, in many real world tasks, the environment is non-stationary. For example, in financial markets, the underlying dynamics change due to economic conditions, regulatory changes, or market sentiment shifts.

<br>

### Solution 3.3

If you go too detailed, the problem becomes too complex.

If you go too high-level, you lose important details, necessary for the agent to make decisions.

Therefore, a good choice is where the agent's actions clearly affect the outcomes and the problem is not too complicated to learn from.

In short: It’s not free choice — it’s about choosing the level that makes the learning and decision-making practical.

<br>

### Solution 3.4

**Transition Probabilities p(s',r | s,a)**:

| Current State (s) | Action (a) | Next State (s') |  Reward (r)  | Probability |
| :---------------: | :--------: | :-------------: | :----------: | :---------: |
|       high        |   search   |      high       | $r_{search}$ |      α      |
|       high        |   search   |       low       | $r_{search}$ |     1-α     |
|        low        |   search   |       low       | $r_{search}$ |      β      |
|        low        |   search   |      high       |      -3      |     1-β     |
|       high        |    wait    |      high       |  $r_{wait}$  |      1      |
|        low        |    wait    |       low       |  $r_{wait}$  |      1      |
|        low        |  recharge  |      high       |      0       |      1      |

<br>

### Solution 3.5

For the continuing case, the equation 3.3 will be modified to:

$$
\sum_{s' \in \mathcal{S}^{+}} \sum_{r \in \mathcal{R}} p(s', r \mid s, a) = 1, \qquad \forall s \in \mathcal{S}, \; a \in \mathcal{A}(s),
$$

where, $\mathcal{S}^{+} = \mathcal{S} \cup \{\text{terminal}\}$

<br>

### Solution 3.6

In the episodic case, if failure occurs after $K$ steps from time $t$, then the return would be

$$
G_t = -\gamma^{K-1}
$$

However, in the continuing case, the return includes the discounted future rewards for all the future failures as well, not just the immediate failure.

Then if $K_1$ is the first failure from time $t$, $K_2$ is the second failure from time $t$, and so on, the return would be

$$
G_t = -\gamma^{K_1-1} - \gamma^{K_2-1} - ... - \gamma^{K_n-1}
$$

<br>

### Solution 3.7

Since we are not discounting the reward, the agent has no incentive to take the shortest route to the goal. Whether it follows the optimal path or wanders randomly before eventually reaching the goal, it still receives the same reward of +1.

To address this, we should introduce reward discounting, so that rewards received sooner are valued more highly. This will encourage the agent to reach the goal as quickly as possible.

<br>

### Solution 3.8

$$
G_5 = 0
$$

$$
G_4 = R_5 + \gamma G_5 = 2 + 0.5(0) = 2
$$

$$
G_3 = R_4 + \gamma G_4 = 3 + 0.5(2) = 4
$$

$$
G_2 = R_3 + \gamma G_3 = 6 + 0.5(4) = 8
$$

$$
G_1 = R_2 + \gamma G_2 = 2 + 0.5(8) = 6
$$

$$
G_0 = R_1 + \gamma G_1 = -1 + 0.5(6) = 2
$$

<br>

### Solution 3.9

$$
G_1 = R_2 + \gamma R_3 + \gamma^2 R_4 + ... + \gamma^n R_{n+1}
$$

$$
= 7 + 0.9(7) + 0.9^2(7) + ... + 0.9^n(7)
$$

This is a geometric series, so we can use the formula for the sum of a geometric series to get:

$$
G_1 = \frac{a}{1 - \gamma} = \frac{7}{1 - 0.9} = 70
$$

Now,

$$
G_0 = R_1 + \gamma G_1 = 2 + 0.9(70) = 65
$$

<br>

### Solution 3.10

Let the sum of the geometric series be $S$.

$$
S = 1 + \gamma + \gamma^2 + ...
$$

Multiplying both sides by $\gamma$, we get:

$$
\gamma S = \gamma + \gamma^2 + \gamma^3 + ...
$$

Subtracting the first equation from the second, we get:

$$
S - \gamma S = (1 + \gamma + \gamma^2 + ...) - (\gamma + \gamma^2 + \gamma^3 + ...)
$$

On the right hand side, all terms cancel except the first 1, leaving us with:

$$
S(1 - \gamma) = 1
$$

$$
S = \frac{1}{1 - \gamma}
$$

<br>

### Solution 3.11

$$
\mathbb{E}_\pi\!\left[ R_{t+1} \mid S_t = s \right]
= \sum_{a} \pi(a \mid s) \sum_{s',\,r} r \cdot p(s', r \mid s, a)
$$

<br>

### Solution 3.12

$$
v_\pi(s) = \sum_{a} \pi(a \mid s) \, q_\pi(s,a)
$$

<br>

### Solution 3.13

$$
q_\pi(s,a) = \sum_{s',\,r} p(s', r \mid s,a) \left[ r + \gamma \, v_\pi(s') \right]
$$

<br>

### Solution 3.14

$$
v_\pi(s) = \sum_a \pi(a \mid s) \sum_{s', r} p(s', r \mid s, a) \left[ r + \gamma v_\pi(s') \right]
$$

Since in our case, the transition probabilities are deterministic, we can simplify the equation to:

$$
v_\pi(s) = \sum_a \pi(a \mid s) \left[ r + \gamma v_\pi(s') \right]
$$

$$
= \sum_{a} \tfrac{1}{4} \Big( 0 + \gamma \, v_\pi(s') \Big)
$$

$$
= 0.9 \cdot \frac{1}{4} \cdot (2.3 + 0.4 - 0.4 + 0.7) = 0.675
$$

Approximating it to the nearest tenth, we get $\approx 0.7$, and hence this equation holds

<br>

### Solution 3.15

$$
v_\pi(s) = \mathbb{E}_\pi \!\left[ \sum_{t=0}^\infty \gamma^t R_{t+1} \right]
$$

Adding a constant $c$ to each reward, we get:

$$
v'_\pi(s) = \mathbb{E}_\pi \!\left[ \sum_{t=0}^\infty \gamma^t (R_{t+1} + c) \right]
$$

$$
= \mathbb{E}_\pi \!\left[ \sum_{t=0}^\infty \gamma^t (R_{t+1} + c) \right]
$$

$$
= \mathbb{E}_\pi \!\left[ \sum_{t=0}^\infty \gamma^t (R_{t+1}) \right] + c \sum_{t=0}^\infty \gamma^t
$$

$$
= v_\pi(s) + \frac{c}{1 - \gamma}
$$

Therefore, adding a constant $c$ to all rewards shifts every state value by the same amount, which does not change the relative ordering of the states. Thus, the signs of the rewards are not important, only the intervals between them are important.

$$
v_c = \frac{c}{1 - \gamma}
$$

<br>

### Solution 3.16

In an episodic task, adding a constant $c$ to all rewards does not shift the values of the states by the same constant. Instead, the shift is dependent on the length of the episode.

$$
v'_\pi(s) = v_\pi(s) +  c \sum_{t=0}^{T-1} \gamma^t
$$

$$
= v_\pi(s) + c \frac{1 - \gamma^T}{1 - \gamma}
$$

Now, we can no longer conclude that the signs of the rewards are not important.

Example: Maze with reward $-1$ per step and $0$ at the goal prefers the shorter path. However, adding a constant $c = 1$ to all rewards, we now have a reward of $0$ per step and $+1$ at the goal. Now, any agent that reaches the goal will get the same reward and we no longer encourage the agent to take the shorter path.

<br>

### Solution 3.17

$$
q_\pi(s,a) = \mathbb{E}_\pi\!\left[\,R_{t+1} + \gamma G_{t+1} \mid S_t=s, A_t=a\right]
$$

$$
= \sum_{s',r} p(s',r \mid s,a) \Big[\, r + \gamma v_\pi(s') \Big]
$$

$$
= \sum_{s',r} p(s',r \mid s,a) \Big[\, r + \gamma \sum_{a'} \pi(a' \mid s') q_\pi(s',a') \Big]
$$

<br>

### Solution 3.18

We can write the equation in the following two forms:

1. Expectation form:

$$
v_\pi(s) = \mathbb{E}_{a \sim \pi(\cdot \mid s)} \! \left[ q_\pi(s,a) \right]
$$

2. Expanded form:

$$
v_\pi(s) = \sum_{a \in \mathcal{A}} \pi(a \mid s) \, q_\pi(s,a)
$$

<br>

### Solution 3.19

We can write the equation in the following two forms:

1. Expectation form:

$$
q_\pi(s,a) = \mathbb{E}_\pi\!\left[\,R_{t+1} + \gamma v_\pi(S_{t+1}) \mid S_t=s, A_t=a\,\right]
$$

2. Expanded form:

$$
q_\pi(s,a) = \sum_{s',r} p(s',r \mid s,a) \Big[\, r + \gamma v_\pi(s') \Big]
$$

<br>

### Solution 3.20

If the ball is on the green, we can use the putter and reach the hole in $1$ stroke.

$$
v^*(s) = -1
$$

If it is a little further away from the green, we can use a driver to land on the green followed by a putter to reach the hole in a total of $2$ strokes.

$$
v^*(s) = -2
$$

If it is even further away from the green, we can use the driver twice to land on the green followed by a putter to reach the hole in a total of $3$ strokes.

$$
v^*(s) = -3
$$

<br>

### Solution 3.21

The first action should be to use a putter, followed by the optimal action from the new state. This can be written mathematically as:

$$
q^*(s,putter) = \mathbb{E}[R_{t+1} + \gamma v^*(S_{t+1}) \mid S_t=s, A_t=putter]
$$

If the ball is on the green, then our first action lands us in the hole.

$$
q^*(s,putter) = -1
$$

If the ball is a little further away from the green, then our first action lands us on the green, followed by a putter to reach the hole in a total of $2$ strokes.

$$
q^*(s,putter) = -2
$$

If the ball is further away from the green, then our first action moves us closer to the green. This is followed by a driver to land us on the green, followed by a putter to reach the hole in a total of $3$ strokes.

$$
q^*(s,putter) = -3
$$

If the ball is even further away from the green, then our first action moves us closer to the green. This is followed by driver used twice to land us on the green, followed by a putter to reach the hole in a total of $4$ strokes.

$$
q^*(s,putter) = -4
$$

If the ball is in the sand, then our first action keeps us in the sand. This is followed by using a driver and landing on the green, and then using a putter to reach the hole. A total of $3$ strokes.

$$
q^*(s,putter) = -3
$$

<br>

### Solution 3.22

If $\gamma = 0$ then only the immediate reward is considered. The reward for taking the left action is $+1$, while the reward for taking the right action is $0$. So the optimal policy is to take the left action.

For the other two cases, following $\pi_{left}$, our value function will be:

$$
V_{left}(s) = 1 + \gamma^2 + \gamma^4 + ... = \frac{1}{1 - \gamma^2}
$$

And following $\pi_{right}$, our value function will be:

$$
V_{right}(s) = 2\gamma + 2\gamma^3 + 2\gamma^5 + ... = \frac{2\gamma}{1 - \gamma^2}
$$

For $\gamma = 0.9$,

$$
V_{left}(s) = \frac{1}{1 - 0.9^2} = 5.26
$$

$$
V_{right}(s) = \frac{2\cdot 0.9}{1 - 0.9^2} = 9.47
$$

Therefore, following $\pi_{right}$ is optimal.

For $\gamma = 0.5$,

$$
V_{left}(s) = \frac{1}{1 - 0.5^2} = 1.33
$$

$$
V_{right}(s) = \frac{2\cdot 0.5}{1 - 0.5^2} = 1.33
$$

Therefore, we can follow either action as both are optimal.

<br>

### Solution 3.23

Since

$$
q^{*}(s, a) = \sum_{s'} p(s' \mid s,a) \Big[\, r(s, a, s') + \gamma \, \max_{a'} q^{*}(s', a') \Big]
$$

Therefore,

$$
q^*(\text{high}, \text{search})     = \alpha \left[ r_{\text{search}} + \gamma \max_{a'} q^*(\text{high}, a') \right]
+ (1-\alpha) \left[ r_{\text{search}} + \gamma \max_{a'} q^*(\text{low}, a') \right]
$$

$$
q^*(\text{low}, \text{search}) = \beta \left[ r_{\text{search}} + \gamma \max_{a'} q^*(\text{high}, a') \right]
+ (1-\beta) \left[ -3 + \gamma \max_{a'} q^*(\text{low}, a') \right]
$$

$$
q^*(\text{high}, \text{wait}) = r_{\text{wait}} + \gamma \max_{a'} q^*(\text{high}, a')
$$

$$
q^*(\text{low}, \text{wait}) = r_{\text{wait}} + \gamma \max_{a'} q^*(\text{low}, a')
$$

$$
q^*(\text{low}, \text{recharge}) = \gamma \max_{a'} q^*(\text{high}, a')
$$

<br>

### Solution 3.24

$$
v^*(s) = \mathbb{E}[r + \gamma v^*(s')]
$$

Since we always move to $A'$ no matter what action we take.

$$
v^*(s) = 10 + 0.9(16) = 24.400
$$

<br>

### Solution 3.25

$$
v^*(s) = \max_a q^*(s,a)
$$

<br>

### Solution 3.26

$$
q^*(s,a) = \sum_{s',r} p(s',r \mid s,a) \Big[\, r + \gamma v^*(s') \Big]
$$

<br>

### Solution 3.27

$$
\pi^*(s) = \arg\max_a q^*(s,a)
$$

<br>

### Solution 3.28

$$
\pi^*(s) = \arg\max_a \sum_{s',r} p(s',r \mid s,a) \Big[\, r + \gamma v^*(s') \Big]
$$

<br>

### Solution 3.29

Firstly, note that

$$
p(s' \mid s,a) = \sum_{r} p(s',r \mid s,a)
$$

and

$$
r(s, a) = \sum_{r} r \cdot p(s',r \mid s,a)
$$

For $v_{\pi}$,

$$
v_{\pi}(s) = \sum_{a} \pi(a \mid s) \sum_{s',r} p(s',r \mid s,a) \Big[\, r + \gamma v_{\pi}(s') \Big]
$$

$$
= \sum_{a} \pi(a \mid s) \Big[ \sum_{s',r} r \cdot p(s',r \mid s,a) + \gamma \sum_{s',r} p(s',r \mid s,a) \cdot v_{\pi}(s') \Big]
$$

$$
= \sum_{a} \pi(a \mid s) \Big[ \sum_{s',r} r \cdot p(s',r \mid s,a) + \gamma \sum_{s'} \Big(\sum_{r} p(s',r \mid s,a)\Big) \cdot v_{\pi}(s') \Big]
$$

$$
= \sum_{a} \pi(a \mid s) \Big[ r(s, a) + \gamma \sum_{s'} p(s' \mid s,a) \cdot v_{\pi}(s') \Big]
$$

For $q_{\pi}$,

$$
q_{\pi}(s,a) = \sum_{s',r} p(s',r \mid s,a) \Big[\, r + \gamma v_{\pi}(s') \Big]
$$

$$
= r(s, a) + \gamma \sum_{s'} p(s' \mid s,a) \cdot v_{\pi}(s')
$$

$$
= r(s, a) + \gamma \sum_{s'} p(s' \mid s,a) \cdot \sum_{a'} \pi(a' \mid s') \cdot q_{\pi}(s',a')
$$

For $v^*$,

$$
v^*(s) = \max_a \Big[r(s, a) + \gamma \sum_{s'} p(s' \mid s,a) \cdot v^*(s') \Big]
$$

For $q^*$,

$$
q^*(s,a) = r(s, a) + \gamma \sum_{s'} p(s' \mid s,a) \cdot \max_{a'} q^*(s', a')
$$

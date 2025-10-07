### Solution 4.1

$$
q_\pi(s,a) = \sum_{s',r} p(s',r \mid s,a) \Big[\, r + \gamma v_\pi(s') \Big]
$$

Since, the transition probabilities are deterministic, we can simplify the equation to:

$$
q_\pi(s,a) = r + \gamma v_\pi(s')
$$

$$
q_\pi(11, down) = -1 + 1(0) = -1
$$

$$
q_\pi(7, down) = -1 + 1(-14) = -15
$$

<br>

### Solution 4.2

Since the transition probabilities are deterministic and $\gamma = 1$, we can write the state-values as:

$$
v_\pi(s) = \sum_{a} \pi(a \mid s) \Big[ r + v_\pi(s') \Big]
$$

For the first scenario, where the $\text{up}$ action at state $15$ leads to the state $13$, we have:

$$
v_\pi(15) = -1 + 0.25 \Big[ v_\pi(12) + v_\pi(13) + v_\pi(14) + v_\pi(15)\Big]
$$

$$
v_\pi(15) = -1 + 0.25 \Big(v_\pi(15) -56\Big)
$$

$$
0.75 \cdot v_\pi(15) = -15
$$

$$
v_\pi(15) = -20
$$

For the second scenario, where the $\text{down}$ action at state $13$ also leads to the state $15$, we have:

$$
v_\pi(15) = -1 + 0.25 \Big[ v_\pi(12) + v_\pi(13) + v_\pi(14) + v_\pi(15)\Big]
$$

$$
v_\pi(15) = -1 + 0.25 \Big[ v_\pi(13) + v_\pi(15) - 36 \Big]
$$

$$
0.75 \cdot v_\pi(15) - 0.25 \cdot v_\pi(13) = -10 \tag{1}
$$

$$
v_\pi(13) = -1 + 0.25 \Big[ v_\pi(9) + v_\pi(12) + v_\pi(14) + v_\pi(15)\Big]
$$

$$
v_\pi(13) = -1 + 0.25 \Big[ v_\pi(15) -56 \Big]
$$

$$
v_\pi(13) - 0.25 \cdot v_\pi(15) = -15 \tag{2}
$$

Solving the two equations simultaneously, we get:

$$
v_\pi(15) = -20
$$

<br>

### Solution 4.3

Analog of (4.3) is:

$$
q_{\pi}(s,a) = \mathbb{E}_{\pi}\!\left[ R_{t+1} + \gamma \, q_{\pi}(S_{t+1},A_{t+1}) \;\middle|\; S_t = s,\, A_t = a \right]
$$

Analog of (4.4) is:

$$
q_{\pi}(s,a) = \sum_{s',r} p(s',r \mid s,a) \Big[ r + \gamma \sum_{a'} \pi(a' \mid s') \, q_{\pi}(s',a') \Big]
$$

Analog of (4.5) is:

$$
q_{k+1}(s,a) = \sum_{s',r} p(s',r \mid s,a) \Big[ r + \gamma \sum_{a'} \pi(a' \mid s') \, q_{k}(s',a') \Big]
$$

<br>

### Solution 4.4

We can update the policy improvement algorithm to only update the policy if there's a strict improvement in the value function if we pick the optimal action.

$policy\text{-}stable \leftarrow true$

For each $s \in \mathcal{S}$:

$\quad old\text{-}action \leftarrow \pi(s)$

$\quad \pi(s) \leftarrow \arg\max_a \sum_{s',r} p(s',r \mid s, a) \big[ r + \gamma V(s') \big]$

$\quad$ If $old\text{-}action \neq \pi(s)$, then $policy\text{-}stable \leftarrow false$

If $policy\text{-}stable$, then stop and return $V \approx v_*$ and $\pi \approx \pi_*$; else go to 2

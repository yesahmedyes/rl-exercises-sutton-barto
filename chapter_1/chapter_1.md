### Solution 1.1

Against an opponent that selects random actions, we learn a policy that can exploit the mistakes made by the opponent.

Whereas against an opponent that also learns through self-play, we will converge to a policy where the opponent also does not make mistakes. Therefore, we learn a safe policy that always leads to a draw.

So, yes, the policies learnt are different.

<br>

### Solution 1.2

Many positions are equivalent under rotations and reflections. If we map every such position to the same state, we will have fewer states to learn.

Therefore, we will learn faster and consume less memory.

If the opponent does not exploit these symmetries, the policies will still converge to the same policy, but it will take longer.

In practice, since the game isn't played an infinite number of times, the values of symmetric states could be different.

<br>

### Solution 1.3

If the player only chooses the greedy action, there is a chance that it will lock into a suboptimal policy. Whereas, a non-greedy (ε-greedy) player keeps exploring and thus discovers better strategies.

So, greedy play often learns worse policies than ε-greedy play because it fails to correct early mistakes.

<br>

### Solution 1.4

If we update the policy from all moves (including the exploratory ones), then the learnt policy represents our actual behavior policy (which includes exploration).

However, to learn a policy to maximize the expected reward, we need to update the policy from only the non-exploratory moves. The exploratory moves do not help us maximize the expected reward. Therefore, they are not part of the target policy.

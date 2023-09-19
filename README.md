# POLICY ITERATION ALGORITHM

## AIM
Write the experiment AIM.

## PROBLEM STATEMENT
Slippery Walk Five MDP
## POLICY ITERATION ALGORITHM

## POLICY IMPROVEMENT FUNCTION
```
def policy_improvement(V, P, gamma=1.0):
    Q = np.zeros((len(P), len(P[0])), dtype=np.float64)
    for s in range(len(P)):
      for a in range(len(P[s])):
        for prob,next_state,reward,done in P[s][a]:
          Q[s][a] += prob * (reward+gamma* V[next_state] * (not done))
    new_pi  = lambda s:{s:a for s,a in enumerate(np.argmax(Q,axis=1))}[s]
    return new_pi

# Finding the improved policy
pi_2 = policy_improvement(V1, P)
print_policy(pi_2, P, action_symbols=('<', '>'), n_cols=7)

print('Reaches goal {:.2f}%. Obtains an average undiscounted return of {:.4f}.'.format(
    probability_success(env, pi_2, goal_state=goal_state)*100,
    mean_return(env, pi_2)))

# Finding the value function for the improved policy
V2 = policy_evaluation(pi_2, P)
print_state_value_function(V2, P, n_cols=7, prec=5)

# comparing the initial and the improved policy
if(np.sum(V1>=V2)==7):
  print("The first policy is the better policy")
elif(np.sum(V2>=V1)==7):
  print("The second policy is the better policy")
else:
  print("Both policies have their merits.")
```
## POLICY ITERATION FUNCTION
```
def policy_iteration(P, gamma=1.0, theta=1e-10):
    random_actions = np.random.choice(tuple(P[0].keys()), len(P))
    # Write your code here to implement the policy iteration algorithm
    pi  = lambda s: {s:a for s , a in enumerate(random_actions)} [s]
    while True:
      old_pi  = {s:pi (s) for s in range (len(P))}
      V = policy_evaluation(pi, P, gamma, theta) 
      pi = policy_improvement(V,P,gamma)
      if old_pi == {s:pi (s) for s in range(len(P))}:
        break
    return V, pi
optimal_V, optimal_pi = policy_iteration(P)
print('Optimal policy and state-value function (PI):')
print_policy(optimal_pi, P, action_symbols=('<', '>'), n_cols=7)

print('Reaches goal {:.2f}%. Obtains an average undiscounted return of {:.4f}.'.format(
    probability_success(env, optimal_pi, goal_state=goal_state)*100,
    mean_return(env, optimal_pi)))

print_state_value_function(optimal_V, P, n_cols=7, prec=5)
```
## OUTPUT:

## RESULT:

Write your result here

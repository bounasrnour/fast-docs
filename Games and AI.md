## Games and AI

basic game ai techniques

- state machines (pac-man)
- path finding (RTS - warhammer)
- decisions trees (warcraft
- GOAP  goal oriented action planning 
- neural network

all these techniques wants to fulfil these tasks ability to move , make decisions where to move and think statically 

### agent based AI

In this context, agent-based AI is about producing autonomous characters that take in information from the game data, determine what actions to take based on the information, and carry out those actions.
it can be seen as a bottom up design 

## Genetic Algo 

 mimicking evolution. , first encoding the solution to the problem as a digital chromosome, create a start population of random chromosomes(each one representing a diff solution), evolve them over time by breeding.  Adding little mutation. At the end it will converge to a solution (no solution guaranteed ) 

Best Use : we do not need to know how to solve a problem , we only need to know how to encode it in a way the genetic algo mechanism can utilize

Example chromosome of len 12 : 011010011101

 

Logic: loop until a solution is found

\-    1 Test each chromosome to see how good it is at solving the problem and assign a gitness score accordingly

\-    2 Select two members from the current population, probability of being selected is dependent on the chromosome fitness(proportional), ROUTED WHEEL SELECTION

\-    3 Dependent on the crossover rate, crossover the bits from each chosen chromosome at a randomly chosen point

\-    4 In the chosen chromosome bits , flip dependent on the mutation rate

\-    5 Repeat step 2, 3 and 4 untill a new population of one hundred members has been created

End loop(generation) epoch is the entire loop 



## Roulette Wheel Selection

a method of choosing members from the population of chromosomes in a way that is proportinal to their fitness.

























 

 
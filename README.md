![alternate text](https://sourceforge.net/p/gatoolbox/wiki/Images/attachment/GA_framework.002.png/thumb)


# Open GA Toolbox

Genetic Algorithms are search heuristics designed to find good solutions to any problem model through bio-inspired heuristics. This is an open MATLAB toolbox to run a Genetic Algorithm on any problem you want to model. 

You can use one of the sample problems as reference to model your own problem with a few simple functions.

You can also collaborate by defining new example problems or new functions for the GA, such as scaling, selection or adaptation methods. In that case, you should then include your credits on the file, upload it to matlab central and contact the author.

Suggestions are also welcome but naturally I won't be able to attend all of them.


Using the toolbox for the first time
------------------

Save the toolbox in any folder you want and save it as a search path.
Go to the folder `sample_problems`, where you can find some examples of problems you can solve.

You can initialize a problem with the function `[problem name]_initialize`. For instance, for the knapsack problem, you should go to the folder knapsack and run:

    problem = knapsack_initialize();

The problem in the variable problem can now be optimized with the command:

    results = GA(problem);

You will be asked to choose the configuration you want for the GA. Those parameters will be discussed in a future section.

![alternate text](https://sourceforge.net/p/gatoolbox/wiki/Images/attachment/settings.png/thumb)

The GA is going to use the functions in the folder `[problem name]` (or `knapsack` in this example) to solve the problem. You can also change the default settings of the GA with the command:

    settings = initialize_settings();

And then change the settings you want you before you run the algorithm again with:

    results = GA(problem, settings);

You can use one of the sample problems to define your own problem or you can extend the genetic algorithm itself with new functions, such as scaling, selection, and adaptation methods. You can also collaborate by sharing those extensions!

You can get more help by typing:

    help GA;

Enjoy it!

Modeling a New Problem for the First Time
===========================

You can use one of the sample problems to help you model your own new problem.

You're going to need to define the evaluation function of a solution and change operators. The simplest sample example is the knapsack' problem, in the foldersample_problems`.

The knapsack problem
------------------------------

The folder knapsack shows the most basic functions needed to model a new problem:

![alternate text](https://sourceforge.net/p/gatoolbox/wiki/Images/attachment/files_knapsack.png)

So, the most basic functions needed to define a new problem are:

* Initialization: this function returns a struct that in fact defines the new problem. The struct indicates for example if it is a minimization or maximization problem.
* Solution generation: returns an initial solution for the problem. Usually, this can be a random solution. 
* Evaluation: returns the quality of a given solution for that problem.
* Crossover: given the population of solutions and the index of at least two parents, return an intermediary solution between those parents. This is the first class of change operators. You can define more than one crossover operator for the same problem.
* Mutation: given a solution, return a perturbation of that solution. This is the most basic change operator in stochastic optimization. You can also define more than one mutation operator for each problem.
* Print: this function is optional. It shows the partial results of the evolution. It can be used to show the best solution, the current population or the status of the evolution.

Settings
=========================

When you run the GA to solve your problem, you are going to see this window asking you for settings. 

![alternate text](https://sourceforge.net/p/gatoolbox/wiki/Images/attachment/settings.png)

You can also save those settings and use `GA(problem, settings)` if you don't want to see this window anymore.

The next section describes the possible parameters to be adjusted.

Change Operators
--------------------------

* Mutation Probability: This parameter decides the probability of a mutation in a solution. It is usual to keep this value relatively low as compared to the cross over rate so the search is not so random.
* Crossover Probability: This parameter decides the probability of a crossover between two selected parents. If the crossover does not occur, only one of the parents is copied and a mutation is applied to it.
* Parents per Crossover: It defines the number of parents involved in each crossover. The usual number is two, but it is also possible to define more than two parents for a crossover. In order to use more than two parents, it is important to make sure that the crossover function for the problem can is using all the list of parents given as input.
* Competition between parents and children: it gives the possibility of parents competing with children so old good individuals will remain in the population for longer. It is usual to let only the children survive in the following generation but highly elitist algorithms may work better with competition between parents and children.
* Adaptation Method: the crossover and mutation probabilities can be constant or variable, dynamically changing every generation. In the second case, the values can be adapted for the whole population or for each individuals, according to methods from the literature.
* Auto reinitialize population after Takeover: when it is recognized that more than 50% of the solutions have the same quality as the best solution, it means that the algorithms has converged to a final solution and therefore it might not be worth investing time in those solutions anymore and the population is regenerated with completely new solutions. 

Selection
---------------------------

* Elitism: a certain percentage of the best individuals goes always to the next generation. Low values are recommended for this parameter.
* Scaling Method: the quality of an individuals is not simple proportional to its fitness, or its probability of being chosen for the next generation. The quality of an individual can be mapped into fitness in many ways. Ranking scaling gives fitness 1, 2, 3, 4... to the worst individuals and ...n-3, n-2, n-1, n to the best individuals. Linear scaling transforms the values a in linear manner.
* Selection Method: the selection of the individual according to their fitness is also an stochastic process in which the bad individuals still have a chance to survive. This can be done by spinning a roulette wheel many times or doing tournaments of 2 individuals in which only the champion survives. 

Halting Criteria
----------------------------

When do we stop evolving the solutions?

* Maximum generations
* Maximum number of generations without improvement in the best solution known
* Maximum time

Other options
------------------------------

* Print partial results at every generation: this option requires the function `problemname_print.m` to work. You can use it to partially see the results of the process.
* Real Time Evolution Control: gives a window with the possibility to adjust the parameters in real time and analyze the changes.


Project Admin
============================

alandefreitas@gmail.com
www.alandefreitas.com

<a rel="license" href="http://creativecommons.org/licenses/by-nc/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-nc/3.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/3.0/deed.en_US">Creative Commons Attribution-NonCommercial 3.0 Unported License</a>.

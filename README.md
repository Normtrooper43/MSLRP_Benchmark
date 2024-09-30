# MSLRP_Benchmark
This repository contains the MSLRP benchmark data as well as the program that can evaluate and generate instances of the MSLRP.

The program is a java program called MSLRP_Benchmark.jar.

It can be executed with the following instruction:

"java -jar MSLRP_Benchmark.jar config.txt"

The program accepts one argument, config.txt which is the config file that tells the program what to do. This file can be called anything so long the argument and file name are consistent.

The program has two modes: evaluate and generate.

EVALUATE
For the evaluate function, the format of the config file is as follows:
eval: a string to tell the program to do the evaluate function
<type>: CG or RG for continuous or rotational grazing
<instances.txt>: a text file containing the names of all the instance files 
<sols.txt>: a text file containing the names of all the solution files.

An example looks like this:
eval
CG
insts.txt
sols.txt

The evaluate function will evaluate each instance in the insts.txt file using the corresponding solution provided in the sols.txt file. It assumes that each line of the insts.txt file corresponds to a line in the sols.txt file. So the first instance is matched to the first solution and so on. This allows for multiple solutions to be evaluated at the same time but the same instance can still be evaluated by multiple different solutions.

The output of the operation will be a list of instances and the fitness values associated with that instance.

GENERATE
The generate function will generate new instances of the MSLRP problem depending on its configuration. The format of the config file is as follows:
gen: a string to tell the program to do the generate function.
<type>: CG or RG for continuous or rotational grazing.
<gen_config.txt>: a text file containing the specs for problems to be generated. 
<inst_config.txt>: a text file containing the specs for the instances to be generated.

The format is similar to the evaluate function except that the two new variables are used to configure the generator for the problems.

The file gen_config.txt has two arguments:
numInstances: The number of instances to generate with the given configuration of variables.
numValidateTries: This is the number of tries the program has to attempt to generate a valid solution with at least one feasible solution. A large number will mean more chances to generate a solution but also increase the time required to generate that instance.

The file inst_config.txt has three arguments:
numAnimals: the number of animals for the instance.
numLocations: the number of locations for the instance.
numSlices: the size of the tensor for the problem.

With these two configurations set, the program will attempt to generate the specified number of instances. If the generation process fails, it means either that the number of validation tries were too small for the problem config, or the problem did not have a feasible solution.

With the current program, it is guaranteed to generate instances with at least one feasible solution depending on the number of the validation tries.

Please refer to the example files for a simple example of both functions.


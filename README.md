# hp-41_eval
## HP-41: EVAL simplifies the evaluation of cases against a requirement specification

A requirement specification consists of a set of requirements or "items". Each item is given a certain importance or "weight".

A requirement specification could be used to decide what piece of production equipment to buy, for choosing a new house or for choosing a new employee. If you are to choose a new employee, the specification would consist of items such as "relevant knowledge", "relevant job experience", "proven production record", "communication skills" or "empathy". You would give each item a certain weight where "relevant knowledge" could be given a weight of "4" while "empathy" for this specific job could be given "2" in weight. It doesn’t matter what minimum or maximum you choose for you "weight" scale, only the relative weight scores matters – like "relevant knowledge" being twice as important as "empathy" (their weight scores might as well have been "30" and "15").

When a requirement specification is populated with a set of weighted items, it’s time to pitch a set of cases against the specification. A case would be one of the candidates for a job or one of the houses you are looking at buying. A case is given a score on each item. You figure out the scale you want to use and put a score on each item of the requirement specification for the case you evaluate. The scale goes from "0" to any number you set as the maximum score. A candidate for a job could score a "3" on "relevant knowledge" and a "5" on empathy on a scale from "0" to "5". You then multiply the score with the item’s weight to get the "weighted score". So even though the candidate receives a maximum score on empathy, she only gets a weighted score of "10" on that item compared to "12" on "relevant knowledge".

Finally, you sum up all the weighted scores, divide by the sum of the item weights, divide by the maximum score and multiply with 100. Then you have a total percentage score of how well that case fits the requirement specification.

The formula for the total percent score is:

![alt text](graphics/eval.png?raw=true "Calculating weighted averages")

"T%" is the total percentage score, "w" is the weight, "v" is the score (value) of an item, v(max) is the maximum score possible.

The EVAL program makes all these evaluations a breeze. You run the program (XEQ "EVAL") and are prompted for a Project Name. The program calls each requirement specification "a project". Enter a name, and if the project does not exist as an Extended Memory file, a file is created and you are asked first for the maximum score you will use when evaluate the cases (the top of the scoring scale). Then you are asked to input the items, one by one using the format "WEIGHT:DESCRIPTION" in the Alpha register (such as "2:EMPATHY"). When you are done entering the items, just press R/S without entering anything on the prompt, and you are taken to the main menu. If a project file already exists, the program will pull that file up and take you directly to the main menu.

From the main menu, you can choose to add more items to the requirement specification, List the items in the file, EDit the file, or decide to enter a case with scores for each item in the requirement specification. Pressing "E" will always take you back to the main menu.

When you press "D" to enter a specific case, Flag 01 is set and the main menu changes. The program uses a "dynamic menu" to change labels A-E depending on whether you are handling the requirement specification or handling specific cases and evaluate them against the specification

The main menu for the cases include the ability to List the scores given on each item (or indeed change the scores already given), to evaluate the case against the requirement specification to yield a total percentage score, to enter another case or to go back to handling the requirement specification (Flag 01 is then cleared and the other menu is again activated). Again, pressing "E" while working with cases will get you back to the "case menu".

You may at any time press "d" to delete (purge) the current file you are working on, whether it is the requirement specification (the project file) or a case that you are working on.

Here is the key mapping (what shows in the programs menu is in parenthesis) when working with a project file (the requirement specification):

Label (Menu)	| Description
----------------|------------
EVAL	|Starts the EVAL program, asks for Project Name. If it exists, pulls that file into memory and takes you to the main menu for working with the project file. If a project file with that name does not exist, creates the file, asks for the maximum score you will use when giving scores for cases and then takes you to LBL A to input the items for this requirement specification.
LBL A (I+)	|Add an item to the requirement specification The program asks you to enter each item with the weight (a number), followed by a colon (":") and then the item’s name/description. When you are done entering items, simply press R/S without inputting anything and you are back at the main menu.
LBL B (L)	|List all the items in the project file.
LBL C (ED)	|EDit the project file. Note that the maximum score is saved in record 00 of the project file.
LBL D (C+)	|Enter a case to evaluate. The program prompts for a score for each item in the requirement specification. When all the items have been given a score, it calculates and displays the total percentage score for that case (how well the case fits the requirement specification as a total percentage).
LBL E (\*)	|Go back to the project menu.

While a project file is saved as an Extended Memory ASCII file, a case file is an Extended Memory DATA file. Here is the key mapping (what shows in the programs menu is in parenthesis) when working with a cases:

Label (Menu)	| Description
----------------|------------
LBL A (C+)	|Add another case to the project. (Same as LBL D from the project menu).
LBL B (L)	|List all the scores for each item for the current case. You may proceed to change each score.
LBL C (W\*V)	|Calculate the total percentage score for the current case against the current requirement specification.
LBL D (^)	|Move back up to working with the project file (takes you to the project menu).
LBL E (\*)	|Go back to the case menu.

# MDVRP Custom Dataset Generator

This repository contains a single Java program, MainData.java, which generates problem instance data files and corresponding solution files for a vehicle routing / drop-off coordination problem. The program prompts the user for a selected problem instance (one of the supported instances) and several parameters, then writes two output files:

- A problem data file: FINALDATA/p{instance}.txt
- A solution file: FINALSOLUTION/pr{instance}.txt

These paths are currently hard-coded to:
C:/Users/USER/Desktop/dropoff-coord/testdataset/FINALDATA/
and
C:/Users/USER/Desktop/dropoff-coord/testdataset/FINALSOLUTION/

If you run this on a different OS or machine, you will likely want to change those paths.

Table of contents
- What this does
- Supported problem instances
- Input (interactive prompts)
- Output (files and format)
- How to compile & run
- Example run
- Known issues & limitations
- Suggested improvements
- License & attribution

What this does
- Prompts the user for a problem instance (allowed values: 2, 3, 5, 9, 12, 15, 18, 21).
- For the chosen instance, asks for a set of integer parameters such as number of vehicles, number of customers, number of depots, deployment time, load capacity, number of orders, demands/frequencies, and starting/ending depot IDs.
- Generates a text file containing problem data (coordinates, demands, metadata) for that instance.
- Generates another text file containing an example/packed solution (objective value followed by routes) for that instance.

Supported problem instances
- 2, 3, 5, 9, 12, 15, 18, 21

Input (interactive prompts)
After starting the program you will be prompted with:
- Select problem instance (enter an integer from the supported list)
- For the chosen instance, the program will prompt for:
  - Number of vehicles
  - Number of customers
  - Number of depot(s)
  - Deployment time
  - Load capacity
  - Customer order count
  - Demand (kg)
  - Visit frequency
  - Number of visit combos
  - Starting depot (integer)
  - Ending depot (integer)

All inputs are expected as integers. The program does not currently validate ranges or types beyond Scanner's nextInt().

Output (files and format)
Two files are created per run. Their names are:
- FINALDATA/p{instance}.txt
- FINALSOLUTION/pr{instance}.txt

Example (for instance 2):
- FINALDATA/p2.txt — contains header lines with vehicle/customer/depot counts, then many numeric lines representing customers, depot coordinates, or metadata. The file uses whitespace-separated integers; some lines contain groups of fields and hard-coded coordinate entries.
- FINALSOLUTION/pr2.txt — contains an objective value on the first line (e.g., "473.53") and subsequent lines showing route definitions (start depot, end depot, elapsedTime, loadCap, endingDepot, sequence-of-stops, terminated with 0 etc.)

Note: The program writes many specific numeric entries (pre-defined customer coordinates/info) inside the code — these are not computed from inputs, they are fixed templates per instance.

How to compile & run
Requirements:
- Java JDK (tested with Java 8+). Any modern JDK should work.

From a command line in the directory containing MainData.java:

Compile:
javac MainData.java

Run:
java MainData

Follow the interactive prompts.

If you prefer to run from an IDE (IntelliJ IDEA, Eclipse, VS Code), import the file as a Java application and run the `main` method.

Example run (interactive)
1) Start the program:
java MainData

2) When prompted:
|++++++++++++++PROBLEM/SOLUTION GENERATOR++++++++++++++|
|+++++++       Enter the problem instance       +++++++|
|++++++++++++ (2, 3, 5, 9, 12, 15, 18, 21 +++++++++++++|

Enter: 2

It will then prompt:
|   Number of vehicles   =>  (enter integer)
|   Number of customers  =>  (enter integer)
...
|   Starting depot       =>  (enter integer)
|   Ending depot         =>  (enter integer)

After completion, two files will be created in the hard-coded directories.

Known issues & limitations
- File paths are hard-coded to a Windows absolute path. On other machines or OSes you must modify:
  - "C:/Users/USER/Desktop/dropoff-coord/testdataset/FINALDATA/" and
  - "C:/Users/USER/Desktop/dropoff-coord/testdataset/FINALSOLUTION/"
- No input validation: entering a non-integer will throw an InputMismatchException.
- Scanner is not closed; file writers are closed but not always with try-with-resources (some writers are closed inside if branches).
- The program uses many magic numbers and duplicated code blocks for each supported instance; it is not DRY and difficult to maintain.
- The program throws IOException in the main signature even though it also catches IOExceptions inside — this is confusing.
- Many numeric lines inside the program are hard-coded templates; they may not reflect arbitrary inputs.
- No unit tests or automation; everything is interactive.



# Using a bash script to complete Lab Report 4

In Lab Report 4, I wrote all the steps I took to fix the error in ListExamples. However, this was time consuming and took a lot of effort to type in commands. So in this lab report, I will be creating a bash script to automatically perform all these commands for me. The bash script will loging to the remote ieng6 computer, clone the repository, fix the error, run JUnit tets, and push the fixed file back to the repository. All of this can be done by running a single command.

However, to do this we will need two bash scripts. The first bash script (script.sh) will contain all the commands as described above, except logging in to the remote computer. The second bash script (fixErrors.sh) will login to the ieng6 computer using ssh and then take script.sh as an input parameter and run all the commands on the remote computer.

![image](https://user-images.githubusercontent.com/61783850/224609868-c9b865f6-91e9-4638-9c2b-86cd5ac40587.png)

## script.sh
Here is the code in script.sh:
```
git clone git@github.com:Akhil-py/lab7.git
cd lab7
javac -cp .:lib/hamcrest-core1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests

sed -i '43s/index1 += 1;/index2 += 1;/' ListExamples.java

javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java 
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests 
git add .
git commit -m "Fixed Errors"
git push
```

## fixErrors.sh
Here is the code in fixErrors.sh:
```
ssh cs15lwi23afv@ieng6.ucsd.edu 'bash -s' < script.sh
```

## How to run the script
To run the script, all you have to do is type `bash fixErrors.sh` in the terminal.

![image](https://user-images.githubusercontent.com/61783850/224610832-35dfe6c7-0ac3-4e26-97ba-a51994cfb19b.png)

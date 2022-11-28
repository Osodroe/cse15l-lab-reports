# Week 9 – Grade Server

For this week, we put together a bash script that will automatically grade a github repository. The grader will then output some information about your grade, such as if it failed to complile or if you failed a test. 

Here is the code of my grade.sh:

```
CPATH=".;./lib/hamcrest-core-1.3.jar;./lib/junit-4.13.2.jar"

rm -rf student-submission > out.txt 2> out-err.txt
git clone -q $1 student-submission/ > git.txt 2> git-err.txt

FPATH=$(find student-submission/* -type f)

if [ $? -eq 0 ]
then   
    echo "Clone succeeded"
else
    echo "Repository not found"
    exit 1
fi

FFILE=$(basename $FPATH)

if [[ $FFILE == "ListExamples.java" ]]
then
    echo "File found"
else   
    echo "$FFILE is incorrect file name"
    exit 1
fi

FDIR=$(dirname $FPATH)

cp TestListExamples.java $FDIR
cp -r lib $FDIR
cd $FDIR

javac -cp $CPATH *.java > compile.txt 2> compile-err.txt

if [ $? -eq 0 ]
then
    echo "Compile succeeded"
else
    echo "Your program didn't compile"
    exit 1
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > result.txt 2> result-err.txt

grep -q "OK" result.txt 

if [ $? -eq 0 ]
then 
    echo "4/4, perfect score!"
    exit 0
else
    SCORE=$(grep -o 'Failures: [1-4]' result.txt | grep -Eo '[1-4]+')
    let "SCORE = 4 - SCORE"
    echo "$SCORE/4."
    cat result.txt
    exit 0
fi
```

Here is my grader testing three different repositories:

[Repository 1](https://github.com/ucsd-cse15l-f22/list-methods-corrected)  

A perfect test, this code ran with no errors and passed all tests.
 
![Example 1](/cse15l-lab-reports/labs/images/lab-6/Example1.png)

[Repository 2](https://github.com/ucsd-cse15l-f22/list-methods-compile-error)

This test failed to compile, which should have been checked before submitting. The grader cannot grade any further.

![Example 2](/cse15l-lab-reports/labs/images/lab-6/Example2.png)

[Repository 3](https://github.com/ucsd-cse15l-f22/list-examples-subtle)

This code can compile, but has some error so a test is failed. A grade of 3/4 is given and the test that failed is shown. 

![Example 3](/cse15l-lab-reports/labs/images/lab-6/Example3.png)

We will now walk through this third example.

First we remove any old student-submission folder, saving the standard output and standard error into some text files, which are empty in this case. 

Then we clone the given repository, once again saving the standard ouput and error to some text files. Since the repository is valid, these text files are empty. 

Then comes our first if, which tests that the git clone ran successfully. Since $? is 0 for this repository, the argument is true and the user is informed. Since the argument is true, lines 14 and 15 are never run.

Now there is another if, this time making sure that a file of the correct name is found in the repository. Since it is found, the argument is true and the user is informed. Because of this, line 24 and 25 are never run. 

Afer copying the proper files into the student-submission/, we move in and compile everything in the working directory. We save the standard output and error, both of which are empty. 

After, we once again check $?, and since the compile was successful the return code was 0 and the argment is true. However, line 40 and 41 are never run. 

The tests are then run, with the standard output and error once again being saved. In this case, the standard output was not empty, containing 

```
JUnit version 4.13.2
..E..
Time: 0.009
There was 1 failure:
1) merge2(TestListExamples)
java.lang.AssertionError: expected:<[crab, power, sand, sandwich, sandwich, towers]> but was:<[crab, power, sand, sandwich, towers]>
	at org.junit.Assert.fail(Assert.java:89)
	at org.junit.Assert.failNotEquals(Assert.java:835)
	at org.junit.Assert.assertEquals(Assert.java:120)
	at org.junit.Assert.assertEquals(Assert.java:146)
	at TestListExamples.merge2(TestListExamples.java:75)

FAILURES!!!
Tests run: 4,  Failures: 1

```

Finally, we have the last if statement, which once again checks $?. This time, the return code represents whether or not "OK" was found in the result, which is not true in this case. So, line 50 and 51 are never run. So, lines 53-57 are run outputting the grade fouhnd and the results of the test before exiting. 
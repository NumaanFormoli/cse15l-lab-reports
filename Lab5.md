# Lab Report 5: Finishing Grading Script
---
Code for Grading Script:
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

# Removes previous submission and clones new one in student-submission directory
rm -rf student-submission
git clone $1 student-submission
echo 'Finished cloning'


cd student-submission

# Checks if they have correct file
if [[ -f "ListExamples.java" ]]
then
    echo "ListExamples found"
else
   echo  "need ListExamples"
   exit 1
fi

# takes file out of directory to compile
cp ListExamples.java ..
cd ..

javac -cp $CPATH *.java 2> javac-errs.txt

# If compile fails, show the error and exit
if [[ $? -ne  0 ]]
then
    cat javac-errs.txt
    exit 1
fi

# run the testListExamples.java against the ListExamples.java using JUnit
java -cp $CPATH org.junit.runner.JUnitCore TestListExamples 2>java-error.txt > results.txt

#Show results
cat results.txt

# Show the score
sed '2,2!d' results.txt > score.txt

FAILURES="$(tr -cd 'E' < score.txt | wc -c)"
SUCCESSES="$(tr -cd '.' < score.txt | wc -c)"

SUCCESSES=`expr $SUCCESSES - 1`
total=`expr $FAILURES + $SUCCESSES`

echo "Score: "
PERCENTAGE=`expr 100 \* $SUCCESSES / $total`
echo $PERCENTAGE "%"
```
- I approached this grading script step by step making sure not to take on too much. I would first ensure that I could find the right files and that the bash script could find the necessary JUnit components. I did this using `if`. This ensured that I didn’t have any issues on my end when testing for errors in the students’ code. I then wrote another test method to test the filter method of the ListExamples.java file. I then ran it against 5 of the listed examples and it proved to be accurate. I tested if compilation worked using if `[[ $? -ne  0 ]]` to see if the exit code was anything but 0. 
- One issue I had was trying to determine the percentage. I settled on using `tr -cd 'E' < score.txt | wc -c` to find the number of failures and successes so this code would still work despite the JUnit tests being replaced. It worked by counting the number of '.' and 'E' which represents number of failures and passed tests.



1. https://github.com/ucsd-cse15l-f22/list-methods-lab3: Same starter code from Lab 3
    ![Image](Screen Shot 2023-03-13 at 5.49.07 PM.png)
2. https://github.com/ucsd-cse15l-f22/list-methods-corrected: Corrected code
    ![Image](Screen Shot 2023-03-13 at 5.49.31 PM.png)
3. https://github.com/ucsd-cse15l-f22/list-methods-compile-error: Missing a Semicolon
    ![Image](Screen Shot 2023-03-13 at 5.49.53 PM.png)
4. https://github.com/ucsd-cse15l-f22/list-methods-signature: types for the arguments of filter in the wrong order
    ![Image](Screen Shot 2023-03-13 at 5.50.32 PM.png)
5. https://github.com/ucsd-cse15l-f22/list-methods-filename
    ![Image](Screen Shot 2023-03-13 at 5.51.21 PM.png)
7. Challenge https://github.com/ucsd-cse15l-f22/list-examples-subtle: Subtle bugs
    ![Image](Screen Shot 2023-03-13 at 5.52.45 PM.png)

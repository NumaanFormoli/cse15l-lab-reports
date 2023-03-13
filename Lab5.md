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

FAILURES="$(grep -c "E" score.txt)"
SUCCESSES=`grep -c "." score.txt`

total=`expr $FAILURES + $SUCCESSES`

echo "Score: "
echo $SUCCESSES / $total

```

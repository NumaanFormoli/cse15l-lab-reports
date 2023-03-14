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
- I approached this grading script step by step making sure not to take on too much. I would first ensure that I could find the write files and the bash script could find the necessary JUnit components. This ensured that I didn't have any issues on my end when testing for errors in the students' code. I then wrote another test method to test the filter method of the ListExamples.java file. I then ran it against 5 of the listed examples and it proved to be accurate. One issue I had was trying to determine the percentage. I settled on using `tr -cd 'E' < score.txt | wc -c` to find the number of failures and successes so this code would still work despite the JUnit tests being replaced.


1. https://github.com/ucsd-cse15l-f22/list-methods-lab3: Same starter code from Lab 3
    ![Image](logIn.png)
    
2. https://github.com/ucsd-cse15l-f22/list-methods-corrected: Corrected code
    ![Image](logIn.png)
3. https://github.com/ucsd-cse15l-f22/list-methods-compile-error: Missing a Semicolon
    ![Image](logIn.png)
4. https://github.com/ucsd-cse15l-f22/list-methods-signature: types for the arguments of filter in the wrong order
    ![Image](logIn.png)
5. Challenge https://github.com/ucsd-cse15l-f22/list-examples-subtle: Subtle bugs
    ![Image](logIn.png)

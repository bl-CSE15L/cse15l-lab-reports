# **Lab Report 5 - Putting It All Together**   
In this lab report, I reflect on my learning throughout the quarter by creating a debugging scenario.

---   

## Debugging Scenario:   

### grade.sh "error: cannot find symbol" #000         
#### [Example Student]   
Hello, I've been having this bug in my grading script where it can't find any of the JUnit tests when using it remotely on the ieng6 machines but it works on my machine. Is it because I'm on the broken ieng6 machine?   

Symptom:   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/2dbb4dfa-d4b1-4bce-a9b7-e0f37100b791)   

grade.sh code:   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/a01c1183-65d2-4ee2-b379-f2dc4b5e6fc3)   

#### [Example TA]
Currently, only the ieng-203 machine is not working. You are on the 201 machine as evidenced by the Prompt in the command line ```[<username>@ieng-201]```. Think carefully about how your personal machine functions differently from the remote machines here at UCSD. It appears your device runs a Windows OS while the machines use Unix. How might this difference affect the behavior of your code?   

#### [Example TA]   
Ah I see. The classpath we use is os-dependent so I can't use the Windows classpath on a Unix system meaning I have to change it using Vim. Thanks so much!   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/b8689294-4709-4e72-a1f2-37928f99b405)   


### File & Directory Structure:   
```
.
├── grader-review
│   ├── grading-area
│   │   ├── lib
│   │   │   ├── hamcrest-core-1.3.jar
│   │   │   └── junit-4.13.2.jar
│   │   ├── ListExamples.java
│   │   └── TestListExamples.java
│   └── lib
│       ├── hamcrest-core-1.3.jar
│       └── junit-4.13.2.jar
├── student-submission
│   └── ListExamples.java
├── grade.sh
├── GradeServer.java
└── Server.java
```

### grade.sh [BEFORE]
```
CPATH='.;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

if [[ -f student-submission/ListExamples.java ]]
then
    echo "ListExamples.java found"
else
    echo "ListExamples.java not found!"
    exit 1
fi

cp -r lib grading-area
cp student-submission/ListExamples.java grading-area/
cp TestListExamples.java grading-area/

cd grading-area
javac -cp $CPATH *.java

if [[ $? -ne 0 ]] 
then 
    echo "Compile error!"
    exit 1
else    
    echo "Compiled successfully"
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > junit-output.txt

lastLine=$(tail -n 2 junit-output.txt | head -n 1)
tests=$(echo $lastLine | awk -F'[, ]' '{print $3}')
failures=$(echo $lastLine | awk -F'[, ]' '{print $6}')

if [[ $tests =~ ^[0-9]+$ ]]; then
    successes=$((tests - failures))
    echo "Score: $successes / $tests"
else
    echo "All tests passed!"
fi
```
### grade.sh [AFTER]
```
CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

if [[ -f student-submission/ListExamples.java ]]
then
    echo "ListExamples.java found"
else
    echo "ListExamples.java not found!"
    exit 1
fi

cp -r lib grading-area
cp student-submission/ListExamples.java grading-area/
cp TestListExamples.java grading-area/

cd grading-area
javac -cp $CPATH *.java

if [[ $? -ne 0 ]] 
then 
    echo "Compile error!"
    exit 1
else    
    echo "Compiled successfully"
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > junit-output.txt

lastLine=$(tail -n 2 junit-output.txt | head -n 1)
tests=$(echo $lastLine | awk -F'[, ]' '{print $3}')
failures=$(echo $lastLine | awk -F'[, ]' '{print $6}')

if [[ $tests =~ ^[0-9]+$ ]]; then
    successes=$((tests - failures))
    echo "Score: $successes / $tests"
else
    echo "All tests passed!"
fi
```

### Lines to Trigger Bug:
```bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected```   

### Bug-Fix:   
Change classpath separator from ```;```(Windows) to ```:```(Unix)   
```CPATH='.;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar'``` >>> ```CPATH='.:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar'```
#### Keys & Commands:   
```
vim grade.sh <enter>
2e
r <shift + ;>
12e
r <shift + ;>
:wq! <enter>
bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected
```

## Reflection:   

I really enjoyed learning how to do more actions from the command line such as how to navigate across directories and files and learning how to edit files using Vim. I also enjoyed learning about SSH and how to remotely access machines. It was really engaging to note the differences in working locally versus working remotely and getting the nuance between the two was an exciting challenge. Overall I had a lot of fun this quarter and I hope to take my experience and lessons learned from this class far into my future career.

# **Lab Report 4 - Vim**   
In this lab report, I reflect on my learning using Vim as a text editor and various Vim shortcuts through the use of an example repository.

---   

## Logging on ieng6:   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/25be46bb-063e-4643-8d45-a576c9d02b66)   
Here I run a ```ssh``` command to log onto one of the ieng6 machines remotely on my computer.   
### Keys & Commands:   
```
ssh blappay@ieng6.ucsd.edu <enter>
cs15lwi24 <enter>
```
## Cloning Fork:
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/61dadbe3-e262-42a6-8607-fd2af15d0488)   
Here I run a ```git clone``` command to clone a fork of the example repository.   
### Keys & Commands:   
```
git clone https://github.com/bl-CSE15L/lab7 <enter>
```   
## Running Tests w/ Failures:   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/c783a64b-1f14-4c1f-98fc-6fe2986058b0)   
Here I run the ```test.sh``` file to test the program revealing bugs. I used ```cd``` and ```ls``` to find and run the testing file.   
### Keys & Commands:   
```
cd lab7/ <enter>
ls <enter>
bash test.sh <enter>
```
## Debugging:   
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/2787623c-a2b1-4a18-9fb3-e33e6398c945)  
Here I use ```vim``` and various ```vim``` commands to debug the program in line 44. ```43j``` moves me down 43 lines to line 44 where the bug is. ```e``` moves me to the end of the next word which in this case is ```1``` in ```index1```. ```r2``` replaces the character at my cursor with ```2``` so ```index1``` becomes ```index2```. I then save and quit with ```:wq!```.   
### Keys & Commands:   
```
vim ListExamples.java <enter>
43j
e
r2
:wq! <enter>
```
## Running Tests 
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/ad8951cc-b522-4c03-90eb-7b946abbc2ba)   
Here I run the ```test.sh``` file once more after fixing the bug showing all my tests now pass. I use terminal keyboard shortcuts to input that command instead of typing it all out again. I pressed the ```<up>``` key because the ```bash test.sh``` command was 2 up in my command history.   
### Keys & Commands:   
```
<up> <up> <enter>
```
## Commiting & Pushing to Git
![image](https://github.com/bl-CSE15L/cse15l-lab-reports/assets/156377155/6aff8105-aba1-4c79-97d9-0f79fd3a691e)   
Here I used ```git``` commands to save my changes to my repository.
```
git commit -a -m "lab report" <enter>
git push origin main <enter>
bl-CSE15L <enter>
<"password/token"> <enter>
```

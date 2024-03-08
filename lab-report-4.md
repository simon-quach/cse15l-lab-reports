# Lab Report 4

I logged into ieng6 using `ssh siquach@ieng6-201.ucsd.edu`.

<img width="752" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/bdf88ecb-9e80-48a7-a4bf-0d0221c90020">

<br/>

Then I cloned my forked repository using the ssh url with this command: `git clone git@github.com:simon-quach/lab7.git`.

<img width="752" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/ef0b5739-3817-4d57-96a0-8313672e52c2">

<br/>

Next, I ran `cd lab7` to set the new directory as my working directory. So now my working directory should be `/lab7`.

To demonstrate that the test cases fail, I first have to compile the code using `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java`. I ran the tests using `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests`. Once I ran that command, there were 2 tests that were run and 1 failure.

<img width="752" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/c1a72bb6-6fd5-4860-b42d-4854b228015c">

<br/>

To start editing `ListExamples.java`, I ran the command `vim ListExamples.java` to start editing the file using `vim`. 

Keys pressed:`<down>*37 <right><right><right><right><right>, r2, :wq`.

I used `r` in vim in order to replace the character under the cursor, 1, with 2. Then I ran the command `:wq: to save the new changes and quit out of the file.

<img width="752" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/0e2977c5-2404-4221-88dd-63d74807dda2">

<br/>

I have to compile the code using `javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java`. I ran the tests again using `java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests`. Once I ran that command, both tests were able to pass.

<img width="752" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/4af379eb-9a7c-42ba-bb06-888044c046a2">

<br/>

In order to commit and push the changes to my remote repository, I used `git add .` to add all of my changes in my current working directory to the staging area. This should add the file `ListExamples.java` to the staging area because it was the only file that was changed. Once this is done, I used `git commit -m "fix failed test case"` to commit the staged changes with the message "fixed failed test case". The `-m` option is what allows you to add a message to your git commit. Once that is done, I ran `git push`, which pushes my commit to the remote repository on Github.

<img width="631" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/b384c7e4-c1f4-420a-9086-93e9f7d88a3d">


# Part 1 - Debugging Scenario

## Student Message
Hi! I'm having an issue with the code that I am writing. I'm writing a function called `merge` that merges two sorted lists of strings (`list1` and `list2`) into one sorted list. When I run `grade.sh` to test if my code works, it fails one of the test cases. I am getting this error: `org.junit.runners.model.TestTimedOutException: test timed out after 500 milliseconds`. I assume my code is not optimized well enough, but I can't seem to figure out what's wrong. Here is a screenshot of my error code and my tester code:

<img width="622" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/44469dbb-6815-452b-8436-fd2375aeebfd">
<img width="527" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/f9eb961b-b9a7-47a9-95e3-ecdf08667b0e">

## TA Message
Hi! Thanks for reaching out. It seems that there is most likely something wrong with the function that you wrote. Can you send a screenshot of your code?

## Student Message
Here is a screenshot of my `merge` function:

<img width="527" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/1eb32b87-2215-42f7-a95d-c136ccf3bc42">

## TA Message
The bug is located in the very last `index1 += 1` line, inside of the `while (index2 < list2.size())` loop. Instead of `index1`, it should be `index2`, because in this while loop, you're supposed to increment the second index to loop through the second list, or else it will be stuck in an infinite loop. Here is the corrected code:

<img width="527" alt="image" src="https://github.com/simon-quach/cse15l-lab-reports/assets/43255108/96e0c793-ce54-4196-92c8-8269a386c5ec">
